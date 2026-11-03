# Review dispositions and primary source record

Date: 3 November 2026. Evidence labels: inspected-source, documented-primary, selected-design, not-run. This is a Codex reconciliation; native Hermes did not author or approve it. No extra Hermes inference is consumed. The v2 package, original research and previous review remain immutable history.

## Seven findings

| Finding | Document disposition | Runtime/approval disposition |
|---|---|---|
| R01 consent/access/bootstrap | Specified in 01, exact operation matrix and owner recovery | Q05/Q06/Q10/Q11 NOT_RUN; live-data policy acknowledgement still required |
| R02 provenance | Manual/reported server-only in 02/09; unsupported fields rejected | Q07/Q08 NOT_RUN; core ingestion explicitly deferred |
| R03 scans/atomicity | Sidecar-only P0 chosen in 03/04; no ambiguous combined commit | Q09/Q15/Q16 NOT_RUN; future scan task has exact prerequisites |
| R04 Redis keys | Dedicated protected filesystem ring and maintenance migration, full restore/journal plan in 05 | Q18/Q19/Q20 NOT_RUN; actual key/cache consumer inventory required |
| R05 migration failure | One deployment owner, read-only schema readiness, fail closed in 05 | Q17 NOT_RUN |
| R06 exact contracts | 01/02/03/07/09 define roles, DTOs, limits, states, errors and fixtures | Contract fixtures checked separately; Q runtime checks NOT_RUN |
| R07 bounded release | P0 scope/targets/build graph and applicable checks in 00/06 | Independent review/component/environment gates still open |

These findings are resolved at specification level, not marked independently accepted, runtime safe or fully build-ready under the repository completion gate. Required component evidence cannot be supplied by wording. No production entitlement, domain, operator or backup destination is invented.

## Required integration patch inventory

- Startup: compile-time module/bridge registrations, feature/version gates; production startup migration replaced by exact schema/readiness verification and private health.
- Identity/base access: exact verified actor selection, per-map helper, membership age/expiry metadata, local ACL/map/account invalidation hooks and single-process gates. Existing global authorization handlers are not sufficient for map-scoped module access.
- Core destructive operations: reject map/system removal/reparenting while active module references exist; no silent FK cascade or unsynchronized SQL path.
- Keys: supported durable protected key store, explicit existing Redis ring migration/consumer inventory and session shutdown/restore epoch handling.
- UI/events/API: Tools panel, module-specific HTTP and invalidation hub with per-operation and per-recipient checks; no base scan implementation replacement.
- Database: module-owned schema/history, manifest-bound migrations and minimum runtime DB privilege; optional Hosting ledger separately enabled.

This enumerates proposed patch responsibilities, not claims that upstream already implements them. Before adding feature code the baseline spike must record actual touched methods/files and prove the seams; inability to cover a path is a blocked qualification, not permission to bypass it.

## Frozen sources and evidence limits

