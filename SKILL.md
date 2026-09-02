---
name: "webapp-testing-checklist"
description: "Walk a web application penetration test through the OWASP Web Security Testing Guide (WSTG) methodology as a structured checklist, and produce WSTG-numbered findings. Covers all 12 WSTG categories (Information Gathering, Configuration, Identity, Authentication, Authorization, Session Management, Input Validation, Error Handling, Cryptography, Business Logic, Client-side, API). This is a checklist and report-generation aid for a human-led engagement, in backseat mode — normal benign traffic (viewing pages, following links, submitting ordinary form input) is fine, but it never sends attack payloads, injection strings, exploit attempts, or runs a scanner; actual security testing is the tester's job with their own tooling (Burp, ZAP, etc.), and this skill interprets the evidence they paste back. Trigger when the user wants to plan, scope, or track a web app pentest against WSTG, wants a structured findings report with WSTG IDs, says things like \"run this through WSTG\", \"OWASP testing guide checklist\", \"pentest checklist for this app\", or is doing manual/tool-assisted testing and wants help organizing coverage and writing up results."
---

# Webapp Testing Checklist (WSTG-aligned)

Structures an authorized web application penetration test around the OWASP Web Security Testing
Guide (WSTG) methodology, tracks checklist coverage, and turns tester-supplied evidence into a
findings report with WSTG IDs. **This skill operates in backseat mode — it never drives the
actual security testing.** Normal, benign application traffic (viewing pages, following links,
submitting a form with ordinary non-malicious input — the same traffic any regular user or the
tester's own browser generates) is fine when it's useful for gathering checklist context. What it
never does: send a payload, injection string, exploit attempt, or fuzz input, or run an automated
scanner. The human tester runs actual security testing with their own tools (Burp Suite, ZAP,
curl, browser devtools, etc.) within their existing authorized engagement; this skill's job is the
checklist, the diagnostic questions per test, interpreting the evidence the tester hands off
(including raw Burp/ZAP request-response captures, via the evidence directory convention in Step
3), and the report.

## Step 1 — Authorization gate (required, do not skip)

Before doing anything else, confirm all of the following. If any is missing, stop and explain
what's needed instead of proceeding — do not walk the checklist without this confirmed:

1. **Written authorization** to test the specific target exists (signed SOW, pentest agreement,
   or equivalent) — ask the tester to confirm this explicitly, don't assume it because they're
   using the skill.
2. **Named engagement and target scope** — client/engagement name (or an internal code name if
   the tester wants to avoid naming a real client in this conversation — flag if they paste a
   real client name and suggest a placeholder instead, per standard data-handling hygiene), and
   the specific hostnames/apps/IP ranges in scope.
3. **Testing window / rules of engagement** — any time restrictions, excluded tests (e.g. no DoS,
   no destructive testing on prod), and points of contact.
4. **Test credentials and accounts** — ask whether the tester will provide existing test
   credentials, how many accounts, and what access role each represents (e.g. anonymous/guest,
   standard user, admin, multiple tenants) — this determines which role-based checks (privilege
   escalation, IDOR, authorization bypass) can actually be covered. Also ask directly: **is
   creating new accounts in the target application in scope?** Default to **no** unless the
   tester confirms the SOW explicitly authorizes test-account creation — see the account-creation
   guardrail below.

   **Never ask the tester to paste actual credentials into the prompt/conversation.** Instead, ask
   them to create a plain text file in the current working directory (suggested name:
   `test-credentials.txt`) with one account per line:

   ```
   label | role | username | password
   admin-1 | admin | testuser | ExamplePlaceholder-ChangeMe
   ```

   Read that file yourself once at the start of the engagement to learn the accounts, then refer
   to accounts by `label` only for the rest of the session and in the report — never repeat the
   username/password back into the conversation or write them into the report. Remind the tester
   this file contains live secrets: it should be `.gitignore`d if the working directory is a git
   repo, and deleted once the engagement is done. If the tester pastes credentials directly into
   the conversation anyway, don't echo them back — acknowledge receipt by label/role only and
   suggest the file-based approach for next time.

Record this once at the start of the session/engagement; don't re-ask on every message within the
same conversation. Never write actual credential values (passwords, API keys, session tokens) into
the report or restate them back into the conversation — track accounts by role/label only (e.g.
"standard-user-1", "admin-1").

## Step 2 — Scope intake

Ask what kind of application this is, since it determines which of the 12 WSTG categories in
`references/` actually apply:

- Server-rendered web app → all categories likely apply.
- API-only (no browser UI) → `references/12-api-testing.md` plus the API-relevant tests called out
  in categories 4 (Authentication), 6 (Session/Token), 7 (Input Validation), and 10 (Business
  Logic) — skip most of `11-client-side.md`.
- SPA with a backend API → both client-side (11) and API (12), plus the rest.

Confirm with the tester which categories to walk, and in what order (default: numeric order,
`references/00-overview.md` through `12-api-testing.md`).

## Step 3 — Walk the checklist

For each in-scope category, load its file from `references/` (don't load all 12 up front — load
one at a time as you reach it, to keep context focused). For each test ID in that file:

1. State the test ID, title, and what it verifies (from the reference table).
2. For tests that need the tester's own hands-on testing (most tests outside Information
   Gathering), prompt with two explicit options and let the tester pick either, per test:
   - **Provide evidence** — via the evidence-directory convention below; assess it against this
     test's criteria and record both the verdict and the evidence.
   - **Just the verdict** — tell the skill Pass/Fail/Not Applicable directly, no evidence
     required. Record the verdict, and note evidence as "not captured in this session — tester to
     add manually" so the report never implies evidence exists when it doesn't.

### Evidence directory convention

