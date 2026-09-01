# WSTG-BUSL — Business Logic Testing

Business logic testing is the category checklists help least with — it requires understanding
*this specific application's* intended workflow and thinking like an attacker about how to abuse
it. Treat these as prompts for that thinking, not mechanical checks.

| ID | Title | What it verifies |
|---|---|---|
| WSTG-BUSL-00 | Introduction to Business Logic (background, not a test) | — |
| WSTG-BUSL-01 | Test Business Logic Data Validation | Business rules (not just type/format validation) are enforced server-side (e.g. quantities, dates, state transitions that make sense) |
| WSTG-BUSL-02 | Test Ability to Forge Requests | A legitimate multi-step process can't be replayed/reordered/skipped by forging requests directly |
| WSTG-BUSL-03 | Test Integrity Checks | Data integrity (e.g. price, hidden totals) can't be tampered with client-side and trusted server-side |
| WSTG-BUSL-04 | Test for Process Timing | Timing-dependent logic (race conditions, TOCTOU) can't be abused — e.g. double-spend via concurrent requests |
| WSTG-BUSL-05 | Test Number of Times a Function Can Be Used Limits | Functions meant to be used a limited number of times (coupon redemption, vote once) actually enforce that limit |
| WSTG-BUSL-06 | Testing for the Circumvention of Work Flows | Required workflow steps can't be skipped by directly calling a later step's endpoint |
| WSTG-BUSL-07 | Test Defenses Against Application Misuse | Anti-automation/anti-abuse controls (rate limiting, CAPTCHA where appropriate) exist for business-critical actions |
| WSTG-BUSL-08 | Test Upload of Unexpected File Types | File upload rejects types outside the intended allow-list, validated by content not just extension/MIME claim |
| WSTG-BUSL-09 | Test Upload of Malicious Files | Uploaded files (even allowed types) are scanned/sandboxed and can't achieve execution or serve as an attack vector |
| WSTG-BUSL-10 | Test Payment Functionality | Payment flows can't be manipulated for price tampering, currency confusion, negative amounts, or double-processing |
