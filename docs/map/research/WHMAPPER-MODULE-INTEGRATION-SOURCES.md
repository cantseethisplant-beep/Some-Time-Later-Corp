# WHMapper module integration evidence

Repository: pfh59/eve-whmapper; immutable commit: 2a493fad9acec9a8e15b619f7943ae8b6e7f30da.
Inspected source text only. These files demonstrate explicit registration and typed base entities; they do not prove a supported general plugin loader, complete authorization or successful build/runtime integration. No upstream code was executed. The two-module bridge remains a proposed maintained patch.

## LICENSE
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/LICENSE
Complete file, lines 1–22.
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

## src/WHMapper/Program.cs
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Program.cs
Complete file, lines 1–126.
```text
using MudBlazor;
using MudBlazor.Services;
using Microsoft.AspNetCore.ResponseCompression;
using System.Net;
using WHMapper;
using WHMapper.Components;
using WHMapper.Extensions;
using WHMapper.Hubs;
using WHMapper.Services.BrowserClientIdProvider.Extension;
using Serilog;



var builder = WebApplication.CreateBuilder(args);

builder.Host.UseSerilog((context, services, configuration) =>
{
    configuration
        .ReadFrom.Configuration(context.Configuration)
        .ReadFrom.Services(services);
});

// Infrastructure
builder.Services.AddDatabaseServices(builder.Configuration);
builder.Services.AddEveAuthentication(builder.Configuration);
builder.Services.AddExternalApiClients(builder.Configuration);
builder.Services.AddMapperServices();
builder.Services.AddWHMapperTelemetry(builder.Configuration, builder.Environment.ApplicationName);

// SignalR & Blazor
builder.Services.AddSignalR(options =>
{
    // Tolerate browser tab throttling: timers in background tabs can fire as slowly as ~1/min.
    // Server waits up to 2 min for a client ping before treating the connection as dead,
    // and pings the client every 15s.
    options.ClientTimeoutInterval = TimeSpan.FromMinutes(2);
    options.KeepAliveInterval = TimeSpan.FromSeconds(15);
    options.HandshakeTimeout = TimeSpan.FromSeconds(30);
});
builder.Services.AddCascadingAuthenticationState();
builder.Services.AddHttpContextAccessor();

builder.Services.AddRazorComponents()
    .AddInteractiveServerComponents(options =>
    {
        // Retain disconnected Blazor circuits longer so a backgrounded tab can resume
        // without "Circuit not initialized" forcing a full page reload.
        options.DisconnectedCircuitMaxRetained = 100;
        options.DisconnectedCircuitRetentionPeriod = TimeSpan.FromMinutes(10);
    });

builder.Services.AddMudServices(config =>
{
    config.SnackbarConfiguration.PositionClass = Defaults.Classes.Position.BottomRight;
    config.SnackbarConfiguration.PreventDuplicates = true;
    config.SnackbarConfiguration.NewestOnTop = false;
    config.SnackbarConfiguration.ShowCloseIcon = true;
    config.SnackbarConfiguration.VisibleStateDuration = 10000;
    config.SnackbarConfiguration.HideTransitionDuration = 500;
    config.SnackbarConfiguration.ShowTransitionDuration = 500;
    config.SnackbarConfiguration.SnackbarVariant = Variant.Filled;
});

builder.Services.AddResponseCompression(opts =>
{
    opts.MimeTypes = ResponseCompressionDefaults.MimeTypes.Concat(
        ["application/octet-stream"]);
});

if (!builder.Environment.IsDevelopment())
{
    builder.Services.AddHttpsRedirection(options =>
    {
        options.RedirectStatusCode = (int)HttpStatusCode.PermanentRedirect;
    });
}

var app = builder.Build();

// Startup tasks
await app.MigrateDatabaseAsync();
await app.InitializeMetricsAsync();

// Middleware pipeline
if (app.Environment.IsProduction())
{
    app.Use((context, next) =>
    {
        context.Request.Scheme = "https";
        return next(context);
    });
}
app.UseForwardedHeaders();
app.UseResponseCompression();
app.UseMiddleware<BrowserClientIdCookieMiddleware>();

if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Error", createScopeForErrors: true);
    app.UseHsts();
}

var applicationUrls = builder.Configuration["Kestrel:Endpoints:Https:Url"];
if ((!string.IsNullOrEmpty(applicationUrls) && app.Environment.IsProduction()) || app.Environment.IsDevelopment())
{
    Log.Information("Using HTTPS redirection");
    app.UseHttpsRedirection();
}
else
{
    Log.Warning("HTTPS redirection is not enabled. Please ensure that the application is behind a reverse proxy that handles HTTPS.");
}

app.MapStaticAssets();
app.UseAntiforgery();
app.UseRateLimiter();

app.MapRazorComponents<App>()
    .AddInteractiveServerRenderMode()
    .WithStaticAssets();

app.MapHub<WHMapperNotificationHub>("/whmappernotificationhub");
app.MapGroup("/authentication").MapLoginAndLogout().RequireRateLimiting("auth");

await app.RunAsync();

```