The first time a tester wants to provide evidence in a session, explain this convention (don't
make them ask for it, and don't ask them to paste raw request/response text or screenshots
directly into the conversation — a file-based handoff keeps the transcript clean and gives the
engagement a permanent evidence archive):

- Create `~/wstg-evidence/` if it doesn't already exist (a plain local directory, not inside any
  git repo — it holds raw request/response captures and screenshots, which shouldn't be
  version-controlled).
- **One subdirectory per finding/test, named exactly with the WSTG test ID** — e.g.
  `~/wstg-evidence/WSTG-INPV-02/`, `~/wstg-evidence/WSTG-AUTHZ-04/`.
- Inside each subdirectory:
  - **`evidence.txt`** — the raw GET/POST request **and** the raw server response, in one file,
    clearly separated:
    ```
    === REQUEST ===
    GET /engagements/2/ HTTP/1.1
    Host: target.example:8001
    Cookie: sessionid=...

    === RESPONSE ===
    HTTP/1.1 200 OK
    Content-Type: text/html

    <h1><script>alert(document.cookie)</script> / ...</h1>
    ```
  - Any supporting **screenshot(s)**, saved directly in that same subdirectory (e.g.
    `screenshot-01.png`, numbered if there's more than one).
- **Evidence that isn't tied to a single request/response pair** — e.g. an nmap/Nessus/Nikto scan
  output supporting WSTG-INFO-04 (Attack Surface Identification) or a broader recon artifact —
  goes directly under `~/wstg-evidence/` with a descriptive filename (e.g. `nmap.txt`,
  `nikto-scan.txt`), not inside a per-finding subdirectory, since it isn't scoped to one test ID.
- Once a subdirectory or file is ready, the tester just needs to say the WSTG ID (or filename) —
  read it directly from disk rather than asking them to paste the content into chat.
3. Record the result: **Pass**, **Fail (finding)**, **Not Applicable** (with a one-line reason —
   e.g. "no file upload feature in this app" for WSTG-BUSL-08/09), or **Not Tested** (out of time/
   scope for this pass — note it as a coverage gap, not a pass).
4. If it's a finding, capture: severity, evidence, affected location (URL/param/endpoint), and a
   remediation recommendation.

Point the tester to the full WSTG page for methodology detail on any specific test if they want it:
`https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/<NN-Category>/<NN-Test_Name>`

## Step 4 — Report

Before generating, ask which format(s) the tester wants: **Markdown** (default), and/or **Word
(.docx)**, and/or **PDF**. More than one is fine — generate each requested format using whatever
document-generation capability is available in the current environment.

Produce a report with:

- **Notes** (top of report, before the engagement summary):
  - Methodology disclaimer: OWASP WSTG-aligned, this is not an official OWASP-endorsed tool (see
    README).
  - Recommendation: pair this dynamic/checklist pass with a **Claude-based source code security
    review** (e.g. the `security-review` skill/capability) when code-level review is included in
    the SOW and the application owner has provided source access — this checklist only covers
    dynamic/black-box testing and doesn't substitute for a code-level review, and vice versa.
- **Engagement summary**: target(s), dates, tester, methodology, categories in scope, and the test
  accounts used this pass by role/label only (e.g. "standard-user-1", "admin-1") — never actual
  credential values.
- **Coverage table**: per category, count of Pass / Fail / N/A / Not Tested, so gaps are visible
  at a glance rather than buried.
- **Findings register**, sorted by severity (Critical → Info), each entry: WSTG ID, title, severity,
  affected location, description, evidence, recommendation.
- **Appendix**, for audit trail / due-diligence purposes:
  - **Not Tested** — every test marked Not Tested, with its one-line coverage-gap reason.
  - **Pass** — every test marked Pass, with whatever evidence was provided for it (or noted as
    "verdict only, no evidence captured" per the Step 3 options).
  - **Not Applicable** — every N/A test with its one-line reason.

## Guardrails

- **Credentials come from a file, never from the prompt.** Ask the tester to write test accounts
  to `test-credentials.txt` (or similar) in the working directory per Step 1 — don't solicit
  passwords in chat, don't echo any credential value back if they paste one anyway, and refer to
  accounts by label/role only everywhere else, including the report.
- **Backseat, never driving.** Normal benign traffic — viewing a page, following a link, submitting
  a form with ordinary non-malicious input — is fine when it helps gather checklist context or
  confirm scope. Never send a payload, injection string, exploit attempt, fuzz input, or anything
  designed to probe or validate a vulnerability, and never run an automated scanner. If the tester
  asks you to "just try" something that would require a payload or attack traffic, redirect them
  to test it with their own tooling (Burp, ZAP, etc.) and hand back the request/response evidence
  via the evidence directory convention above — don't attempt it yourself, and don't judge whether
  something is exploitable by trying it.
- **Never create an account in the target application on your own initiative.** Even though
  normal form submission is otherwise fine under backseat mode, account/registration creation is
  out of scope unless (a) the tester has confirmed the SOW explicitly authorizes test-account
  creation, and (b) the tester gives real-time go-ahead for that specific account at the point
  it's needed (e.g. an Identity Management registration-abuse test). Until both are true, treat it
  as not permitted and ask the tester to supply existing test credentials instead.
- Business logic (category 10) and parts of Authorization/Session testing require understanding
  *this specific app's* intended behavior — don't mechanically mark these "Pass" without the
  tester describing the actual workflow; flag them as needing more context if unclear.
- A clean run through this checklist is not a certification and doesn't guarantee the absence of
  vulnerabilities — WSTG itself isn't exhaustive, and this skill's summaries are shorter than the
  full WSTG guidance. Say so in the report, don't imply completeness the testing didn't achieve.
- If the tester hasn't confirmed authorization (Step 1), do not proceed past scope intake.
