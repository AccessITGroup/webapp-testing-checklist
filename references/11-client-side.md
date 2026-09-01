# WSTG-CLNT — Client-side Testing

| ID | Title | What it verifies |
|---|---|---|
| WSTG-CLNT-01 | Testing for DOM-based Cross Site Scripting | Client-side JS doesn't write attacker-influenced data into a dangerous DOM sink (`innerHTML`, `eval`, etc.) |
| WSTG-CLNT-01.1 | Testing for Self DOM Based Cross Site Scripting | Victim can't be tricked into pasting attacker-supplied input into the browser console/address bar to self-XSS |
| WSTG-CLNT-02 | Testing for JavaScript Execution | Unintended JS execution paths (e.g. via URL schemes, postMessage) aren't reachable |
| WSTG-CLNT-03 | Testing for HTML Injection | User input rendered client-side can't inject arbitrary HTML structure even without script execution |
| WSTG-CLNT-04 | Testing for Client-side URL Redirect | Client-side redirect logic validates destination and can't be abused for open-redirect phishing |
| WSTG-CLNT-05 | Testing for CSS Injection | Attacker-controlled CSS can't exfiltrate data (attribute selectors) or perform UI redress |
| WSTG-CLNT-06 | Testing for Client-side Resource Manipulation | Client-side logic that constructs resource URLs/paths can't be manipulated to load unintended resources |
| WSTG-CLNT-07 | Testing Cross Origin Resource Sharing | CORS policy doesn't reflect arbitrary `Origin` or use wildcard `*` alongside credentialed requests |
| WSTG-CLNT-08 | Testing for Cross Site Flashing | Legacy Flash content (if any remains) doesn't expose cross-domain vulnerabilities |
| WSTG-CLNT-09 | Testing for Clickjacking | `X-Frame-Options`/`frame-ancestors` (CSP) prevents the page from being framed for UI-redress attacks |
| WSTG-CLNT-10 | Testing WebSockets | WebSocket handshake validates origin, uses `wss://`, and messages are validated same as any other input |
| WSTG-CLNT-11 | Testing Web Messaging | `postMessage` handlers validate the origin of received messages and don't trust arbitrary senders |
| WSTG-CLNT-12 | Testing Browser Storage | LocalStorage/SessionStorage/IndexedDB don't hold sensitive data unnecessarily exposed to XSS |
| WSTG-CLNT-13 | Testing for Cross Site Script Inclusion | Sensitive data isn't exposed via JSONP/script-tag inclusion that a third-party origin could read |
| WSTG-CLNT-14 | Testing for Reverse Tabnabbing | Links opening in a new tab (`target="_blank"`) use `rel="noopener"` so the opened page can't manipulate the opener |
| WSTG-CLNT-15 | Testing for Client-Side Template Injection | User input reaching a client-side template engine (Angular, Vue, etc.) can't execute template expressions |
