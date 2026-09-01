# WSTG-INFO — Information Gathering

| ID | Title | What it verifies |
|---|---|---|
| WSTG-INFO-01 | Conduct Search Engine Discovery Reconnaissance for Information Leakage | Google/Bing dorking, cached pages, and search-indexed content don't expose internal paths, credentials, or sensitive docs |
| WSTG-INFO-02 | Fingerprint Web Server | Server banner, headers, and behavioral quirks reveal server software/version (informs known-CVE exposure, not a reason to skip patching regardless) |
| WSTG-INFO-03 | Review Webserver Metafiles for Information Leakage | `robots.txt`, `sitemap.xml`, `security.txt`, `humans.txt` don't disclose hidden admin paths or internal structure |
| WSTG-INFO-04 | Attack Surface Identification (formerly "Enumerate Applications on Webserver") | All hostnames/vhosts/ports/apps behind the target IP(s) are enumerated so nothing in scope is missed |
| WSTG-INFO-05 | Review Web Page Content for Information Leakage | HTML comments, JS source, metadata, and client-side code don't leak internal hostnames, credentials, or logic |
| WSTG-INFO-06 | Identify Application Entry Points | Every place the app accepts input (params, headers, cookies, file uploads, hidden fields) is mapped before testing input handling |
| WSTG-INFO-07 | Map Execution Paths Through Application | Application flow/state machine is understood (multi-step processes, conditional branches) to plan business-logic and auth testing |
| WSTG-INFO-08 | Fingerprint Web Application Framework | Framework identification (headers, error pages, file structure) to target framework-specific known weaknesses |
| WSTG-INFO-09 | Fingerprint Web Application | Specific app/CMS/version identification (plugin lists, changelogs, version strings) |
| WSTG-INFO-10 | Map Application Architecture | Overall architecture (CDN, WAF, load balancer, backend services) is understood to plan realistic attack paths |
