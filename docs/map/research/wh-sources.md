# pfh59/eve-whmapper pinned source extracts

Commit: 2a493fad9acec9a8e15b619f7943ae8b6e7f30da
These are inspected source/document extracts, not runtime verification. MIT licence reproduced below. Dependencies/assets/data require their own licence and compatibility checks before copying. No upstream scripts were executed.

## LICENSE
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/LICENSE
Lines 1-22 of 22. Missing lines are not supplied evidence.

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

## README.md
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/README.md
Lines 1-60 of 60. Missing lines are not supplied evidence.

```text
# EvE-WHMapper
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) ![GitHub top language](https://img.shields.io/github/languages/top/pfh59/eve-whmapper) ![GitHub language count](https://img.shields.io/github/languages/count/pfh59/eve-whmapper) [![Continous Integration and Deployment](https://github.com/pfh59/eve-whmapper/actions/workflows/ci-cd.yaml/badge.svg)](https://github.com/pfh59/eve-whmapper/actions/workflows/ci-cd.yaml) [![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=pfh59_eve-whmapper&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=pfh59_eve-whmapper) ![GitHub commit activity (main)](https://img.shields.io/github/commit-activity/m/pfh59/eve-whmapper) ![GitHub Release](https://img.shields.io/github/v/release/pfh59/eve-whmapper) ![Downloads (all assets, all releases)](https://img.shields.io/github/downloads/pfh59/eve-whmapper/total) ![GitHub Downloads (all assets, latest release)](https://img.shields.io/github/downloads/pfh59/eve-whmapper/latest/total)

EvE-WHMapper is a lightweight wormhole mapping and planning tool for EVE Online. It was originally inspired by [Pathfinder](https://github.com/exodus4d/pathfinder) and has been redesigned to be easier to deploy, maintain, and use in modern fleets and wormhole groups.

Key goals:
- Lightweight and fast
- Simple to deploy and administrate
- Easy to maintain over time

## Core Features

### Authentication
- CCP SSO login
- ESI API integration
- Multi-account support

### Access Control & Administration
- Define administration access lists per character
- Control Eve-WHMapper access for alliances, corporations, and characters
- Configure per-map access lists

### Map Module
- Share maps with other players and alts
- Track pilots and their current locations
- Automatic location tracking via ESI
- Auto-tag multi-system targets with the same class using A/B/C markers (or adjust manually with `+` / `-` or `Up` / `Down` keys)
- Add systems manually via right-click
- Select multiple systems with `Ctrl` + left click and move them together
- Link two systems by selecting them and pressing `L`
- Edit existing system connection links
- Lock systems to prevent accidental moves

### Route Planner Module
- Calculate optimal travel paths between systems—using both stargates and mapped wormholes
- Support route planning for individuals or fleets moving across your chain

### Jump Module
- Track and summarize all jumps between two systems
- Display hole size and current status (e.g., Normal / Critical)
- Show first and last jump information
- Keep a detailed log of each pilot and ship that passes through

## Hosting & Public Instance

EvE-WHMapper can be self-hosted using Docker, Kubernetes, or other deployment options described in the documentation.

For hosted usage, a public instance is available at [https://www.whmapper.ovh](https://www.whmapper.ovh), where you can create and manage your own Eve WHMapper space for an alliance, corporation, or personal use.

## Documentation

Full documentation (installation, configuration, modules, and usage guides) is available at: [https://pfh59.github.io/eve-whmapper-docs/home](https://pfh59.github.io/eve-whmapper-docs/home).

## Contributing

Contributions are welcome. Please see the repository's contributing guidelines in `CONTRIBUTING.md` before opening issues or pull requests.

## License

This project is released under the [MIT License](https://opensource.org/licenses/MIT).
```

## src/WHMapper/WHMapper.csproj
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/WHMapper.csproj
Lines 1-52 of 52. Missing lines are not supplied evidence.

