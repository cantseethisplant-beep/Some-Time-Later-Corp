# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/37

Automated critic only; independent review pending.

# MAP-043 handoff — SSO, token validation and revocation evidence

**Task:** MAP-043. **Claim commit:** 398d68d456d6b3691565c1c394d894e187c60f2f (tracked by commit, not token). **Worker:** hermes-laptop-map-043-auto-20261030. **Output:** docs/map/specs/loop-map-043-wh-research.md (complete file section delivered above).

**Exact sources used:**
- esi/esi-docs @ 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d: docs/services/sso/index.md (lines 1-221), snippets/sso/authorization-code-pkce.py (1-71), snippets/sso/validate-jwt-token.py (1-86); receipts included in report §2.
- pfh59/eve-whmapper @ 2a493fad9acec9a8e15b619f7943ae8b6e7f30da: src/WHMapper/Services/EveOAuthProvider/Services/EVEOnlineTokenProvider.cs (1-162, complete); receipt sha256 cd989360... in report §2.
- ESI public metadata snapshot @ 2026-11-02T15:49:01Z: compatibility-dates, openapi.json (compatibility_date=2026-08-18), .well-known/oauth-authorization-server; receipt sha256 values in report §2.
- Policy/context: docs/map/research/LOCAL-RESEARCH.md @ 01e3a01b..., MAP-042 blueprint context @ 6e023274...

**Checks actually performed:** full reads of all pinned packets; receipt hash verification where supplied; cross-check of discovery metadata vs documented endpoints; inspected provider behavior for refresh/expiry/revoke/cache-clear and failure modes; consistency check of MAP-042 §11 and OD-03/07/14 against sourced contract (found consistent: marked runtime-unverified/unresolved).

**Limitations:** no authenticated route called; no app registered; no terms accepted; no runtime, test, security, compatibility, licence-acceptance, or cost evidence; documentation treated as vendor description, not implementation proof; inspected code not executed. Missing evidence listed in report §11.

**Remaining work / review pending:** owner decisions OD-03 (ESI scopes/rate limits/issuer contract), OD-07 (token storage, encrypted-at-rest, revocation effectiveness), OD-14 (opt-in defaults, expiry, per-jump vs continuous); CCP developer agreement review; transitive dependency/asset/game-data licence checks; runtime validation of JWT validation, refresh rotation, and revocation failure handling in any future implementation. This report does not self-accept, amend MAP-042 text, or certify build readiness; it is review material for the evidence register/amendment stage.

**Evidence status labels used:** documented-primary, inspected-source, public-metadata, proposed, unresolved — preserved throughout; no unresolved policy presented as a mandate.



## Automated screening
{
  "task_id": "MAP-043",
  "decision": "submit_draft",
  "summary": "No defects found. The MAP-043 research report is source-linked to pinned commits/paths with receipt hashes, labels every finding's evidence status (documented-primary, inspected-source, public-metadata, proposed, unresolved), gives validity/version and invalidation conditions per claim in the §6 claim validation register, and lists explicit unavailable evidence in §11. Recommendations and owner choices (§9 questions, §10 proposed amendments) are kept distinct from primary claims; the report makes no server-access, acceptance, implementation, cost, or blueprint-overwrite claims, does not infer handler security or choose consent defaults, and explicitly treats MAP-042 as unaccepted context only. It addresses OD-03/07/14 by separating the documented authorization/PKCE/JWT/discovery/refresh/revocation contract (§3) from the inspected upstream token-provider code (§4), enumerating rotation/revocation failure cases (§4.5, §7), and distinguishing external token revocation from local cache logout and consent (§8).",
  "findings": []
}
