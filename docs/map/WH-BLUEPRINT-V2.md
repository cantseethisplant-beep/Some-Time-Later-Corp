# WHMapper + WH Tools + optional Hosting — start here

This is the owner-directed v2 planning/build proposal. It favours two mods to EVE-WHMapper rather than the older new-app-first approach. No app or cloud deployment has been built; independent review and the listed implementation/release gates remain.

## Reading order

1. [Architecture and scope](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/1fff5e1110d2bbfebed1d96a993aa6e5cfafd71e/docs/map/specs/map-050-01-architecture.md): pinned base, exactly two modules, small maintained bridge, integer core IDs and UUID module records, trust/consent boundaries and OD decisions.
2. [WH Tools](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/1fff5e1110d2bbfebed1d96a993aa6e5cfafd71e/docs/map/specs/map-050-02-wh-tools.md): one useful evidence-stamped observation workflow first; reuse existing mapper features; uncertainty, conflict and sharing controls.
3. [Hosting](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/1fff5e1110d2bbfebed1d96a993aa6e5cfafd71e/docs/map/specs/map-050-03-hosting.md): optional/read-only first, separate owner/operator authority and bounded approvals; no hidden cloud commands or self-destruction.
4. [Build and acceptance](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/1fff5e1110d2bbfebed1d96a993aa6e5cfafd71e/docs/map/specs/map-050-04-build-and-acceptance.md): nine dependency-ordered steps, sixteen focused checks and requirement traceability. These are future checks, not passing app tests.
5. [Oracle behind Cloudflare](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/1fff5e1110d2bbfebed1d96a993aa6e5cfafd71e/docs/map/specs/map-050-05-oracle-cloudflare.md): conditional pilot origin, live account/quota/ARM/proxy/SSO/recovery qualification required. No promise of free guaranteed production capacity.
6. [Integration sources](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/1fff5e1110d2bbfebed1d96a993aa6e5cfafd71e/docs/map/specs/map-050-06-integration-sources.md) and [completed research](research/RESEARCH-HANDOFF.md): exact source versions, 35 evidence records, limitations and licence notices.

## What changed

The base is EVE-WHMapper at the manifest's immutable commit. Two separately versioned modules use a compile-time maintained integration patch; a supported hot plugin ABI has not been demonstrated. Core integer IDs remain intact; module records use UUIDs. Hosting stays optional even if Oracle hosts the app. Cloudflare remains the public midpoint; PostgreSQL/Redis remain private. Source facts, proposed policies and runtime evidence remain distinct.

MAP-049 has a disclosed coordinator correction without native recheck; this v2 blueprint is Codex-authored from the owner's direction and source-reconciled native Hermes research. No native generation/approval is claimed for v2. Original v1 and research history remain available.

## Next action

Review this concrete proposal, then authorise the first implementation milestone if desired. Start with M-B00/M-B01 and an isolated synthetic fixture profile. Do not jump from a document to real cloud/player credentials or automated hosting effects. Before release, produce the exact locks/notices, authorization/consent/proxy/restore evidence, measured capacity and operator account/domain decisions named in the build plan. A future builder can use this package without repeating broad discovery; revalidate only changed or unresolved scoped evidence.

manifest.json records immutable commits and SHA-256 for all pinned content. Old v1 remains historical; do not treat both designs as simultaneously authoritative. No server was used, no paid fallback or automated task loop remains, and no independent acceptance/merge occurred.


[Exact-source manifest](WH-MODULES-BLUEPRINT-MANIFEST.json). Historical [v1 guide](WH-BLUEPRINT-V1.md) remains available; the owner's two-module direction supersedes its new-app-first recommendation.
