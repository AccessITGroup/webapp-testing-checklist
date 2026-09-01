# WSTG-INPV — Input Validation Testing

| ID | Title | What it verifies |
|---|---|---|
| WSTG-INPV-01 | Testing for Reflected Cross Site Scripting | User input reflected in the response is properly encoded/sanitized for the output context |
| WSTG-INPV-02 | Testing for Stored Cross Site Scripting | Input persisted and later rendered to other users is properly encoded/sanitized for the output context |
| WSTG-INPV-03 | Testing for HTTP Verb Tampering | Access control and input validation apply consistently regardless of HTTP method used |
| WSTG-INPV-04 | Testing for HTTP Parameter Pollution | Duplicate parameter names are handled consistently and can't be used to bypass validation/WAF rules |
| WSTG-INPV-05 | Testing for SQL Injection | Database queries are parameterized; no injectable input reaches SQL construction |
| WSTG-INPV-05.1 | Testing for Oracle | Oracle-specific injection vectors and error-based/blind techniques don't succeed |
| WSTG-INPV-05.2 | Testing for MySQL | MySQL-specific injection vectors don't succeed |
| WSTG-INPV-05.3 | Testing for SQL Server | SQL Server-specific injection vectors (incl. `xp_cmdshell` exposure) don't succeed |
| WSTG-INPV-05.4 | Testing PostgreSQL | PostgreSQL-specific injection vectors don't succeed |
| WSTG-INPV-05.5 | Testing for MS Access | MS Access-specific injection vectors don't succeed |
| WSTG-INPV-05.6 | Testing for NoSQL Injection | NoSQL query operators/objects can't be injected via input (e.g. Mongo `$where`/operator injection) |
| WSTG-INPV-05.7 | Testing for ORM Injection | ORM query-builder misuse doesn't allow injection despite the abstraction layer |
| WSTG-INPV-05.8 | Testing for Client-side | Client-side data stores (IndexedDB, WebSQL) queried from JS aren't injectable |
| WSTG-INPV-06 | Testing for LDAP Injection | LDAP filter syntax can't be injected via input to alter directory queries |
| WSTG-INPV-07 | Testing for XML Injection | XML input can't inject unintended elements/attributes or abuse parser features (see also XXE under this category's parser-specific testing) |
| WSTG-INPV-08 | Testing for SSI Injection | Server-Side Includes directives can't be injected via user input |
| WSTG-INPV-09 | Testing for XPath Injection | XPath queries built from user input can't be manipulated to bypass logic or extract data |
| WSTG-INPV-10 | Testing for IMAP/SMTP Injection | Mail-header/command injection isn't possible via input passed to mail functions |
| WSTG-INPV-11 | Testing for Code Injection | User input can't reach a code-evaluation sink (`eval`, dynamic includes, deserialization-to-code) |
| WSTG-INPV-11.1 | Testing for File Inclusion | Local/remote file inclusion (LFI/RFI) isn't possible via user-controlled file paths |
| WSTG-INPV-12 | Testing for Command Injection | User input can't reach an OS command execution sink |
| WSTG-INPV-13 | Testing for Buffer Overflow | Fixed-size buffers (native code paths, older stacks) don't overflow on oversized/malformed input |
| WSTG-INPV-13 (format string) | Testing for Format String Injection | User input isn't passed directly as a format-string argument (`printf`-family) |
| WSTG-INPV-14 | Testing for Incubated Vulnerability | Multi-step attack chains (e.g. upload a file now, trigger it later) aren't possible across separate requests/sessions |
| WSTG-INPV-15 | Testing for HTTP Response Splitting | User input reflected into headers can't inject CRLF sequences to split the response |
| WSTG-INPV-16 | Testing for HTTP Request Smuggling | Front-end/back-end request parsing (Content-Length vs Transfer-Encoding) can't be desynced to smuggle requests |
| WSTG-INPV-17 | Testing for Host Header Injection | `Host` header isn't trusted for routing, password-reset links, or cache keys without validation |
| WSTG-INPV-18 | Testing for Server-side Template Injection | User input reaching a template engine can't execute template syntax/code |
| WSTG-INPV-19 | Testing for Server-Side Request Forgery | User-supplied URLs/hosts can't make the server issue requests to internal/unintended destinations |
| WSTG-INPV-20 | Testing for Mass Assignment | API/form binding can't be abused to set fields the client shouldn't control (e.g. `isAdmin`) |
| WSTG-INPV-21 | Testing for CSV Injection | Data exported to CSV/Excel doesn't allow formula injection (`=`, `+`, `-`, `@` prefixes) that executes on open |
| WSTG-INPV-22 | Testing for Prototype Pollution | JS object-merge/assignment logic can't be abused to pollute `Object.prototype` |
| WSTG-INPV-23 | Testing for Insecure Deserialization | Deserialization of untrusted data can't lead to object injection, code execution, or logic bypass |