```text
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net10.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
    <UserSecretsId>4a1af26f-e1f0-4229-b68c-16e61e58037d</UserSecretsId>
    <Version>0.0.0</Version>
    <SatelliteResourceLanguages>en</SatelliteResourceLanguages>
  </PropertyGroup>

  <ItemGroup>
    <None Include="Services/BrowserClientIdProvider/IBrowserClientIdProvider.cs" />
  </ItemGroup>

  <ItemGroup>
    <EmbeddedResource Include="Resources/wh-effects.json" />
  </ItemGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.EntityFrameworkCore" Version="10.*" />
    <PackageReference Include="Microsoft.Extensions.Http.Resilience" Version="10.9.0" />
    <PackageReference Include="MudBlazor" Version="9.9.0" />
    <PackageReference Include="Serilog.AspNetCore" Version="10.*" />
    <PackageReference Include="Serilog.Settings.Configuration" Version="10.*" />
    <PackageReference Include="Serilog.Sinks.File" Version="7.0.0" />
    <PackageReference Include="Z.Blazor.Diagrams" Version="3.0.4.1" />
    <PackageReference Include="YamlDotNet" Version="18.*" />
    <PackageReference Include="FluentValidation" Version="12.*" />
    <PackageReference Include="Microsoft.IdentityModel.Protocols.OpenIdConnect" Version="8.22.0" />
    <PackageReference Include="Microsoft.AspNetCore.SignalR.Client" Version="10.*" />
    <PackageReference Include="FibonacciHeap" Version="2.0.2" />
    <PackageReference Include="Microsoft.AspNetCore.Authentication.JwtBearer" Version="10.*" />
    <PackageReference Include="Npgsql" Version="10.*" />
    <PackageReference Include="Npgsql.EntityFrameworkCore.PostgreSQL" Version="10.*" />
    <PackageReference Include="Microsoft.IdentityModel.JsonWebTokens" Version="8.22.0" />
    <PackageReference Include="Microsoft.AspNetCore.Authentication.OpenIdConnect" Version="10.*" />
    <PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="10.*" />
    <PackageReference Include="Microsoft.Extensions.Caching.StackExchangeRedis" Version="10.*" />
    <PackageReference Include="Microsoft.AspNetCore.DataProtection.StackExchangeRedis" Version="10.*" />
    <PackageReference Include="Z.Blazor.Diagrams.Algorithms" Version="3.0.4.1" />
    <PackageReference Include="OpenTelemetry" Version="1.18.0" />
    <PackageReference Include="OpenTelemetry.Exporter.OpenTelemetryProtocol" Version="1.18.0" />
    <PackageReference Include="OpenTelemetry.Extensions.Hosting" Version="1.18.0" />
    <PackageReference Include="OpenTelemetry.Instrumentation.AspNetCore" Version="1.18.0" />
    <PackageReference Include="OpenTelemetry.Instrumentation.Http" Version="1.18.0" />
    <PackageReference Include="OpenTelemetry.Instrumentation.Process" Version="1.18.0-rc.1" />
    <PackageReference Include="OpenTelemetry.Instrumentation.Runtime" Version="1.18.0" />
  </ItemGroup>

</Project>

```

## src/WHMapper/Models/Db/WHSignature.cs
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Models/Db/WHSignature.cs
Lines 1-113 of 113. Missing lines are not supplied evidence.

