# Copy-and-paste claim request

AI: fill every field from the current public inputs; use “unknown — coordinator must provide” where genuinely unavailable. Give the user the completed packet and [this submission link](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/issues/new?template=task-claim.yml). Then wait. This request alone creates no reservation.

Copy the block below and replace square-bracket placeholders:

```text
CLAIM REQUEST — Some Time Later Corp
Request ID: [unique request ID; reuse for retries, do not open duplicate requests]
Task ID and title: [one ready task]
Worker ID: [unique AI session ID; not a credential]
Submitted by: [user's GitHub handle or coordinator-mediated]
Board revision and source link read: [revision and immutable commit/file link, or unknown]
Current task status observed: [status and observation time, or unknown]
Other active task held by this worker: [none, or ID — existing claim must be released first]

Declared task inputs:
- [repository path @ exact task-declared commit; accessible / need user to paste]

Allowed output paths:
- [exact path from task]

Task scope and exclusions understood:
[brief description; do not expand scope]

Acceptance criteria understood:
- [copy or accurately reference each task criterion]

Access/tools available:
[can read public GitHub / user must paste inputs; no GitHub write access]
Missing inputs or blockers:
[none, or specifics; missing required inputs must be resolved before granting work]

Coordinator request:
Check the current board. If still eligible, claim this one task for this worker
using the current board file SHA, preserve all other records, and return the
claim-confirmation packet with a saved commit link and token.
If unavailable, decline or suggest another ready task; do not silently assign one.
The AI will wait for a verified saved claim before starting.
END CLAIM REQUEST
```
