# WSTG-SESS — Session Management Testing

| ID | Title | What it verifies |
|---|---|---|
| WSTG-SESS-01 | Testing for Session Management Schema | Session token generation is unpredictable (sufficient entropy, no exploitable pattern) |
| WSTG-SESS-02 | Testing for Cookies Attributes | Session cookies set `Secure`, `HttpOnly`, and an appropriate `SameSite` value |
| WSTG-SESS-03 | Testing for Session Fixation | The app issues a fresh session token on login rather than accepting a pre-set/attacker-supplied one |
| WSTG-SESS-04 | Testing for Exposed Session Variables | Session tokens/identifiers aren't leaked via URL, Referer header, logs, or browser history |
| WSTG-SESS-05 | Testing for Cross Site Request Forgery | State-changing requests require a CSRF token (or equivalent) validated server-side, not just present in the request |
| WSTG-SESS-06 | Testing for Logout Functionality | Logout actually invalidates the session server-side (not just client-side cookie deletion) and covers all active tokens |
| WSTG-SESS-07 | Testing Session Timeout | Idle and absolute session timeouts are enforced server-side within a reasonable window |
| WSTG-SESS-08 | Testing for Session Puzzling | Session variables set in one flow can't be misused/reinterpreted in an unrelated flow to bypass logic |
| WSTG-SESS-09 | Testing for Session Hijacking | Session tokens can't be predicted, stolen via transport weaknesses, or reused across contexts (e.g. IP/device binding where appropriate) |
| WSTG-SESS-10 | Testing JSON Web Tokens | JWT signature is verified server-side, `alg: none`/algorithm-confusion isn't accepted, and claims (exp, aud, iss) are validated |
| WSTG-SESS-11 | Testing for Concurrent Sessions | Concurrent session policy (allow/deny/limit) is enforced as intended and old sessions are properly invalidated when required |
