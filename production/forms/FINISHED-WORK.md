# Copy-and-paste finished work

AI: give the user this completed packet and [the finished-work issue link](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/issues/new?template=finished-work.yml). Include complete file contents, not just a narrative. Creating the issue submits a draft for review; it does not accept it or release ownership.

Copy the outer block, replace placeholders, and repeat the FILE section for every output. Use a longer outer code fence if the file contents contain triple backticks.

````text
FINISHED WORK — Some Time Later Corp
Submission ID: [unique submission ID; reuse for corrections]
Task ID and title: [task]
Worker ID: [same AI session ID]
Claim token: [saved token]
Original claim issue / request: [URL or ID]
Claim-confirmation board revision and commit: [revision and SHA/link]
Current claim checked: [time and board link, or not independently checked]
Submission state: complete for review / partial and blocked
Part: [1 of N]
All expected parts: [N]
Output manifest:
- [exact repository path; parts containing this file; complete or partial]

Summary of changes:
[brief summary]

Input provenance:
- [path/source URL @ exact revision/version; how it was used]

Acceptance criteria and checks:
- [criterion]: [check actually performed, observed result, evidence location]
Checks not performed:
[explicitly state any; do not invent test execution]
Unresolved decisions / limitations:
[none or details]
Blockers or scope differences:
[none or details; do not present partial work as completed]

BEGIN FILE: [exact allowed repository path]
[complete proposed UTF-8 file contents]
END FILE: [same path]
[repeat for every output; for chunked files identify file part numbers]

Coordinator request:
Recheck the claim and input/output scope. Verify every part is present before
integration. Put the proposed files on a work branch, record this submission and
commit/PR in the board, and move the task to review if eligible.
Please explicitly record whether my claim is released; submission is not acceptance.

END SUBMISSION: [task ID] | [submission ID] | [N] PARTS
````

For a multipart packet, put the final END SUBMISSION marker only on the last part, and label every comment with the same task, worker, claim token, submission ID and part number. List corrections as a new explicit packet revision that supersedes named parts. Do not mix revisions silently. The coordinator waits for a complete consistent set.

If files are attached instead of pasted, replace the inline FILE sections with an attachment link and a path-to-file manifest. The complete files must remain retrievable; do not rely on a private chat link. Never include secrets or private operational records.
