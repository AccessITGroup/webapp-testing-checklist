---
name: "webapp-testing-checklist"
description: "Walk a web application penetration test through the OWASP Web Security Testing Guide (WSTG) methodology as a structured checklist, and produce WSTG-numbered findings. Covers all 12 WSTG categories (Information Gathering, Configuration, Identity, Authentication, Authorization, Session Management, Input Validation, Error Handling, Cryptography, Business Logic, Client-side, API). This is a checklist and report-generation aid for a human-led engagement — it does not send requests to any target, run scanners, or perform testing itself. Trigger when the user wants to plan, scope, or track a web app pentest against WSTG, wants a structured findings report with WSTG IDs, says things like \"run this through WSTG\", \"OWASP testing guide checklist\", \"pentest checklist for this app\", or is doing manual/tool-assisted testing and wants help organizing coverage and writing up results."
---

# Webapp Testing Checklist (WSTG-aligned)

Structures an authorized web application penetration test around the OWASP Web Security Testing
Guide (WSTG) methodology, tracks checklist coverage, and turns tester-supplied evidence into a
findings report with WSTG IDs. **This skill does not perform any testing itself** — no requests
to any target, no scanning, no exploitation. The human tester runs their own tools (Burp Suite,
ZAP, curl, browser devtools, etc.) within their existing authorized engagement; this skill's job
is the checklist, the diagnostic questions per test, interpreting evidence the tester pastes in,
and the report.

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

Record this once at the start of the session/engagement; don't re-ask on every message within the
same conversation.

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
2. Ask the tester what they found — or, if they paste evidence (HTTP requests/responses, screenshots,
   config dumps, headers), assess it against that specific test's criteria.
3. Record the result: **Pass**, **Fail (finding)**, **Not Applicable** (with a one-line reason —
   e.g. "no file upload feature in this app" for WSTG-BUSL-08/09), or **Not Tested** (out of time/
   scope for this pass — note it as a coverage gap, not a pass).
4. If it's a finding, capture: severity, evidence, affected location (URL/param/endpoint), and a
   remediation recommendation.

Point the tester to the full WSTG page for methodology detail on any specific test if they want it:
`https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/<NN-Category>/<NN-Test_Name>`

## Step 4 — Report

When the tester wants a deliverable, produce a Markdown report with:

- **Engagement summary**: target(s), dates, tester, methodology (OWASP WSTG, note this is not an
  official OWASP-endorsed tool — see README), categories in scope.
- **Coverage table**: per category, count of Pass / Fail / N/A / Not Tested, so gaps are visible
  at a glance rather than buried.
- **Findings register**, sorted by severity (Critical → Info), each entry: WSTG ID, title, severity,
  affected location, description, evidence, recommendation.
- **Appendix**: full per-test results including Pass and N/A entries with their reasons, for audit
  trail / due-diligence purposes.

## Guardrails

- Never send a request to, scan, or attempt to exploit anything — if the tester asks you to
  "just try it," redirect them to run it with their own tooling and paste back the result.
- Business logic (category 10) and parts of Authorization/Session testing require understanding
  *this specific app's* intended behavior — don't mechanically mark these "Pass" without the
  tester describing the actual workflow; flag them as needing more context if unclear.
- A clean run through this checklist is not a certification and doesn't guarantee the absence of
  vulnerabilities — WSTG itself isn't exhaustive, and this skill's summaries are shorter than the
  full WSTG guidance. Say so in the report, don't imply completeness the testing didn't achieve.
- If the tester hasn't confirmed authorization (Step 1), do not proceed past scope intake.
