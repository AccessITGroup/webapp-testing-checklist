# WSTG-CONF — Configuration and Deployment Management Testing

| ID | Title | What it verifies |
|---|---|---|
| WSTG-CONF-01 | Test Network Infrastructure Configuration | Network-level config (open ports, unnecessary services, TLS termination points) doesn't expand attack surface beyond what's needed |
| WSTG-CONF-02 | Test Application Platform Configuration | App server/platform hardening — default configs, sample apps, verbose errors, directory listing all disabled |
| WSTG-CONF-03 | Test File Extensions Handling for Sensitive Information | Backup/config/source extensions (`.bak`, `.old`, `.config`, `.git`) aren't served or don't leak source/secrets |
| WSTG-CONF-04 | Review Old Backup and Unreferenced Files for Sensitive Information | Forgotten backup files, old versions, or unlinked files aren't reachable and don't leak sensitive data |
| WSTG-CONF-05 | Enumerate Infrastructure and Application Admin Interfaces | Admin/management interfaces aren't discoverable/reachable without proper access controls |
| WSTG-CONF-06 | Test HTTP Methods | Only required HTTP methods are enabled (no TRACE/PUT/DELETE where unneeded); method-based access-control bypass isn't possible |
| WSTG-CONF-07 | Test HTTP Strict Transport Security | HSTS header present with adequate `max-age` and (where appropriate) `includeSubDomains`/`preload` |
| WSTG-CONF-08 | Test RIA Cross Domain Policy | `crossdomain.xml`/`clientaccesspolicy.xml` (Flash/Silverlight legacy) don't grant overly permissive cross-domain access |
| WSTG-CONF-09 | Test File Permission | Files/directories on the server don't have overly permissive read/write/execute permissions |
| WSTG-CONF-10 | Test for Subdomain Takeover | DNS records (CNAMEs to decommissioned cloud services, etc.) don't point at unclaimed resources an attacker could claim |
| WSTG-CONF-11 | Test Cloud Storage | Cloud storage buckets (S3, Blob, GCS) tied to the app aren't publicly readable/writable beyond intended access |
| WSTG-CONF-12 | Test for Content Security Policy | CSP header exists, is restrictive (no wildcard/`unsafe-inline`/`unsafe-eval` without justification), and actually mitigates XSS impact |
| WSTG-CONF-13 | Test for Path Confusion | URL parsing inconsistencies (path normalization, trailing slashes/dots) don't let requests bypass routing-based access controls |
| WSTG-CONF-14 | Test Other HTTP Security Header Misconfigurations | Remaining security headers (`X-Content-Type-Options`, `X-Frame-Options`, `Referrer-Policy`, `Permissions-Policy`, etc.) are present and correctly configured |