## src/WHMapper/Models/Db/WHMap.cs
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Models/Db/WHMap.cs
Complete file, lines 1–39.
```text
﻿using System.ComponentModel.DataAnnotations;

namespace WHMapper.Models.Db
{
    public class WHMap
    {
        [Key]
        public int Id { get; set; }

        [Required]
        [StringLength(255, ErrorMessage = "Map name is too long.")]
        public string Name { get; set; } = string.Empty;

        /// <summary>
        /// The instance this map belongs to. Null for legacy maps (backward compatibility).
        /// </summary>
        public int? WHInstanceId { get; set; }

        public virtual ICollection<WHSystem> WHSystems { get; } = new HashSet<WHSystem>();
        public virtual ICollection<WHSystemLink> WHSystemLinks { get; } = new HashSet<WHSystemLink>();
        public virtual ICollection<WHMapAccess> WHMapAccesses { get; } = new HashSet<WHMapAccess>();

        [Obsolete("EF Requires it")]
        protected WHMap() { }

        public WHMap(string name)
        {
            Name = name;
        }

        public WHMap(string name, int whInstanceId)
        {
            Name = name;
            WHInstanceId = whInstanceId;
        }
    }
}


```

## src/WHMapper/Models/Db/WHSystem.cs
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Models/Db/WHSystem.cs
Complete file, lines 1–77.
```text
﻿
using System.ComponentModel.DataAnnotations;


namespace WHMapper.Models.Db
{
    public class WHSystem
    {
        [Key]
        public int Id { get; set; }

        [Required]
        public int WHMapId { get; set; }

        [Required]
        public int SoloarSystemId { get; set; } = -1;

        [Required, StringLength(255, ErrorMessage = "Map name is too long.")]
        public String Name { get; set; } = string.Empty;

        [StringLength(255, ErrorMessage = "Alternate name is too long.")]
        public String? AlternateName { get; set; } = null;

        public byte NameExtension { get; set; }

        [Required]
        public float SecurityStatus { get; set; }

        public virtual ICollection<WHSignature> WHSignatures { get; } = new HashSet<WHSignature>();

        public double PosX { get; set; } = 0.0;

        public double PosY { get; set; } = 0.0;

        public bool Locked { get; set; } = false;

        [Obsolete("EF Requires it")]
        protected WHSystem() { }
        public WHSystem(int whMapId, int solarSystemId, string name, float securityStatus, double posX, double posY)
        {
            WHMapId = whMapId;
            SoloarSystemId = solarSystemId;
            Name = name;
            SecurityStatus = securityStatus;
            PosX = posX;
            PosY = posY;
        }

        public WHSystem(int whMapId, int solarSystemId, string name, char nameExtension, float securityStatus, double posX, double posY)
        {
            WHMapId = whMapId;
            SoloarSystemId = solarSystemId;
            Name = name;
            NameExtension = Convert.ToByte(nameExtension);
            SecurityStatus = securityStatus;
            PosX = posX;
            PosY = posY;
        }


        public WHSystem(int whMapId, int solarSystemId, string name, float securityStatus) :
            this(whMapId, solarSystemId, name, securityStatus, 0, 0)
        {
        }

        public WHSystem(int whMapId, int solarSystemId, string name, char nameExtension, float securityStatus) :
            this(whMapId, solarSystemId, name, nameExtension, securityStatus, 0, 0)
        {

        }
        
        

    }
}


```

