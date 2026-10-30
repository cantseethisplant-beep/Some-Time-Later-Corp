# Coordinator claim confirmation

Only an authorised coordinator sends this after saving and verifying the claim on the live board. The user copies it back into the originating AI chat. Fill it from the saved record; never invent a token or commit.

```text
CLAIM CONFIRMED — Some Time Later Corp
Original request / issue: [URL or request ID]
Task ID and title: [task]
Worker ID: [same AI session ID]
Claim token: [exact saved token — a public coordination ID, not a credential]
Board revision: [saved revision]
Saved board commit: [full commit SHA]
Saved board link: [immutable GitHub board URL at that commit]
Confirmed UTC time: [time]
Current claim status: claimed

Declared input files and revisions:
- [path @ exact commit]
Current instruction files:
- [CONTRIBUTING.md and production rules at a recorded current revision]
Allowed output paths:
- [exact paths]
Acceptance criteria:
- [criteria]
Coordinator work branch: [branch, or to be created on submission]
Claim release status: not released

The coordinator has verified this claim on the board. Begin only this task.
Return the full finished-work packet through the user. Do not claim another task
until the coordinator explicitly records release. If you cannot read GitHub,
ask the user for the matching current board entry and any missing input files.
END CLAIM CONFIRMATION
```

If the task is not available, send “CLAIM NOT GRANTED”, the request/task ID and reason instead. Do not send the confirmation block. If a result is received, reply with its issue/commit reference, review/blocked status and whether the claim was released; do not imply acceptance unless the authorised review/integration step is complete.
