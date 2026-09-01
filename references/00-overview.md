# WSTG Checklist — Overview

Source of truth for this skill's checklist content: **OWASP Web Security Testing Guide (WSTG)**,
current stable line, cross-checked against `OWASP/wstg` on GitHub on 2026-09-01 (latest tagged
PDF release is v4.2; the `master` branch has continued to add tests since that tag — e.g. OAuth,
JWT, SSRF, mass assignment, prototype pollution, insecure deserialization, and expanded API
testing — so this checklist reflects the living document, not just the v4.2 PDF snapshot).

**Attribution & license**: the test IDs, titles, and category structure below are derived from the
OWASP WSTG (https://github.com/OWASP/wstg), licensed **CC BY-SA 4.0** by the OWASP Foundation. This
derivative checklist is shared under the same license — see `LICENSE-CONTENT`. This project is
**not an official OWASP project and is not endorsed by the OWASP Foundation.**

## Categories (load the matching file in this directory as you reach it)

| # | Category | ID prefix | File |
|---|---|---|---|
| 1 | Information Gathering | WSTG-INFO | `01-information-gathering.md` |
| 2 | Configuration and Deployment Management Testing | WSTG-CONF | `02-configuration-and-deployment.md` |
| 3 | Identity Management Testing | WSTG-IDNT | `03-identity-management.md` |
| 4 | Authentication Testing | WSTG-ATHN | `04-authentication.md` |
| 5 | Authorization Testing | WSTG-AUTHZ | `05-authorization.md` |
| 6 | Session Management Testing | WSTG-SESS | `06-session-management.md` |
| 7 | Input Validation Testing | WSTG-INPV | `07-input-validation.md` |
| 8 | Testing for Error Handling | WSTG-ERRH | `08-error-handling.md` |
| 9 | Testing for Weak Cryptography | WSTG-CRYP | `09-weak-cryptography.md` |
| 10 | Business Logic Testing | WSTG-BUSL | `10-business-logic.md` |
| 11 | Client-side Testing | WSTG-CLNT | `11-client-side.md` |
| 12 | API Testing | WSTG-APIT | `12-api-testing.md` |

## How each category file is structured

Each row is one WSTG test: `ID | Title | What it verifies`. The third column is a one-line
prompt for what evidence to ask the tester for or what to look for in evidence they provide —
it is **not** a reproduction of the full WSTG guidance page (which is far more detailed; link to
the live page — `https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/<NN-Category>/<NN-Test_Name>` — when the tester wants the full methodology for a specific test).

Not every test applies to every engagement (e.g. skip Client-side tests for an API-only target,
skip most of API Testing for a server-rendered app with no API surface). Scope intake (see
`SKILL.md`) determines which category files actually get walked.
