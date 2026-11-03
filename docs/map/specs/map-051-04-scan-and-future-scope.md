# Scan and future feature boundaries

This resolves R03 by selecting the safe P0 branch of the review: **sidecar notes only; no combined base-scan transaction is promised or exposed**. Existing WHMapper paste/signature/route functions stay base functions, separately qualified in the baseline. Tools notes do not parse pasted signatures or attach themselves automatically to a jump/connection. A note's only target is a verified core system belonging to its map. Core signature/connection reference types are therefore absent from the P0 API, rather than guessed from names.

## Version/operation disposition

| Existing proposal | v3 treatment | Reopening condition |
|---|---|---|
| TO-04 scan preview | No product route/feature in P0 | A separately versioned import grammar, fixtures and pinned base signature IDs are completed |
| TO-05 atomic scan commit | No product route/feature; no base writes | Exact base repository/DbContext transaction seam and concurrency tests prove common commit, or a new proposal specifies a visible reconciliation workflow |
| TO-06 uncertain route overlay | Base route UI only, no Tools verdict | Typed core connection identity + source/age semantics + tested scope checks |
| TO-07 export | Operator encrypted backup only; no user bulk-export API | Redaction/version/scope/retention and export permission contract complete |
| core observation and corroborated labels | P0 rejects caller source/uncertainty fields; all notes manual/reported | Verified adapter provenance, origin immutability, duplicate identity and corroboration evidence rules complete |
| Hosting execution/node catalog/scheduling | Disabled; read-only contract in 07 | Separate command, enrollment, fencing, credential, approval and effect/reconciliation contracts with acceptance evidence |

## Exact constraints for a future scan task

The next scan design task must read the immutable selected base implementation, not repeat all research. It must identify actual signature/connection PK types, map/system foreign keys, normalization/validation and write service/DbContext lifetimes. Preserve the base's current signature constraint initially; seven-character declaration is not a universal EVE rule. Any type change is an explicit compatibility decision.

Its required fixtures are: empty input, malformed/partial row, duplicate identical row, duplicate conflicting row, case/whitespace normalization, same signature with changed type/group, missing pasted row, deleted/reused signature, different-map reference, two previews of the same revision, expired preview, role/consent revoke between preview and commit, identical retry, changed-payload retry and failure between core/sidecar writes. Missing row must never mean automatic deletion. Preview must bind actor/map/system, canonical input digest, base revisions and five-minute server expiry. Commit revalidates all of them, reauthorizes and fails STALE_PREVIEW if any changed. A preview is not authority to write after revoke.

Until a common transaction is demonstrated, future scan tooling can save an explicitly separate manual evidence note only and direct the user to the normal base scan workflow. It must never report that both committed atomically. P0 does not need to discover or implement that transaction seam to deliver its selected note slice.

## Completion claim

P0 completeness means the bounded selected feature set is specified; it does not mean every long-term WH or hosting ambition is ready to build. Future requirements remain a labelled backlog and cannot silently appear in a release advert or a task's acceptance criteria. This is a scope decision, not a claim that missing evidence was found.
