# Oracle and Cloudflare — documented option evidence

Observed: 2 November 2026. Recheck before provisioning; no owner account/VM/domain inspected or configured. Candidate deployment evidence only, no server access or paid service.

- OCI-01: Oracle's Always Free resource guide currently describes A1 as 1,500 OCPU-hours/9,000 GB-hours monthly (2 OCPUs/12 GB total), home-region allocation, possible capacity shortage and idle-instance reclamation. Source: https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm
- OCI-02: Oracle distinguishes temporary trial credits from Always Free. Signup commonly requires phone/card; the Free Tier guide says charging requires upgrading and warns that excess trial A1 capacity may be removed after trial. Source: https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier.htm
- CF-01: Tunnel is documented as outbound-only and available on all plans; setup requires an account/domain and origin internet access, including port 7844. Sources: https://developers.cloudflare.com/tunnel/ and https://developers.cloudflare.com/tunnel/get-started/
- CF-02: WebSockets on all plans and SignalR are documented; WAF inspection is for the opening handshake, not continuing frames. Source: https://developers.cloudflare.com/network/websockets/
- MS-01: .NET 10 proxy guidance documents explicit trusted forwarded-header configuration outside IIS. Source: https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/proxy-load-balancer?view=aspnetcore-10.0

Planning inference: a single qualified Oracle VM behind a Cloudflare named tunnel is a plausible pilot origin, with PostgreSQL/Redis private and an independently recoverable encrypted backup. This inference is not measured capacity, an account entitlement, an SLA or a zero-cost guarantee. Architecture-specific images, quotas, egress/storage/backup costs, hostname/SSO/SignalR and recovery must be qualified. No automatic paid upgrade or artificial workload to evade reclamation is proposed.
