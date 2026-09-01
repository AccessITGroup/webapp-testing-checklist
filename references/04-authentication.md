# WSTG-ATHN — Authentication Testing

| ID | Title | What it verifies |
|---|---|---|
| WSTG-ATHN-01 | Testing for Credentials Transported over an Encrypted Channel | Credentials are never sent over plaintext HTTP at any point (login, password reset, API auth) |
| WSTG-ATHN-02 | Testing for Default Credentials | No default/vendor/sample accounts or passwords remain active |
| WSTG-ATHN-03 | Testing for Weak Lock Out Mechanism | Account lockout/rate-limiting on auth attempts exists, has a sane threshold, and can't itself be abused (e.g. to lock out victims) |
| WSTG-ATHN-04 | Testing for Bypassing Authentication Schema | Auth can't be bypassed via forced browsing, parameter tampering, SQL injection, or alternate request paths |
| WSTG-ATHN-05 | Testing for Vulnerable Remember Password | "Remember me" tokens are unpredictable, expire appropriately, and don't store the password itself insecurely |
| WSTG-ATHN-06 | Testing for Browser Cache Weaknesses | Sensitive pages/credentials aren't cacheable by the browser (proper `Cache-Control`/`Pragma` headers) |
| WSTG-ATHN-07 | Testing for Weak Authentication Methods | Auth method itself (basic auth, custom scheme, etc.) is appropriate and not trivially bypassable |
| WSTG-ATHN-08 | Testing for Weak Security Question Answer | Security questions (if used) aren't easily guessable/researchable and aren't the sole factor protecting an account |
| WSTG-ATHN-09 | Testing for Weak Password Change or Reset Functionalities | Password change/reset flows require proper re-authentication, use non-guessable/expiring tokens, and don't leak account existence |
| WSTG-ATHN-10 | Testing for Weaker Authentication in Alternative Channel | Alternate channels (mobile API, legacy endpoint, IVR) don't allow weaker auth than the primary channel |
| WSTG-ATHN-11 | Testing Multi-Factor Authentication | MFA (if present) can't be bypassed via response manipulation, replay, missing server-side enforcement, or backup-code weaknesses |
