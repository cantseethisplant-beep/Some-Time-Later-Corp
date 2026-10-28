# Concept

## Two build ideas

Build Idea 1 is a fixed stack for one corporation. The discussion evolved from a large list to a shortlist of Wanderer, Alliance Auth, AA Buyback, Indy Hub and AA Structures. That shortlist is historical planning context and needs fresh technical review.

Build Idea 2 is the reusable product: a corporation hosting manager. It would present a curated catalogue of EVE community software, record member hardware offers and cloud resources, and help authorised managers assign applications to suitable hosts.

## Proposed journey

1. A corporation establishes its administration and recovery contacts.
2. Members offer a computer, virtual machine or limited resource allocation. They specify availability and acceptable workloads.
3. The CEO or appointed managers choose a reviewed application bundle and inspect its dependencies and resource requirements.
4. A manager proposes an assignment within the hardware owner's consent and limits.
5. The platform prepares and verifies a controlled deployment on an approved host.
6. Authorised users monitor health, request backups or use scheduled backups.
7. If hosting changes, the platform follows an application-specific movement or recovery procedure, recording what succeeded and what needs attention.

These steps describe intended behaviour, not available features.

## Hosting assignment

An assignment could describe its application version, dependencies, owner-approved host, resource limits, operating schedule, assignment expiry, movement window, backup schedule, destination, retention and recovery custodians. A backup button and a timed backup should use the same verified procedure.

For example, a trusted host might run an authentication bundle, with a maintenance window on Sunday, backups every six hours, and recovery access for the CEO and an appointed officer. These are illustrative settings, not universal defaults.

## Deployment choices

| Mode | Intended use | Main tradeoff |
| --- | --- | --- |
| Single host | One trusted corporation server | Simpler operation; host failure affects several services |
| Member distributed | Several members offer resources | More capacity; variable availability and more trust boundaries |
| Hybrid cloud | Member resources plus authorised cloud services | More options; cloud costs and account permissions need controls |

The controller needs reliable storage and hosting of its own. Existing workloads should be designed to keep running during controller outages, subject to their own dependencies; this must be tested.

## Dependency awareness

An application and its add-ons may form one deployment bundle. Ten volunteered hosts do not mean every add-on can run independently on a different machine. Placement must consider databases, background jobs, persistent data and application-specific requirements. The catalogue must distinguish standalone applications from add-ons and shared services.