```text
﻿using System.ComponentModel.DataAnnotations;
using WHMapper.Models.Db.Enums;

namespace WHMapper.Models.Db
{

    public class WHSignature
    {
        private const string DEFAULT_SCAN_USER_VALUE = "Unknown";

        [Key]
        public int Id { get;  set; }

        [Required]
        public int WHId { get; set; }


        [Required]
        [StringLength(7, ErrorMessage = "Bad Signature Format")]
        public string Name { get; set; } = string.Empty;


        private WHSignatureGroup _sigGroup = WHSignatureGroup.Unknow;

        [Required]
        public WHSignatureGroup Group
        {
            get
            {
                return _sigGroup;
            }

            set
            {
                if (_sigGroup != value)
                    Type = String.Empty;

                _sigGroup = value;
            }
        } 

        public string? Type { get;  set; }

        [Required]
        public DateTime Created { get; set; } = DateTime.UtcNow;
        [Required]
        public string? CreatedBy { get; set; } = DEFAULT_SCAN_USER_VALUE;
        [Required]
        public DateTime Updated { get;  set; } = DateTime.UtcNow;
        [Required]
        public string? UpdatedBy { get; set; } = DEFAULT_SCAN_USER_VALUE;

        [Obsolete("EF Requires it")]
        protected WHSignature() { }

        public WHSignature(int whId,string name) :
            this(whId,name, DEFAULT_SCAN_USER_VALUE)
        {

        }

        public WHSignature(int whId, string name,string scanUser)
            : this(whId,name,WHSignatureGroup.Unknow,null,scanUser)
        {

        }

        public WHSignature(int whId, string name, WHSignatureGroup group, string? type,string scanUser)
        {
            WHId = whId;
            Name = name;
            Group = group;
            Type = type;
            CreatedBy = scanUser;
            UpdatedBy = scanUser;
        }

        public WHSignature(int whId, string name, WHSignatureGroup group, string? type) :
            this(whId,name, group,type, DEFAULT_SCAN_USER_VALUE)
        {

        }

        /// <summary>
        /// Indicates whether this signature has the same name, group and type as another signature.
        /// </summary>
        /// <remarks>
        /// A null type and an empty type are considered equal. Audit fields are ignored.
        /// </remarks>
        public bool HasSameContent(WHSignature other)
        {
            return Name == other.Name
                && Group == other.Group
                && string.Equals(Type ?? string.Empty, other.Type ?? string.Empty, StringComparison.Ordinal);
        }

        /// <summary>
        /// Indicates whether the group is known and the type is set, as for a signature probed to 100%.
        /// </summary>
        /// <remarks>
        /// A method rather than a property, so Entity Framework never maps it.
        /// </remarks>
        public bool IsIdentified()
        {
            return Group != WHSignatureGroup.Unknow && !string.IsNullOrWhiteSpace(Type);
        }


    }

}


```

## src/WHMapper/Models/Db/WHMapAccess.cs
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Models/Db/WHMapAccess.cs
Lines 1-48 of 48. Missing lines are not supplied evidence.

```text
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

## src/WHMapper/Data/WHMapperContext.cs
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Data/WHMapperContext.cs
Lines 1-104 of 104. Missing lines are not supplied evidence.

```text
﻿using Microsoft.EntityFrameworkCore;
using WHMapper.Models.Db;

namespace WHMapper.Data
{
    public class WHMapperContext : DbContext
	{
        // Core tables
        public DbSet<WHMap> DbWHMaps { get; set; } = null!;
		public DbSet<WHSystem> DbWHSystems { get; set; } = null!;
        public DbSet<WHSystemLink> DbWHSystemLinks { get; set; } = null!;
        public DbSet<WHSignature> DbWHSignatures { get; set; } = null!;
        public DbSet<WHNote> DbWHNotes { get; set; } = null!;
        public DbSet<WHRoute> DbWHRoutes { get; set; } = null!;
        public DbSet<WHJumpLog> DbWHJumpLogs { get; set; } = null!;

        // Multi-tenant instance tables
        public DbSet<WHInstance> DbWHInstances { get; set; } = null!;
        public DbSet<WHInstanceAdmin> DbWHInstanceAdmins { get; set; } = null!;
        public DbSet<WHInstanceAccess> DbWHInstanceAccesses { get; set; } = null!;
        public DbSet<WHMapAccess> DbWHMapAccesses { get; set; } = null!;
        public DbSet<WHUserSetting> DbWHUserSettings { get; set; } = null!;

        // Activity log tables
        public DbSet<WHActivityType> DbWHActivityTypes { get; set; } = null!;
        public DbSet<WHActivityLog> DbWHActivityLogs { get; set; } = null!;

