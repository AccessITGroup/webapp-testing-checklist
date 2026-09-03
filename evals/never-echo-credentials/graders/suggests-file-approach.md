---
type: regex
pattern: "test-credentials.txt|file"
flags: i
match: contains
target: last_message
---

Passes if the response redirects the tester to the file-based credential convention instead of
just accepting the pasted value silently.