## src/WHMapper/Models/Db/WHInstance.cs
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Models/Db/WHInstance.cs
Complete file, lines 1–72.
```text
using System.ComponentModel.DataAnnotations;
using WHMapper.Models.Db.Enums;

namespace WHMapper.Models.Db
{
    /// <summary>
    /// Represents a WHMapper instance (tenant) that can be owned by a character, corporation, or alliance.
    /// Each instance has its own maps, access controls, and administrators.
    /// </summary>
    public class WHInstance
    {
        [Key]
        public int Id { get; set; }

        [Required]
        [StringLength(255, ErrorMessage = "Instance name is too long.")]
        public string Name { get; set; } = string.Empty;

        [StringLength(1000, ErrorMessage = "Description is too long.")]
        public string? Description { get; set; }

        /// <summary>
        /// The EVE entity ID that owns this instance (character, corporation, or alliance ID)
        /// </summary>
        [Required]
        public int OwnerEveEntityId { get; set; }

        [Required]
        public string OwnerEveEntityName { get; set; } = string.Empty;

        [Required]
        public WHAccessEntity OwnerType { get; set; }

        [Required]
        public int CreatorCharacterId { get; set; }

        [Required]
        public string CreatorCharacterName { get; set; } = string.Empty;

        public DateTime CreatedAt { get; set; } = DateTime.UtcNow;

        public bool IsActive { get; set; } = true;

        public virtual ICollection<WHMap> WHMaps { get; } = new HashSet<WHMap>();

        public virtual ICollection<WHInstanceAdmin> Administrators { get; } = new HashSet<WHInstanceAdmin>();

        public virtual ICollection<WHInstanceAccess> InstanceAccesses { get; } = new HashSet<WHInstanceAccess>();

        [Obsolete("EF Requires it")]
        protected WHInstance() { }

        public WHInstance(string name, int ownerEveEntityId, string ownerEveEntityName, WHAccessEntity ownerType, 
            int creatorCharacterId, string creatorCharacterName)
        {
            Name = name;
            OwnerEveEntityId = ownerEveEntityId;
            OwnerEveEntityName = ownerEveEntityName;
            OwnerType = ownerType;
            CreatorCharacterId = creatorCharacterId;
            CreatorCharacterName = creatorCharacterName;
        }

        public WHInstance(string name, int ownerEveEntityId, string ownerEveEntityName, WHAccessEntity ownerType,
            int creatorCharacterId, string creatorCharacterName, string? description)
            : this(name, ownerEveEntityId, ownerEveEntityName, ownerType, creatorCharacterId, creatorCharacterName)
        {
            Description = description;
        }
    }
}

```

## src/WHMapper/Extensions/MapperServiceExtensions.cs
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Extensions/MapperServiceExtensions.cs
Complete file, lines 1–68.
```text
using WHMapper.Models.DTO;
using WHMapper.Repositories.WHActivityLogs;
using WHMapper.Repositories.WHInstances;
using WHMapper.Repositories.WHJumpLogs;
using WHMapper.Repositories.WHMapAccesses;
using WHMapper.Repositories.WHMaps;
using WHMapper.Repositories.WHNotes;
using WHMapper.Repositories.WHSignatures;
using WHMapper.Repositories.WHSystemLinks;
using WHMapper.Repositories.WHSystems;
using WHMapper.Repositories.WHUserSettings;
using WHMapper.Services.BrowserClientIdProvider;
using WHMapper.Services.BrowserClientIdProvider.Extension;
using WHMapper.Services.EveMapper;
using WHMapper.Services.MapLayout;
using WHMapper.Services.WHActivityLogs;
using WHMapper.Services.WHColor;
using WHMapper.Services.WHSignature;
using WHMapper.Services.WHSignatures;
using WHMapper.Services.WHStatistics;
using WHMapper.Services.WHUserSettings;

namespace WHMapper.Extensions;

public static class MapperServiceExtensions
{
    public static IServiceCollection AddMapperServices(this IServiceCollection services)
    {
        // Repositories
        services.AddScoped<IWHMapRepository, WHMapRepository>();
        services.AddScoped<IWHSystemRepository, WHSystemRepository>();
        services.AddScoped<IWHSignatureRepository, WHSignatureRepository>();
        services.AddScoped<IWHSystemLinkRepository, WHSystemLinkRepository>();
        services.AddScoped<IWHNoteRepository, WHNoteRepository>();
        services.AddScoped<IWHRouteRepository, WHRouteRepository>();
        services.AddScoped<IWHJumpLogRepository, WHJumpLogRepository>();
        services.AddScoped<IWHInstanceRepository, WHInstanceRepository>();
        services.AddScoped<IWHMapAccessRepository, WHMapAccessRepository>();
        services.AddScoped<IWHUserSettingRepository, WHUserSettingRepository>();
        services.AddScoped<IWHActivityLogRepository, WHActivityLogRepository>();

        // Mapper services
        services.AddSingleton<IBrowserClientIdProvider, BrowserClientIdProvider>();
        services.AddScoped<ClientUID>();
        services.AddSingleton<IEveMapperUserManagementService, EveMapperUserManagementService>();
        services.AddScoped<IEveMapperService, EveMapperService>();
        services.AddScoped<IEveMapperCacheService, EveMapperCacheService>();
        services.AddScoped<IEveMapperAccessHelper, EveMapperAccessHelper>();
        services.AddScoped<IEveMapperInstanceService, EveMapperInstanceService>();
        services.AddScoped<IInstanceRegistrationHelper, InstanceRegistrationHelper>();
        services.AddScoped<IEveMapperTracker, EveMapperTracker>();
        services.AddScoped<IEveMapperSearch, EveMapperSearch>();
        services.AddScoped<IEveMapperHelper, EveMapperHelper>();
        services.AddScoped<IEveMapperRoutePlannerHelper, EveMapperRoutePlannerHelper>();
        services.AddScoped<IWHSignatureHelper, WHSignatureHelper>();
        services.AddScoped<IWHColorHelper, WHColorHelper>();
        services.AddScoped<IEveMapperRealTimeService, EveMapperRealTimeService>();
        services.AddScoped<IPasteServices, PasteServices>();
        services.AddScoped<IWHUserSettingService, WHUserSettingService>();
        services.AddScoped<IMapLayoutStorage, ProtectedLocalStorageMapLayoutStorage>();
        services.AddScoped<IMapLayoutService, MapLayoutService>();
        services.AddScoped<IWHActivityLogService, WHActivityLogService>();
        services.AddScoped<IWHStatisticsService, WHStatisticsService>();

        return services;
    }
}

```