        public WHMapperContext(DbContextOptions<WHMapperContext> options) : base(options)
		{

        }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<WHInstance>().ToTable("Instances");
            modelBuilder.Entity<WHInstance>().HasIndex(x => new { x.OwnerEveEntityId, x.OwnerType }).IsUnique(true);
            modelBuilder.Entity<WHInstance>().HasMany(x => x.WHMaps).WithOne().HasForeignKey(x => x.WHInstanceId).OnDelete(DeleteBehavior.Cascade);
            modelBuilder.Entity<WHInstance>().HasMany(x => x.Administrators).WithOne().HasForeignKey(x => x.WHInstanceId).IsRequired().OnDelete(DeleteBehavior.Cascade);
            modelBuilder.Entity<WHInstance>().HasMany(x => x.InstanceAccesses).WithOne().HasForeignKey(x => x.WHInstanceId).IsRequired().OnDelete(DeleteBehavior.Cascade);

            modelBuilder.Entity<WHInstanceAdmin>().ToTable("InstanceAdmins");
            modelBuilder.Entity<WHInstanceAdmin>().HasIndex(x => new { x.WHInstanceId, x.EveCharacterId }).IsUnique(true);

            modelBuilder.Entity<WHInstanceAccess>().ToTable("InstanceAccesses");
            modelBuilder.Entity<WHInstanceAccess>().HasIndex(x => new { x.WHInstanceId, x.EveEntityId, x.EveEntity }).IsUnique(true);

            modelBuilder.Entity<WHMap>().ToTable("Maps");
            modelBuilder.Entity<WHMap>().HasIndex(x => new { x.Name }).IsUnique(true);
            modelBuilder.Entity<WHMap>().HasMany(x => x.WHSystems).WithOne().HasForeignKey(x => x.WHMapId).IsRequired().OnDelete(DeleteBehavior.Cascade);
            modelBuilder.Entity<WHMap>().HasMany(x => x.WHSystemLinks).WithOne().HasForeignKey(x => x.WHMapId).IsRequired().OnDelete(DeleteBehavior.Cascade);
            modelBuilder.Entity<WHMap>().HasMany(x => x.WHMapAccesses).WithOne(x => x.WHMap).HasForeignKey(x => x.WHMapId).IsRequired().OnDelete(DeleteBehavior.Cascade);

            modelBuilder.Entity<WHMapAccess>().ToTable("MapAccesses");
            modelBuilder.Entity<WHMapAccess>().HasIndex(x => new { x.WHMapId, x.EveEntityId, x.EveEntity }).IsUnique(true);

            modelBuilder.Entity<WHSystem>().ToTable("Systems");
            modelBuilder.Entity<WHSystem>().HasIndex(x => new { x.WHMapId,x.SoloarSystemId }).IsUnique(true);
            modelBuilder.Entity<WHSystem>().HasIndex(x => new { x.WHMapId,x.Name }).IsUnique(true);
            modelBuilder.Entity<WHSystem>().HasOne<WHMap>().WithMany(x => x.WHSystems).HasForeignKey(x =>x.WHMapId).IsRequired().OnDelete(DeleteBehavior.Cascade);
            modelBuilder.Entity<WHSystem>().HasMany<WHSystemLink>().WithOne().HasForeignKey(x=>x.IdWHSystemFrom).OnDelete(DeleteBehavior.Cascade);
            modelBuilder.Entity<WHSystem>().HasMany<WHSystemLink>().WithOne().HasForeignKey(x => x.IdWHSystemTo).OnDelete(DeleteBehavior.Cascade);

            modelBuilder.Entity<WHSystemLink>().ToTable("SystemLinks");
            modelBuilder.Entity<WHSystemLink>().HasIndex(x => new { x.WHMapId,x.IdWHSystemFrom, x.IdWHSystemTo }).IsUnique(true);
            modelBuilder.Entity<WHSystemLink>().HasOne<WHMap>().WithMany(x => x.WHSystemLinks).HasForeignKey(x =>x.WHMapId).IsRequired().OnDelete(DeleteBehavior.Cascade);
            modelBuilder.Entity<WHSystemLink>().HasMany<WHJumpLog>(x=>x.JumpHistory).WithOne().HasForeignKey(x => x.WHSystemLinkId).IsRequired().OnDelete(DeleteBehavior.Cascade);
      