- MAP-050 v2 output: `1fff5e1110d2bbfebed1d96a993aa6e5cfafd71e`, draft PR #44, six completed released unaccepted documents.
- MAP-049 register: `1c853a2c267494e8e2d9507214fb2d2ffe8573ed`, draft PR #43. Completed source-qualified synthesis, not independent acceptance.
- Original primary research packets: `01e3a01b4e4deb9317f304aa2977be8f2a8e6dec`; includes notices and exact ESI/auth/access/dependency/options/observations scope. Do not treat unavailable runtime evidence as documented facts.
- Additional integration/Oracle packet: `9ef8585addc52d9a42ed8997f7d5cdddad5cac55`; dated Oracle/Cloudflare observations, not this account's quota or tested deployment.
- Base: `pfh59/eve-whmapper@2a493fad9acec9a8e15b619f7943ae8b6e7f30da`. Three additional complete source files below were read at that commit through the GitHub connector. Their local snapshot hashes cover the delivered normalized UTF-8 text, not a claimed original HTTP-byte receipt.
- Microsoft primary documentation consulted 3 November 2026: [key providers](https://learn.microsoft.com/en-us/aspnet/core/security/data-protection/implementation/key-storage-providers?view=aspnetcore-10.0), [EF migration application](https://learn.microsoft.com/en-us/ef/core/managing-schemas/migrations/applying), and [ASP.NET antiforgery](https://learn.microsoft.com/en-us/aspnet/core/security/anti-request-forgery?view=aspnetcore-10.0). The selected CSRF design uses explicit server validation; existing middleware presence alone does not qualify future endpoints. Documentation is mutable: recheck affected mechanism on framework/provider change, not on a recurring general audit.

## Source observations versus choices

The per-map helper reads the map, denies null instance, obtains character corporation/alliance, checks instance allowance then map allowance. The interface supplies per-map, instance and instance-admin methods. WHMapAccess documents unrestricted maps within an allowed instance when no map restrictions exist. Tools explicit grants narrow these existing semantics; v3 does not silently rewrite them. Source inspection does not prove endpoint coverage, data freshness or atomic module/core behavior.

The supplied older integration source also shows Redis DataProtection-Keys persistence and a logged migration exception without rethrow. v3's key migration, gate/invalidation hooks, protected endpoints, migration job, journal, limits, retention, target timings and compatibility manifest are selected NEW design requirements. They are not upstream feature claims or accepted legal/provider policies.

Oracle remains a conditional later origin behind Cloudflare. Retain the dated option document in the package and qualify actual Console/home-region quota, ARM builds, egress/storage/backup costs, domain/callback, origin isolation, trusted proxies and real-time reconnect at deployment. No free allowance is treated as permanent. No account, existing physical server or paid service was accessed.

## Upstream licence notice

```text
MIT License

Copyright (c) 2023 pfh59

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

```

## src/WHMapper/Services/EveMapper/EveMapperAccessHelper.cs

Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Services/EveMapper/EveMapperAccessHelper.cs

Snapshot SHA-256: `12f7bdf8ecbc25ffec856c32685fa9a8bcf8a13327fa13583916bc2d2687ba53`. Complete file; source inspection only.

```csharp
﻿using WHMapper.Models.Db.Enums;
using WHMapper.Repositories.WHMaps;
using WHMapper.Repositories.WHInstances;
using WHMapper.Repositories.WHMapAccesses;
using WHMapper.Services.EveAPI.Characters;

namespace WHMapper.Services.EveMapper
{
    public class EveMapperAccessHelper : IEveMapperAccessHelper
    {
        private readonly ICharacterServices _characterServices;
        private readonly IWHMapRepository _mapRepo;
        private readonly IWHInstanceRepository _instanceRepo;
        private readonly IWHMapAccessRepository _mapAccessRepo;

        public EveMapperAccessHelper(
            IWHMapRepository mapRepo, 
            IWHInstanceRepository instanceRepo,
            IWHMapAccessRepository mapAccessRepo,
            ICharacterServices characterServices)
        {
            _mapRepo = mapRepo;
            _instanceRepo = instanceRepo;
            _mapAccessRepo = mapAccessRepo;
            _characterServices = characterServices;
        }

        /// <summary>
        /// Check if a user has access to at least one instance.
        /// If no instances exist, user has no access (must register first).
        /// </summary>
        public async Task<bool> IsEveMapperUserAccessAuthorized(int eveCharacterId)
        {
            // Get character info for corp/alliance check
            var characterInfo = await _characterServices.GetCharacter(eveCharacterId);
            if (!characterInfo.IsSuccess || characterInfo.Data == null)
                return false;

            var charData = characterInfo.Data;
            
            // Check if user has access to any instance
            var accessibleInstances = await _instanceRepo.GetAccessibleInstancesAsync(
                eveCharacterId, 
                charData.CorporationId > 0 ? charData.CorporationId : null,
                charData.AllianceId > 0 ? charData.AllianceId : null);

            return accessibleInstances?.Any() == true;
        }

        /// <summary>
        /// Check if any of the provided characters has access to at least one instance.
        /// Used for multi-account scenarios where the user may have multiple EVE characters linked.
        /// </summary>
        public async Task<bool> IsEveMapperUserAccessAuthorizedForAny(IEnumerable<int> eveCharacterIds)
        {
            if (eveCharacterIds == null || !eveCharacterIds.Any())
                return false;

            foreach (var characterId in eveCharacterIds)
            {
                if (await IsEveMapperUserAccessAuthorized(characterId))
                    return true;
            }
            return false;
        }

        /// <summary>
        /// Check if a user is admin of at least one instance.
        /// </summary>
        public async Task<bool> IsEveMapperAdminAccessAuthorized(int eveCharacterId)
        {
            var administeredInstances = await _instanceRepo.GetInstancesForAdminAsync(eveCharacterId);
            return administeredInstances?.Any() == true;
        }

        /// <summary>
        /// Check if a user has access to a specific map through its instance and map-level access control.
        /// </summary>
        public async Task<bool> IsEveMapperMapAccessAuthorized(int eveCharacterId, int mapId)
        {
            // Get the map to check its instance
            var map = await _mapRepo.GetById(mapId);
            if (map == null)
                return false;

            // Map must belong to an instance
            if (!map.WHInstanceId.HasValue)
                return false;

            var characterResult = await _characterServices.GetCharacter(eveCharacterId);
            if (!characterResult.IsSuccess || characterResult.Data == null)
                return false;

            var character = characterResult.Data;
            int? corporationId = character.CorporationId > 0 ? character.CorporationId : null;
            int? allianceId = character.AllianceId > 0 ? character.AllianceId : null;

            // First check instance-level access
            var hasInstanceAccess = await _instanceRepo.HasInstanceAccessAsync(
                map.WHInstanceId.Value,
                eveCharacterId,
                corporationId,
                allianceId);

            if (!hasInstanceAccess)
                return false;

            // Check map-level access
            // If no restrictions exist on the map, all instance members can access it
            // If restrictions exist, check if user has explicit access
            return await _mapAccessRepo.HasMapAccessAsync(mapId, eveCharacterId, corporationId, allianceId);
        }

        /// <summary>
        /// Check if a user has access to a specific instance, without considering map-level restrictions.
        /// </summary>
        public async Task<bool> IsEveMapperInstanceAccessAuthorized(int eveCharacterId, int instanceId)
        {
            var characterResult = await _characterServices.GetCharacter(eveCharacterId);
            if (!characterResult.IsSuccess || characterResult.Data == null)
                return false;

            var character = characterResult.Data;

            return await _instanceRepo.HasInstanceAccessAsync(
                instanceId,
                eveCharacterId,
                character.CorporationId > 0 ? character.CorporationId : null,
                character.AllianceId > 0 ? character.AllianceId : null);
        }

        /// <summary>
        /// Ids of every instance the character can access, through character, corporation or alliance.
        /// </summary>
        public async Task<IEnumerable<int>> GetAccessibleInstanceIdsAsync(int eveCharacterId)
        {
            var characterResult = await _characterServices.GetCharacter(eveCharacterId);
            if (!characterResult.IsSuccess || characterResult.Data == null)
                return Enumerable.Empty<int>();

            var character = characterResult.Data;

            var instances = await _instanceRepo.GetAccessibleInstancesAsync(
                eveCharacterId,
                character.CorporationId > 0 ? character.CorporationId : null,
                character.AllianceId > 0 ? character.AllianceId : null);

            return instances?.Select(i => i.Id).ToArray() ?? Enumerable.Empty<int>();
        }

        /// <summary>
        /// Checks if a character is an admin of a specific instance
        /// </summary>
        public async Task<bool> IsInstanceAdminAuthorized(int eveCharacterId, int instanceId)
        {
            return await _instanceRepo.IsInstanceAdminAsync(instanceId, eveCharacterId);
        }

        /// <summary>
        /// Returns the instance a map belongs to, or null when the map is unknown or orphaned.
        /// </summary>
        public async Task<int?> GetMapInstanceIdAsync(int mapId)
        {
            var map = await _mapRepo.GetById(mapId);
            return map?.WHInstanceId;
        }
    }
}


```

## src/WHMapper/Services/EveMapper/IEveMapperAccessHelper.cs

Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Services/EveMapper/IEveMapperAccessHelper.cs

Snapshot SHA-256: `7a7a03f2b8fcd6965e1fcd2d129db7f3d5088c1325ac6c0e98ce4599b3b824f8`. Complete file; source inspection only.

```csharp
﻿namespace WHMapper.Services.EveMapper
{
    public interface IEveMapperAccessHelper
    {
        public Task<bool> IsEveMapperUserAccessAuthorized(int eveCharacterId);
        public Task<bool> IsEveMapperUserAccessAuthorizedForAny(IEnumerable<int> eveCharacterIds);
        public Task<bool> IsEveMapperAdminAccessAuthorized(int eveCharacterId);
        public Task<bool> IsEveMapperMapAccessAuthorized(int eveCharacterId, int mapId);
        public Task<bool> IsEveMapperInstanceAccessAuthorized(int eveCharacterId, int instanceId);

        /// <summary>
        /// Ids of every instance the character can access, through character, corporation or alliance.
        /// </summary>
        public Task<IEnumerable<int>> GetAccessibleInstanceIdsAsync(int eveCharacterId);
        public Task<bool> IsInstanceAdminAuthorized(int eveCharacterId, int instanceId);

        /// <summary>
        /// Returns the instance a map belongs to, or null when the map is unknown or orphaned.
        /// </summary>
        public Task<int?> GetMapInstanceIdAsync(int mapId);
    }
}


```

## src/WHMapper/Models/Db/WHMapAccess.cs

Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Models/Db/WHMapAccess.cs

Snapshot SHA-256: `c026fc11edb865c9bc7e0baf558c756122925769d3aeca5a03da43287103919e`. Complete file; source inspection only.

```csharp
using System.ComponentModel.DataAnnotations;
using WHMapper.Models.Db.Enums;

namespace WHMapper.Models.Db
{
    /// <summary>
    /// Represents an access entry for a specific map within an instance.
    /// When no access entries exist for a map, all instance members can access it.
    /// When at least one access entry exists, only explicitly granted entities can access the map.
    /// </summary>
    public class WHMapAccess
    {
        [Key]
        public int Id { get; set; }

        [Required]
        public int WHMapId { get; set; }

        /// <summary>
        /// The EVE entity ID (character, corporation, or alliance ID)
        /// </summary>
        [Required]
        public int EveEntityId { get; set; }

        [Required]
        [StringLength(255)]
        public string EveEntityName { get; set; } = string.Empty;

        [Required]
        public WHAccessEntity EveEntity { get; set; }

        public DateTime GrantedAt { get; set; } = DateTime.UtcNow;

        public virtual WHMap? WHMap { get; set; }

        [Obsolete("EF Requires it")]
        protected WHMapAccess() { }

        public WHMapAccess(int whMapId, int eveEntityId, string eveEntityName, WHAccessEntity eveEntity)
        {
            WHMapId = whMapId;
            EveEntityId = eveEntityId;
            EveEntityName = eveEntityName;
            EveEntity = eveEntity;
        }
    }
}


```
