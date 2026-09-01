# WSTG-AUTHZ — Authorization Testing

| ID | Title | What it verifies |
|---|---|---|
| WSTG-AUTHZ-01 | Testing Directory Traversal File Include | Path traversal (`../`), null-byte, or encoding tricks can't reach files/includes outside the intended directory |
| WSTG-AUTHZ-02 | Testing for Bypassing Authorization Schema | Authorization can't be bypassed via forced browsing, HTTP method switching, or parameter manipulation |
| WSTG-AUTHZ-03 | Testing for Privilege Escalation | A lower-privileged user can't gain higher privileges (vertical escalation) via parameter tampering, hidden fields, or role manipulation |
| WSTG-AUTHZ-04 | Testing for Insecure Direct Object References | Object IDs (order #, file ID, user ID in URL/param) are authorization-checked server-side, not just obscured (horizontal escalation / IDOR) |
| WSTG-AUTHZ-05 | Testing for OAuth Weaknesses | If OAuth is used, redirect_uri validation, state parameter (CSRF), and scope handling are correctly implemented |
| WSTG-AUTHZ-05.1 | Testing for OAuth Authorization Server Weaknesses | The authorization server itself correctly validates client registration, redirect URIs, and grant types |
| WSTG-AUTHZ-05.2 | Testing for OAuth Client Weaknesses | The OAuth client (relying party) correctly validates tokens, state, and doesn't trust unverified claims |