            modelBuilder.Entity<WHSignature>().ToTable("Signatures");
            modelBuilder.Entity<WHSignature>().HasIndex(x => new { x.WHId,x.Name }).IsUnique(true);
            modelBuilder.Entity<WHSignature>().HasOne<WHSystem>().WithMany(x => x.WHSignatures).HasForeignKey(x=>x.WHId).IsRequired().OnDelete(DeleteBehavior.Cascade);

            modelBuilder.Entity<WHNote>().ToTable("Notes");
            modelBuilder.Entity<WHNote>().HasOne<WHMap>().WithMany().HasForeignKey(x => x.MapId).IsRequired().OnDelete(DeleteBehavior.Cascade);
            modelBuilder.Entity<WHNote>().HasIndex(x => new { x.MapId, x.SoloarSystemId }).IsUnique(true);

            modelBuilder.Entity<WHRoute>().ToTable("Routes");
            modelBuilder.Entity<WHRoute>().HasOne<WHMap>().WithMany().HasForeignKey(x => x.MapId).IsRequired().OnDelete(DeleteBehavior.Cascade);
            modelBuilder.Entity<WHRoute>().HasIndex(x => new { x.MapId,x.SolarSystemId,x.EveEntityId }).IsUnique(true);

            modelBuilder.Entity<WHJumpLog>().ToTable("JumpLogs");
            modelBuilder.Entity<WHJumpLog>().HasIndex(x => new { x.CharacterId, x.JumpDate }).IsUnique(true);

            modelBuilder.Entity<WHUserSetting>().ToTable("UserSettings");
            modelBuilder.Entity<WHUserSetting>().HasIndex(x => x.EveCharacterId).IsUnique(true);

            modelBuilder.Entity<WHActivityType>().ToTable("ActivityTypes");
            modelBuilder.Entity<WHActivityType>().Property(x => x.Id).ValueGeneratedNever();
            modelBuilder.Entity<WHActivityType>().HasIndex(x => x.Code).IsUnique(true);
            // Ids are explicit so they match WHActivityTypeIds on every deployment.
            modelBuilder.Entity<WHActivityType>().HasData(
                new WHActivityType(WHActivityTypeIds.SignatureCreated, "SignatureCreated", "Signature created"),
                new WHActivityType(WHActivityTypeIds.SignatureUpdated, "SignatureUpdated", "Signature updated"),
                new WHActivityType(WHActivityTypeIds.SystemOpened, "SystemOpened", "System opened"));

            modelBuilder.Entity<WHActivityLog>().ToTable("ActivityLogs");
            // Restrict: an activity type still referenced by the history cannot be deleted.
            modelBuilder.Entity<WHActivityLog>().HasOne<WHActivityType>().WithMany().HasForeignKey(x => x.WHActivityTypeId).IsRequired().OnDelete(DeleteBehavior.Restrict);
            // No foreign key to maps or systems: deleting them must not delete the history.
            modelBuilder.Entity<WHActivityLog>().HasIndex(x => new { x.WHInstanceId, x.ActivityDate });
            modelBuilder.Entity<WHActivityLog>().HasIndex(x => new { x.WHMapId, x.ActivityDate });
        }
    }
}

