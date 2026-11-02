# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/39

Automated critic only; independent review pending.

MAP-045 dependency and licence evidence-gap research report complete at docs/map/specs/loop-map-045-wh-research.md.

Diagnosed issues and exact corrections:
1. Direct-vs-transitive misclassification: react/promise ^3.2, react/socket ^1.16, react/promise-stream ^1.7 and clue/ndjson-react ^1.3 are declared in composer.json `require` (production, direct per §3.1) but §3.2 previously listed them under "Transitive (inferred)". Corrected: reclassified these four as direct production dependencies in §3.2 and §4. cache/adapter-common 1.3.0, cache/hierarchical-cache 1.2.0, cache/tag-interop 1.1.0, ikkez/f3-schema-builder v2.2.6 and the remaining react/psr/symfony/evenement/ralouphie/caseyamcl packages remain transitive/inferred.
2. Scoped inventory omissions: §4 previously omitted direct production dependencies ikkez/f3-cortex (GPL-3.0, dev-master#47d2596914776877ef4d87706d1faa812d1398f2), ikkez/f3-sheet (GPL-3.0, v0.4.3), xfra35/f3-cron (GPL-3.0-only, v1.3.0), league/html-to-markdown (MIT, 5.2.3), react/promise (v3.3.0), react/socket (v1.17.0), react/promise-stream (v1.7.0) and clue/ndjson-react (v1.3.0). Rows added with declaration, locked version from composer.lock, declared licence, prod group and direct flag.
3. Source-inventory receipt accuracy: the three root LICENSE files (esi/esi-docs, Pathfinder, EVE-WHMapper) have no fetch receipt or hash in the packet; retrieval evidence now reads "quoted inline in next-dependencies-sources.md; no fetch receipt in packet" and SHA256 "not receipted in packet". Timestamps/hashes retained only for the five receipted items (Pathfinder composer.json/composer.lock, EVE-WHMapper WHMapper.csproj/src/global.json, esi docs/resources/license.md).

Inputs verified present and pinned: baseline 6e023274d7cb692f36b132d980d5a335d4387897 (MAP-042 WH design candidate); inventory 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec (LOCAL-RESEARCH.md + NEXT-SOURCE-SNAPSHOT.json); dependencies 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec (next-dependencies-sources.md). Sources used: pinned esi/esi-docs LICENSE (CCP hf MIT 2015), Pathfinder LICENSE (Mark Friedrich MIT 2017), EVE-WHMapper LICENSE (pfh59 MIT 2023), Pathfinder composer.json + composer.lock projection (locked), EVE-WHMapper WHMapper.csproj + src/global.json (declarations only, no lock), esi docs/resources/license.md (CCP developer agreement pointer at https://developers.eveonline.com/license-agreement).

Checks actually performed: document-level reading only; separated declared vs locked versions (PHP locked via unverified projection; .NET declarations only, no lock supplied); separated require from require-dev (PHP) and prod from design-time (.NET where identifiable); catalogued audit-ignore entry PKSA-y2cr-5h3j-g3ys and allow-plugin entry dealerdirect/phpcodesniffer-composer-installer; catalogued declared GPL-3.0/BSD-3-Clause/MIT/LGPL labels in the projection (labels, not inspected licence files); verified root-require packages against composer.json for direct-vs-transitive classification.

Limitations and remaining uncertainty: no network/shell/account/server tools; no composer install/audit, dotnet restore, vulnerability scan, licence-file inspection beyond roots, SBOM, asset licence reads, CCP agreement review, legal interpretation, compatibility/security/runtime tests; composer.lock projection packet-labelled as not independently verified; direct-vs-transitive separation not fully completable from the projection alone (composer.json require is the authoritative direct-declaration source); asset licences, CCP agreement terms, and ESI scope/rate-limit/issuer contracts were not supplied and remain unchecked.

Remaining upstream checks: Pathfinder actual licence-file inspection and audit-ignore/allow-plugin owner review; EVE-WHMapper lock file acquisition and NuGet licence review; asset licence reads (wh-effects.json, Pathfinder favicon/logo); CCP developer agreement review; ESI scopes/rate limits/issuer contract (sibling packets out of scope).

Unresolved owner decisions: OD-02 stack/runtime, OD-04 dependency audit scope, OD-05 assets/game-data/ESI terms, OD-12 database engine. Evidence status: documented/inspected claims quoted from pinned packets; proposed framing labelled; no accepted facts. No tests or acceptance claimed; submission is not build-ready; awaiting coordinator review.


## Automated screening
{
  "task_id": "MAP-045",
  "decision": "submit_draft",
  "summary": "No current actionable defects in docs/map/specs/loop-map-045-wh-research.md. The draft correctly separates declared vs locked/floating versions (composer.json require plus composer.lock projection; WHMapper.csproj declarations with no lock file supplied), direct vs transitive packages (composer.json require treated as authoritative), declared SPDX labels vs inspected root LICENCE texts only, and production vs dev tooling (PHP require/require-dev separated; .NET dev split noted as not evidenced). It catalogues config.audit.ignore PKSA-y2cr-5h3j-g3ys, config.allow-plugins, wildcard ranges, dev-master, pre-release and GPL-family entries without vulnerability claims, provides a scoped non-SBOM inventory with exact remaining upstream checks, links the official CCP developer agreement, and leaves assets/game-data/terms plus OD-02/OD-04/OD-05/OD-12 owner decisions unresolved, with no acceptance, implementation or verified-claim statements.",
  "findings": []
}
