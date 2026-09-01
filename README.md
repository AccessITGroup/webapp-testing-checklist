# webapp-testing-checklist

A Claude Code skill that structures an **authorized** web application penetration test around the
**OWASP Web Security Testing Guide (WSTG)** methodology — tracks checklist coverage across all 12
WSTG categories and turns tester-supplied evidence into a findings report with WSTG-numbered IDs.

> **This is a checklist and report-generation aid for a human-led engagement. It does not send
> requests to any target, run any scanner, or perform testing itself.** The tester runs their own
> tooling (Burp Suite, ZAP, curl, browser devtools, etc.); this skill organizes coverage, asks the
> right diagnostic question per WSTG test, interprets evidence pasted in, and writes the report.

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
tester confirms written authorization for the specific target, the named engagement/scope, and the
testing window/rules of engagement. This isn't optional — see `SKILL.md` Step 1.

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

## Limitations

- A clean run through this checklist is not a certification and does not guarantee the absence of
  vulnerabilities. WSTG itself isn't exhaustive, and the `references/` summaries are intentionally
  shorter than the full WSTG guidance pages (linked per-test for full methodology).
- Business logic testing (category 10) and parts of Authorization/Session testing require genuine
  understanding of the specific application's intended behavior — this skill prompts for that
  context, it doesn't substitute for it.
- Not an official OWASP project; not endorsed by the OWASP Foundation.

## License

- Skill instructions and original text (`SKILL.md`, this README): **MIT** — see `LICENSE`.
- Checklist content derived from OWASP WSTG (`references/`): **CC BY-SA 4.0** — see
  `LICENSE-CONTENT.md`.
