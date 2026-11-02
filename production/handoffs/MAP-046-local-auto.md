# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/40

Automated critic only; independent review pending.

MAP-046 — Research map access, bootstrap and membership behavior
Claim worker: hermes-laptop-map-046-auto-20261030
Claim commit: 1f2915de0262953dbdf7a92d9fb7af2c5894e22f
Output produced: docs/map/specs/loop-map-046-wh-research.md (one file section, plain text, no wrapper)
Inputs used:
- docs/map/specs/loop-map-042-wh-design.md @ 6e023274d7cb692f36b132d980d5a335d4387897 (baseline blueprint context; unaccepted)
- docs/map/research/LOCAL-RESEARCH.md @ 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec (research policy/inventory)
- docs/map/research/NEXT-SOURCE-SNAPSHOT.json @ 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec (snapshot pins: esi/esi-docs 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d; pathfinder 06af7d86fe6456947fb960220c54d02a8623c0ff; eve-whmapper 2a493fad9acec9a8e15b619f7943ae8b6e7f30da)
- docs/map/research/next-access-sources.md @ 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec (access pack: six complete files at eve-whmapper 2a493fa...; receipt sha256/bytes/etag recorded in section 2 of the report)
Diagnosed issues and exact corrections:
1. Section 3.1 step 3 (and section 6 test #3) previously misstated the null-primaryAccount control flow in EveMapperRequirementHandlerBase.cs. Correction: when GetPrimaryAccountAsync returns null after an account-group match, the if block has no return in the null case, so execution falls through to IsAuthorizedAsync(authenticatedCharacterId); fail-closed on that branch is not current source behavior.
2. Section 6 item 8 previously conflated helper returning false with helper throwing. Correction: EveMapperRequirementHandlerBase.HandleRequirementAsync awaits IsAuthorizedAsync with no try/catch on either the primary-account path or the direct fallback, so a helper exception propagates out of the handler and aborts the request instead of leaving an unsatisfied requirement; split into two unexecuted, source-linked expectations — helper returns false leaves the requirement unsatisfied (clean denial); helper throws propagates an unhandled exception/aborts the request — pending IEveMapperAccessHelper implementations (OD-09).
Checks actually performed: read all six access-pack files in full; traced visible call relationships (handler base → browser client provider → user management → abstract IsAuthorizedAsync; access/admin handlers → IEveMapperAccessHelper; registration helper → instance/character/EVE mapper services + CreateInstanceAsync); inspected WHMapAccess empty-list policy comment; mapped OD-09/10/13/14 to evidence; proposed ten negative-case tests (none executed); proposed six candidate amendments (none adopted).
Limitations: no handler/service implementations supplied (IEveMapperAccessHelper and all service interfaces are missing); tests read not executed; no ESI/scope/rate-limit evidence in this pack; no first-owner seed, cache invalidation, membership sync, or role column visible; root MIT notice does not cover transitive/asset/game-data/CCP terms.
Remaining work: owner decisions OD-09, OD-10, OD-13, OD-14; missing source evidence listed in section 9; report consolidation into evidence register.
Review pending: coordinator review of this report; no self-acceptance; not acceptance, merge, or build-ready certification.


## Automated screening
{
  "task_id": "MAP-046",
  "decision": "submit_draft",
  "summary": "No current actionable defects. The MAP-046 research report is source-linked to all six access-pack files at eve-whmapper 2a493fa... with receipt hashes, labels evidence status (documented-primary/inspected/proposed/unresolved), states research version 1, and lists explicit missing evidence in section 9. It keeps recommendations, owner choices, and unexecuted test proposals distinct from primary claims. It covers OD-09/10/13/14, traces visible handler call relationships, distinguishes missing service implementations from proved orchestration logic, and addresses first-owner bootstrap, the per-map empty-list policy, character/corporation/alliance membership, administrator boundaries, and cache invalidation limitations, without claiming acceptance, runtime verification, server access, accepted facts, app implementation, costs, or blueprint overwrite. Section 6 test proposals and section 7 amendments are explicitly marked unexecuted and non-mandatory. The corrected null-primaryAccount fall-through behavior in section 3.1 and test #3 matches the supplied EveMapperRequirementHandlerBase.cs source.",
  "findings": []
}