```

## deploy/docker/eve-whmapper/docker-compose.yml
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/deploy/docker/eve-whmapper/docker-compose.yml
Lines 1-46 of 46. Missing lines are not supplied evidence.

```text
services:
  db:
    image: postgres:17-alpine
    restart: always
    environment:
      POSTGRES_USER: ${POSTGRES_USER:-postgres}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-secret}
      POSTGRES_DB: whmapper
      PGDATA: /data/postgres
    volumes:
     - postgres:/data/postgres
    networks:
     - net

  redis:
    image: redis:8-alpine
    restart: always
    networks:
     - net

  whmapper:
    image: ghcr.io/pfh59/eve-whmapper:latest
    restart: unless-stopped
    environment:
     - EveSSO__ClientId=xxxxxxxxx
     - EveSSO__Secret=xxxxxxxxx
     - ConnectionStrings__DatabaseConnection=server=db;port=5432;database=whmapper;User Id=postgres;Password=secret
     - ConnectionStrings__RedisConnection=redis:6379
     - Serilog__MinimumLevel__Default=Warning
     - Serilog__MinimumLevel__Override__Microsoft.EntityFrameworkCore.Database.Command=Warning
    links:
      - db
      - redis
    depends_on:
      - db
      - redis
    networks:
     - net
    volumes:
     - ./Logs:/app/Logs

networks:
  net:

volumes:
    postgres:
```

## src/WHMapper/Models/Db/WHSystemLink.cs
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Models/Db/WHSystemLink.cs
Lines 1-49 of 49. Missing lines are not supplied evidence.

```text
﻿using System.ComponentModel.DataAnnotations;
using WHMapper.Models.Db.Enums;

namespace WHMapper.Models.Db
{
    public class WHSystemLink
    {
        [Key]
        public int Id { get; set; }

        [Required]
        public int WHMapId { get; set; }

        [Required]
        public int IdWHSystemFrom { get; set; }

        [Required]
        public int IdWHSystemTo  { get; set; }

        [Required]
        public SystemLinkEolStatus EndOfLifeStatus { get; set; } = SystemLinkEolStatus.Normal;

        [Required]
        public SystemLinkSize Size { get; set; } = SystemLinkSize.Large;

        [Required]
        public SystemLinkMassStatus MassStatus { get; set; } = SystemLinkMassStatus.Normal;

        [Required]
        public virtual ICollection<WHJumpLog> JumpHistory { get; } = new HashSet<WHJumpLog>();


        [Obsolete("EF Requires it")]
        protected WHSystemLink() { }
        public WHSystemLink(int idWHSystemFrom, int idWHSystemTo) :
            this(0,idWHSystemFrom,idWHSystemTo)
        {
        }

        public WHSystemLink(int whMapId,int idWHSystemFrom, int idWHSystemTo)
        {
            WHMapId = whMapId;
            IdWHSystemFrom = idWHSystemFrom;
            IdWHSystemTo = idWHSystemTo;
        }
    }
}


```

## src/WHMapper/Models/Db/WHJumpLog.cs
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Models/Db/WHJumpLog.cs
Lines 1-47 of 47. Missing lines are not supplied evidence.

```text
﻿using System.ComponentModel.DataAnnotations;

namespace WHMapper.Models.Db;

public class WHJumpLog
{
    [Key]
    public int Id { get; set; }

    [Required]
    public int WHSystemLinkId { get; set; }

    [Required]
    public int CharacterId { get; set; }
    
    [Required]
    public DateTime JumpDate { get; set; }

    public int? ShipTypeId { get; set; }

    public long? ShipItemId { get; set; }
    
    public float? ShipMass { get; set; }

    [Obsolete("EF Requires it")]
    protected WHJumpLog() { }
    
    //Construstor when lin k are create manually, no ship used
    public WHJumpLog(int linkId,int characterId) :
     this(linkId, characterId, null, null, null)
    {

    }

   //Constrtuctor for real jump with a real ship 
    public WHJumpLog(int linkId,int characterId,int? shipTypeId, long? shipItemId, float? shipMass)
    {
        WHSystemLinkId=linkId;
        CharacterId = characterId;
        JumpDate = DateTime.UtcNow;
        ShipTypeId = shipTypeId;
        ShipItemId = shipItemId;
        ShipMass = shipMass;
    }

}

