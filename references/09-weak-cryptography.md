# WSTG-CRYP — Testing for Weak Cryptography

| ID | Title | What it verifies |
|---|---|---|
| WSTG-CRYP-01 | Testing for Weak Transport Layer Security | TLS config uses current protocol versions/cipher suites only; no SSLv3/TLS 1.0/1.1, weak ciphers, or cert issues |
| WSTG-CRYP-02 | Testing for Padding Oracle | Padding-oracle attacks against CBC-mode encryption aren't possible (no distinguishable padding-error responses) |
| WSTG-CRYP-03 | Testing for Sensitive Information Sent via Unencrypted Channels | No sensitive data (PII, tokens, credentials) is ever transmitted over an unencrypted channel |
| WSTG-CRYP-04 | Testing for Weak Cryptographic Primitives | No deprecated/broken algorithms in use (MD5/SHA1 for security purposes, weak key lengths, ECB mode, hardcoded keys/IVs) |
