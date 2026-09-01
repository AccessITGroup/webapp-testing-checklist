# WSTG-IDNT — Identity Management Testing

| ID | Title | What it verifies |
|---|---|---|
| WSTG-IDNT-01 | Test Role Definitions | Roles are distinct, least-privilege, and don't overlap in ways that create unintended access |
| WSTG-IDNT-02 | Test User Registration Process | Registration can't be abused to claim unverified identities, impersonate domains, or bypass approval steps |
| WSTG-IDNT-03 | Test Account Provisioning Process | Accounts can only be created/modified/deprovisioned by properly authorized parties, with no gaps in the process |
| WSTG-IDNT-04 | Testing for Account Enumeration and Guessable User Account | Login, registration, and password-reset flows don't reveal whether a given username/email exists |
| WSTG-IDNT-05 | Testing for Weak or Unenforced Username Policy | Username policy doesn't leak PII (e.g. sequential IDs, predictable formats) or allow trivially guessable identifiers |