```

## src/WHMapper/Services/EveOAuthProvider/EVEOnlineAuthenticationDefaults.cs
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Services/EveOAuthProvider/EVEOnlineAuthenticationDefaults.cs
Lines 1-43 of 43. Missing lines are not supplied evidence.

```text
﻿namespace WHMapper.Services.EveOAuthProvider
{
    public static class EVEOnlineAuthenticationDefaults
    {
        /// <summary>
        /// Default value for <see cref="AuthenticationScheme.Name"/>.
        /// </summary>
        public const string AuthenticationScheme = "EVEOnline";

        /// <summary>
        /// Default value for <see cref="AuthenticationScheme.DisplayName"/>.
        /// </summary>
        public static readonly string DisplayName = "EVEOnline";

        /// <summary>
        /// Default value for <see cref="AuthenticationSchemeOptions.ClaimsIssuer"/>.
        /// </summary>
        public static readonly string Issuer = "EVEOnline";

        /// <summary>
        /// Default value for <see cref="RemoteAuthenticationOptions.CallbackPath"/>.
        /// </summary>
        public static readonly string CallbackPath = "/signin-eveonline";

        /// <summary>
        /// Default value for <see cref="OAuthOptions.AuthorizationEndpoint"/>.
        /// </summary>
        public static readonly string AuthorizationEndpoint = "https://login.eveonline.com/v2/oauth/authorize";

        /// <summary>
        /// Default value for <see cref="OAuthOptions.TokenEndpoint"/>.
        /// </summary>
        public static readonly string TokenEndpoint = "https://login.eveonline.com/v2/oauth/token";
        public static readonly string JWKEndpoint = "https://login.eveonline.com/oauth/jwks";
        public static readonly string RevokeTokenEndpoint = "https://login.eveonline.com/v2/oauth/revoke";

        public const string Scopes = "urn:eveonline:scopes";

        public static readonly string ValideIssuer = "https://login.eveonline.com";
        public static readonly string ValideAudience = "EVE Online";
    }
}

```

## src/WHMapper.Tests/WHHelper/WHSignatureHelperImportTests.cs
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper.Tests/WHHelper/WHSignatureHelperImportTests.cs
Lines 1-115 of 115. Missing lines are not supplied evidence.

```text
using Moq;
using WHMapper.Models.Db;
using WHMapper.Models.Db.Enums;
using WHMapper.Repositories.WHSignatures;
using WHMapper.Services.WHSignatures;

namespace WHMapper.Tests.WHHelper;

public class WHSignatureHelperImportTests
{
    private const int WH_ID = 1;
    private const string SCAN_USER = "FOOBAR";
    private const string UNRESOLVED_SIG_NAME = "IGU-360";
    private const string WORMHOLE_SIG_NAME = "WAM-436";
    private const string UNSTABLE_WORMHOLE = "Unstable Wormhole";

    // One unresolved signature and one signature resolved as a wormhole.
    private static readonly string SCAN = string.Join(Environment.NewLine,
        $"{UNRESOLVED_SIG_NAME}\tCosmic Signature\t\t\t0,0%\t37,21 AU",
        $"{WORMHOLE_SIG_NAME}\tCosmic Signature\tWormhole\t{UNSTABLE_WORMHOLE}\t100,0%\t101 km");

    [Fact]
    public async Task ImportScanResult_WhenScanIsUnchanged_ReportsNoChange()
    {
        var existingSignatures = new List<WHSignature>
        {
            new(WH_ID, UNRESOLVED_SIG_NAME, WHSignatureGroup.Unknow, string.Empty),
            new(WH_ID, WORMHOLE_SIG_NAME, WHSignatureGroup.Wormhole, UNSTABLE_WORMHOLE)
        };
        var sut = new WHSignatureHelper(CreateRepository(existingSignatures).Object);

        var result = await sut.ImportScanResult(SCAN_USER, WH_ID, SCAN, false);

        Assert.True(result.Persisted);
        Assert.Equal(0, result.FullyScannedCreatedCount);
        Assert.Equal(0, result.FullyScannedChangedCount);
    }

