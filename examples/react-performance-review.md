### Input

Review this file using your performance rules.

### Output (excerpt)

Severity: High

Problem:
Sequential data fetching inside a server component.

Why it matters:
Each await introduces a full network roundtrip.

Fix:
Parallelize requests using Promise.all.