# Contribute through your talking AI

You can contribute even when your AI cannot write to GitHub. You act as the messenger: paste a claim request into GitHub, bring the confirmed claim back to your AI, then paste its finished work back into GitHub.

The project owner or an authorised coordinator handles board updates and integration. You do not need repository write access to open an issue. You do need a GitHub account to post an issue or comment. If you cannot use GitHub, paste the same packets into a chat with the project owner/coordinator who can submit them for you.

## 1. Give your AI the project

Copy this into your AI:

> Help me contribute one small task to Some Time Later Corp: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp . Read CONTRIBUTING.md, AI-CONTEXT.md, docs/PRODUCTION.md and production/board.json. You cannot write to GitHub, so use the user-mediated route. Choose one ready task, prepare the claim-request packet, and tell me exactly where to paste it. Do not start the task until I bring back a verified claim confirmation. Do not claim that a chat message or issue reserves the task.

If the AI cannot read the public repository either, copy the current instructions, relevant board entry and pinned input files into the chat. It should tell you which files/revisions it still needs. It must not invent unseen inputs or assume old screenshots show current availability.

## 2. Request one task

Ask your AI to fill in [the claim-request packet](production/forms/CLAIM-REQUEST.md). Give the AI session a unique worker ID; use the same ID throughout this task. It is a coordination identifier, not a password. One AI session may own only one active task.

Open [Request a task claim](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/issues/new?template=task-claim.yml) and paste the complete packet into the form. Replace the issue title placeholders with the task and worker IDs. Before submitting, check that the packet contains only information you intend to make public.

**Opening the issue does not reserve the task.** Another worker may claim it first. Wait for a coordinator's confirmed board update. If unavailable, request another ready task rather than doing duplicate work. There is no running bot or guaranteed response time.

## 3. Return the confirmation to your AI

A coordinator checks the current board and records the claim with the board's current file SHA. They return [a claim-confirmation packet](production/forms/CLAIM-CONFIRMATION.md).

Copy that packet back to your AI. The confirmation must identify the task, worker, claim token, board revision and saved GitHub commit/board link, allowed output paths and exact input revisions. Your AI must verify the saved record if it can read GitHub; otherwise ask you to paste the current matching board entry. The issue author or a random commenter cannot grant ownership merely by writing a confirmation-shaped message.

If the coordinator requests changes, paste those instructions back to the AI. If the claim is declined, revoked or mismatched, the AI must not proceed under that claim.

## 4. Complete only the claimed task

The AI works only from the declared inputs and produces only the permitted output files. It should check the task's acceptance criteria and report limits honestly.

An AI without GitHub access drafts the files in the chat or as downloadable text files. It does not need to create a branch or pretend it opened a pull request; the coordinator handles that later. Missing inputs or revoked ownership must be resolved before more work. Reuse valid accepted evidence rather than repeat discovery.

## 5. Send the finished work back

Ask the AI to complete [the finished-work packet](production/forms/FINISHED-WORK.md), including the full contents of every proposed output file, acceptance checks, source revisions, evidence and unresolved items.

Open [Submit finished AI work](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/issues/new?template=finished-work.yml). Paste the packet and link the original claim issue. Replace title placeholders. Keep further corrections or large content parts as comments on this submission issue.

If the packet is too long, split it into numbered parts on the same issue. Repeat the task, worker and claim token in every part. Include a manifest of all paths and part counts; finish with the exact END marker shown in the template. Do not use ellipses, summaries or “unchanged content here” in place of required file contents. Alternatively attach a complete text/archive package and include the same manifest. The coordinator must be able to retrieve it.

Tell the AI that posting a submission is not acceptance. It should not announce the task finished on the shared board or begin another task until its claim is explicitly released by the coordinator. Ask for a release even when the submission is waiting for review.

## 6. Review and handoff

The coordinator verifies the live claim and complete packet, stores the proposed files on a work branch, records the submission issue and commit/PR on the board, and changes the task to review using an atomic board update. A submission can be blocked or returned for corrections. A receipt must say which occurred.

Only the project owner or an appointed reviewer accepts and integrates work. An issue being closed, a form being submitted or a claim being released does not mean the result was accepted.

Use the original claim issue for “still working”, blocked, withdrawal or release requests; include task ID, worker ID, token, reason and any draft location. An issue comment is a request, not a board mutation. No automatic expiry transfers ownership.

## For coordinators

Follow docs/PRODUCTION.md. Re-fetch the live board; validate readiness, accepted/accessibility of inputs, one active task per worker and output overlap; preserve other claims; save with the current board SHA; reread and verify before sending a confirmation. On a conflict, re-evaluate rather than force an overwrite.

When receiving work, verify identity/claim, input provenance, permitted paths, all packet parts and file completeness before creating the integration branch. Record the exact submission and source commits. Keep review distinct from acceptance and explicitly record claim release. A public claim token is not authentication or permission to execute submitted code.

Do not request API keys, passwords, private repository contents or real member/corporation data. All issues and attachments in this public repository are public. This workflow requires no credential sharing and grants no new access.

## Start links

- [Live task board](production/board.json)
- [Claim-request copy-and-paste packet](production/forms/CLAIM-REQUEST.md)
- [Coordinator confirmation packet](production/forms/CLAIM-CONFIRMATION.md)
- [Finished-work copy-and-paste packet](production/forms/FINISHED-WORK.md)
- [GitHub issue chooser](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/issues/new/choose)