    [Fact]
    public async Task ImportScanResult_WhenGroupIsResolved_ReportsOneChange()
    {
        var existingSignatures = new List<WHSignature>
        {
            new(WH_ID, UNRESOLVED_SIG_NAME, WHSignatureGroup.Unknow, string.Empty),
            new(WH_ID, WORMHOLE_SIG_NAME, WHSignatureGroup.Unknow, string.Empty)
        };
        var sut = new WHSignatureHelper(CreateRepository(existingSignatures).Object);

        var result = await sut.ImportScanResult(SCAN_USER, WH_ID, SCAN, false);

        Assert.True(result.Persisted);
        Assert.Equal(0, result.FullyScannedCreatedCount);
        Assert.Equal(1, result.FullyScannedChangedCount);
        Assert.Equal(WHSignatureGroup.Wormhole, existingSignatures[1].Group);
        Assert.Equal(UNSTABLE_WORMHOLE, existingSignatures[1].Type);
    }

    [Fact]
    public async Task ImportScanResult_WhenSignaturesAreNew_CountsOnlyFullyScannedAsCreated()
    {
        var repository = CreateRepository(new List<WHSignature>());
        var sut = new WHSignatureHelper(repository.Object);

        var result = await sut.ImportScanResult(SCAN_USER, WH_ID, SCAN, false);

        Assert.True(result.Persisted);
        // Both signatures are created, but only the one at 100% counts.
        repository.Verify(r => r.Create(It.Is<IEnumerable<WHSignature>>(sigs => sigs.Count() == 2)), Times.Once);
        Assert.Equal(1, result.FullyScannedCreatedCount);
        Assert.Equal(0, result.FullyScannedChangedCount);
    }

    [Fact]
    public async Task ImportScanResult_WhenGroupIsResolvedBelowFullSignal_ReportsNoChange()
    {
        var existingSignatures = new List<WHSignature>
        {
            new(WH_ID, WORMHOLE_SIG_NAME, WHSignatureGroup.Unknow, string.Empty)
        };
        var sut = new WHSignatureHelper(CreateRepository(existingSignatures).Object);
        string partialScan = $"{WORMHOLE_SIG_NAME}\tCosmic Signature\tWormhole\t\t42,5%\t12,3 AU";

        var result = await sut.ImportScanResult(SCAN_USER, WH_ID, partialScan, false);

        Assert.True(result.Persisted);
        Assert.Equal(WHSignatureGroup.Wormhole, existingSignatures[0].Group);
        Assert.Equal(0, result.FullyScannedChangedCount);
    }

    [Theory]
    [InlineData("100,0%")]
    [InlineData("100.0%")]
    [InlineData("100.0 %")]
    public async Task ImportScanResult_WhenSignalStrengthUsesAnyDecimalSeparator_CountsFullyScanned(string signalStrength)
    {
        var sut = new WHSignatureHelper(CreateRepository(new List<WHSignature>()).Object);
        string scan = $"{WORMHOLE_SIG_NAME}\tCosmic Signature\tWormhole\t{UNSTABLE_WORMHOLE}\t{signalStrength}\t101 km";

        var result = await sut.ImportScanResult(SCAN_USER, WH_ID, scan, false);

        Assert.Equal(1, result.FullyScannedCreatedCount);
    }

    private static Mock<IWHSignatureRepository> CreateRepository(List<WHSignature> existingSignatures)
    {
        var repository = new Mock<IWHSignatureRepository>();
        repository.Setup(r => r.GetByWHId(WH_ID)).ReturnsAsync(existingSignatures);
        repository.Setup(r => r.Update(It.IsAny<IEnumerable<WHSignature>>()))
            .ReturnsAsync((IEnumerable<WHSignature> signatures) => signatures.Cast<WHSignature?>().ToList());
        repository.Setup(r => r.Create(It.IsAny<IEnumerable<WHSignature>>()))
            .ReturnsAsync((IEnumerable<WHSignature> signatures) => signatures.Cast<WHSignature?>().ToList());
        return repository;
    }
}

```
