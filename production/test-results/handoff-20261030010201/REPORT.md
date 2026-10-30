# User-mediated AI contribution test — HANDOFF-20261030010201

Date: 30 October 2026. **Result: live GitHub handoff mechanics passed; browser and independent-AI usability remain untested.**

This is a synthetic workflow test requested by the project owner. It is not an accepted build-map deliverable or evidence that Eve Cloud works.

## Evidence trail

- [Claim request and coordinator confirmation](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/issues/1) — opening the issue did not grant ownership; the coordinator separately saved and verified the claim.
- [Finished-work submission](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/issues/2) — wrong-token initial packet refused; corrected part 1 held pending; corrected part 2 completed the packet.
- [Draft review PR](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/3) — one synthetic Markdown file transcribed from the issue comments.
- [Immutable supplied input](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a5932f71bc9c7e4819b345d5ff1e290a05524272/production/test-inputs/handoff-20261030010201.md).
- [Exact transferred output](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/da8bb22d7e2bb213da1b8c7cba517614f8d78578/production/test-results/handoff-20261030010201/fixture.md).
- [Saved claim](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/ac91e05b86e4a2cc974c566a2fa054a6d9f89e60/production/board.json).
- [Review and explicit claim release](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/ef89b11b20d412c286c590018838c0073de1457f/production/board.json).

## Checks and observed results

| Check | Observed result | Enforcement tested |
| --- | --- | --- |
| Issue request alone is not ownership | Board remained ready until a separate claim write | Actual saved board read |
| Claim saved before work | Matching task, worker and token reread from board | Coordinator protocol and GitHub API |
| Stale competing claim | GitHub returned HTTP 409; board unchanged | Actual GitHub SHA conflict |
| Two producers on one task | Existing claimed status refused a second claimant | Test coordinator admission check |
| Same worker on another task | Existing unreleased claim refused MAP-001 | Test coordinator admission check; MAP-001 unchanged |
| Wrong-token finished packet | Refused; no board transition | Test coordinator identity/claim check |
| Missing second packet part | Held pending; no final marker or complete file | Test coordinator completeness check |
| Complete two-part submission | Reassembled directly from fetched issue comments | Live GitHub text transport |
| UTF-8 and Markdown integrity | Exact content match including café, em dash, m³, JSON fence and final newline | Remote file readback |
| Review handoff | Branch and draft PR #3 created; board changed to review | Live GitHub branch/commit/PR and board API |
| Explicit claim release | released_at saved; no active test claim remains | Remote board readback |
| Existing production work | All 15 original task records and both backlog records unchanged | Structured before/after comparison |
| Acceptance separation | accepted_revision remains null; draft PR unmerged | Remote state and coordinator rule |

## Final state

The synthetic task is in review with its producer claim released. The request issue is closed as processed; the finished-work issue and draft PR remain open for project-owner review. Closing the request did not accept the output. Normal map tasks were not consumed. No autonomous inbox processor or queue service was installed.

## Limits

- Browser control failed to initialise before any UI action. Actual form typing, browser validation and human clipboard interaction were not tested.
- One agent simulated contributor, messenger and coordinator roles; no independent LLM session with GitHub tools disabled was run.
- Wrong-token, duplicate-work and completeness gates were applied by the test coordinator, not a deployed automatic validator.
- GitHub rejected the stale SHA through its actual API; intentional bypass by a privileged writer is outside this cooperative protocol.
- No product code, integration, app functionality, private repository contents or real map task was tested or changed.
- Draft PR and synthetic task remain for owner review; no self-acceptance or merge was performed.

An actual user copying the forms between a separate talking-AI chat and GitHub in a browser remains a useful next usability check. This test does not claim that every AI will follow the instructions or that form validation alone enforces board rules.
