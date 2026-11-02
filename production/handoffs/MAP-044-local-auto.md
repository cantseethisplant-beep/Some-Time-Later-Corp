# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/38

Automated critic only; independent review pending.

# Handoff — MAP-044 ESI research report

Task: MAP-044 — Research ESI location, ship, polling and rate-limit contracts
Claim commit (tracked, not a token): 3904087aa16c2a43b51e065ef87a53044f7e23bf
Worker: hermes-laptop-map-044-auto-20261030
Output delivered: docs/map/specs/loop-map-044-wh-research.md (complete file section above)

Inputs consumed:
- docs/map/specs/loop-map-042-wh-design.md @ 6e023274d7cb692f36b132d980d5a335d4387897 (baseline, UNACCEPTED)
- docs/map/research/LOCAL-RESEARCH.md @ 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec
- docs/map/research/NEXT-SOURCE-SNAPSHOT.json @ 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec (pins esi/esi-docs 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d; pathfinder 06af7d86fe6456947fb960220c54d02a8623c0ff; eve-whmapper 2a493fad9acec9a8e15b619f7943ae8b6e7f30da)
- docs/map/research/next-esi-sources.md @ 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec (ESI pack: overview.md sha256 bbc184e12fbac3808523b8e0a6b4e4fd76aba92ca988f74bd01853836f7d1de9, retrieved 2026-11-02T15:49:04.221763Z; rate-limiting.md sha256 05bcba0b7beb70d85555519613f049935fc5a5fb0accd61e7ae640e2e008e5ff, retrieved 2026-11-02T15:49:04.570577Z; best-practices.md sha256 f56bbb52daa9ba23c32074216df285e73678663821ffd6e9a5bb371839de653c, retrieved 2026-11-02T15:49:04.915083Z)

Public metadata receipts recorded:
- https://esi.evetech.net/meta/compatibility-dates (208 bytes, sha256 7ac78423fb677a08e0edaac0c8fb71e3a70a6abb1e98071fddc45a4aad61e299, retrieved 2026-11-02T15:49:01.061611Z)
- https://esi.evetech.net/meta/openapi.json?compatibility_date=2026-08-18 (614672 bytes, sha256 9a9a0f4af77216300e960cfd2576c9baac085a8170022e40c928c28622d80fc6, retrieved 2026-11-02T15:49:01.330345Z)
- https://login
.eveonline.com/.well-known/oauth-authorization-server (813 bytes, sha256 dc04adbd7e6c74e1e6c3e50efa20a0bd7814bef66a04ec6526f8ce3fe16eb572, retrieved 2026-11-02T15:49:01.485329Z)

Checks actually performed:
- Pinned ESI source text read (overview.md, rate-limiting.md, best-practices.md, LICENSE lines 1-22).
- Public metadata inspected: compatibility date requested 2026-08-18, returned spec version 2026-08-18, title "EVE SKINR Ingenuity (ESI) - tranquility".
- Selected-paths inventory checked for jump-log endpoints: none found in selected_paths or all_path_names (snapshot-limited negative).
- Legacy 100 errors/minute → 420 coexistence with new per-route bucket limits documented.
- Four location/ship operations extracted with required scopes, response fields, cache metadata, and rate-limit extensions.
- Root MIT licence notice preserved; CCP developer agreement flagged as unreviewed/unaccepted.

Limitations:
- No network, shell, account, delegation or server tools used; no authenticated/player route called.
- Public metadata snapshot only; no runtime verification or accepted facts.
- Absence from this path inventory is not proof of absence from all CCP services.
- Negative claim limited to snapshot esi/esi-docs 98b42d5..., compatibility date 2026-08-18, retrieved 2026-11-02.

Remaining work / review pending:
- OD-03 ESI scopes/rate limits/issuer runtime contract remains missing runtime evidence.
- Polling interval is an owner decision; not prescribed here.
- Jump-log requirement unsupported by this snapshot; owner decision or additional upstream evidence needed.
- CCP developer agreement requires owner review; no agreement accepted.
- Coordinator review and acceptance gate pending; this report is not accepted or build-ready.



## Automated screening
{
  "task_id": "MAP-044",
  "decision": "submit_draft",
  "summary": "The MAP-044 research report is complete and source-linked. It inventories the four location/ship OpenAPI operations with scopes, parameters, response fields, cache metadata and rate-limit extensions; records the requested compatibility date (2026-08-18) and returned spec version (2026-08-18); documents floating-window bucket rate limiting, token costs, headers, Retry-After, and coexistence with the legacy 100-errors/minute 420 error limit; explains what an opted-in character can supply and what is unknown between polls; makes a snapshot-limited negative finding on a character-scoped jump-log endpoint; clearly separates documented/inspected findings from proposed checklist items and unresolved decisions (OD-03/06/07, polling interval); preserves the root MIT licence; and makes no claims of tested calls, accepted facts, or blueprint acceptance. No actionable defects found.",
  "findings": []
}