## src/WHMapper/Extensions/DatabaseExtensions.cs
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/Extensions/DatabaseExtensions.cs
Complete file, lines 1–74.
```text
using Microsoft.EntityFrameworkCore;
using StackExchange.Redis;
using Microsoft.AspNetCore.DataProtection;
using WHMapper.Data;
using WHMapper.Services.Cache;
using WHMapper.Services.WHActivityLogs;

namespace WHMapper.Extensions;

public static class DatabaseExtensions
{
    public static IServiceCollection AddDatabaseServices(this IServiceCollection services, IConfiguration configuration)
    {
        services.AddDbContextFactory<WHMapperContext>(options =>
            options.UseNpgsql(configuration.GetConnectionString("DatabaseConnection"),
                o => o.UseQuerySplittingBehavior(QuerySplittingBehavior.SplitQuery))
            .UseQueryTrackingBehavior(QueryTrackingBehavior.NoTracking));

        var redisConnectionString = configuration.GetConnectionString("RedisConnection")
            ?? throw new InvalidOperationException("RedisConnection is not configured in the settings.");
        var redis = ConnectionMultiplexer.Connect(redisConnectionString);

        services.AddStackExchangeRedisCache(option =>
        {
            option.Configuration = configuration.GetConnectionString("RedisConnection");
            option.InstanceName = "WHMapper";
        });

        services.AddDataProtection()
            .SetApplicationName("WHMapper")
            .PersistKeysToStackExchangeRedis(redis, "DataProtection-Keys");

        services.AddScoped<ICacheService, CacheService>();

        return services;
    }

    public static async Task MigrateDatabaseAsync(this WebApplication app)
    {
        using var scope = app.Services.CreateScope();
        var logger = scope.ServiceProvider.GetRequiredService<ILogger<Program>>();
        var dbContext = scope.ServiceProvider.GetRequiredService<WHMapperContext>();

        int attempt = 0;
        while (!await dbContext.Database.CanConnectAsync() && attempt < 10)
        {
            attempt++;
            logger.LogWarning("Database not ready yet. Attempt {Attempt}/10", attempt);
            await Task.Delay(TimeSpan.FromSeconds(Math.Min(attempt * 2, 10)));
        }

        if (attempt >= 10)
        {
            logger.LogError("Database not ready after 10 attempts; exiting.");
            Environment.Exit(1);
        }

        if ((await dbContext.Database.GetPendingMigrationsAsync()).Any())
        {
            logger.LogInformation("Migrating database...");
            try
            {
                await dbContext.Database.MigrateAsync();
                logger.LogInformation("Database migrated successfully.");
            }
            catch (Exception ex)
            {
                logger.LogError(ex, "An error occurred while migrating the database.");
            }
        }
    }

}

```

