# webapp-testing-checklist

A Claude Code skill that structures an **authorized** web application penetration test around the
**OWASP Web Security Testing Guide (WSTG)** methodology — tracks checklist coverage across all 12
WSTG categories and turns tester-supplied evidence into a findings report with WSTG-numbered IDs.

> **This is a checklist and report-generation aid for a human-led engagement, in backseat mode.**
> Normal benign traffic (viewing pages, following links, submitting ordinary form input) is fine;
> it never sends a payload, injection string, exploit attempt, or runs a scanner. The tester runs
> actual security testing with their own tooling (Burp Suite, ZAP, curl, browser devtools, etc.);
> this skill organizes coverage, asks the right diagnostic question per WSTG test, interprets
> evidence pasted in (including raw Burp/ZAP captures), and writes the report.

## Why WSTG, and why this exists

WSTG is OWASP's current, actively maintained web application testing methodology (the earlier
OWASP Testing Guide, OTG v3/v4, was retired in WSTG's favor). This skill's checklist reflects the
live WSTG structure — including recent additions like OAuth, JWT, SSRF, mass assignment, prototype
pollution, and insecure deserialization — not a frozen PDF snapshot. See
`references/00-overview.md` for exactly what was cross-checked and when.

Author's background: Kevin Horvath is a contributing author to the earlier OWASP Testing Guide
(v3 and v4), the predecessor methodology WSTG evolved from — noted here as background, not as a
claim of authorship on WSTG itself.

## Authorization requirement

The skill's first step is an **authorization gate**: it will not walk the checklist until the
tester confirms written authorization for the specific target, the named engagement/scope, the
testing window/rules of engagement, and the test credentials/accounts (count and role) being used.
This isn't optional — see `SKILL.md` Step 1.

**Credentials never go in the chat.** Test accounts are supplied via a plain text file
(`test-credentials.txt` by convention) in the working directory, one account per line
(`label | role | username | password`) — the skill reads it once, then refers to accounts by
label/role only for the rest of the session and in the report. `.gitignore` that file and delete
it after the engagement.

**Account creation is a separate, stricter gate.** Even though normal form submission is otherwise
fine, the skill will not create an account in the target application unless the tester has
confirmed the SOW explicitly authorizes test-account creation, and gives real-time go-ahead at the
point it's needed. Default is always no — existing test credentials are the expected path.

**This gate is conversational, not technical.** The authorization check is a prompt the assistant
follows, not a mechanism that can independently verify anything — it relies on the tester
answering honestly. Nothing here stops a user from misrepresenting their authorization, and
nothing stops someone from forking this repo and stripping the guardrails out entirely. Treat this
skill as a workflow aid for testers who are already authorized, not as a safeguard that makes
unauthorized use impossible.

## What it covers

All 12 WSTG categories — Information Gathering, Configuration & Deployment, Identity Management,
Authentication, Authorization, Session Management, Input Validation, Error Handling, Weak
Cryptography, Business Logic, Client-side, and API Testing. Full per-category test lists are in
`references/`.

## Usage

Install as a Claude Code skill (via the `AITG-hub` marketplace, or directly):

```
/plugin marketplace add AccessITGroup/claude-plugins
/plugin install webapp-testing-checklist@AITG-hub
```

Then, within an authorized engagement, trigger it with something like *"walk this app through the
WSTG checklist"* or *"help me track coverage and write findings against WSTG for this pentest."*

For each test that needs hands-on testing, you can either paste evidence (a Burp/ZAP
request/response, a screenshot) for the skill to assess, or just give the verdict directly
(Pass/Fail/N/A) — either is fine, the report is explicit about which was used. When you want the
deliverable, you'll be asked which format(s): Markdown, Word (.docx), and/or PDF.

The final report notes that pairing this dynamic/checklist pass with a **Claude-based source code
security review** is recommended when code-level review is in the SOW and source access has been
provided by the application owner — this checklist covers dynamic/black-box testing only.

## Limitations

- A clean run through this checklist is not a certification and does not guarantee the absence of
  vulnerabilities. WSTG itself isn't exhaustive, and the `references/` summaries are intentionally
  shorter than the full WSTG guidance pages (linked per-test for full methodology).
- Business logic testing (category 10) and parts of Authorization/Session testing require genuine
  understanding of the specific application's intended behavior — this skill prompts for that
  context, it doesn't substitute for it.
- Not an official OWASP project; not endorsed by the OWASP Foundation.
- **Word (`.docx`) output reliability varies by local toolchain.** Text and tables convert fine,
  but embedding local screenshot images into `.docx` has proven unreliable with some common
  local HTML→DOCX conversion tools (e.g. macOS `textutil` dropped images entirely in testing,
  while the same source converted to PDF embedded them correctly). If a report includes
  screenshots, **open the generated `.docx` and verify the images actually appear** before
  delivering it — don't assume success from the file being created. `pandoc` or `python-docx`,
  where available, have generally proven more reliable for this than OS-builtin converters.

## Changelog

See `CHANGELOG.md` for version history.

## License

- Skill instructions and original text (`SKILL.md`, this README): **MIT** — see `LICENSE`.
- Checklist content derived from OWASP WSTG (`references/`): **CC BY-SA 4.0** — see
  `LICENSE-CONTENT.md`.
