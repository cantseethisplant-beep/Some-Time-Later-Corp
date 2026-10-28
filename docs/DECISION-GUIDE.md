# Decision guide

The concept is useful when a corporation wants to compare software and coordinate hosting without giving managers unrestricted control of members' computers. It may be excessive for a corporation already satisfied with one manually maintained server or hosted services.

| Choice | Benefit | Cost or limitation | Evidence needed before deciding |
| --- | --- | --- | --- |
| Fixed stack (Idea 1) | Narrow setup and support scope | Less flexibility | Pilot requirements and administrator capacity |
| Deployment manager (Idea 2) | Reusable selection and assignment | Larger engineering and security scope | One complete deployment and recovery demonstration |
| Volunteer hardware | Uses offered resources | Availability, trust and withdrawal risk | Owner consent, limits and measured uptime |
| Trusted server or cloud | Clearer responsibility for sensitive data | Cost and operational responsibility | Budget, access controls and recovery exercise |
| Scheduled backup | Predictable recovery copies | Changes after the last good copy may be lost | Successful restore and measured data-loss window |
| Automatic movement | Less manual intervention | Stateful handover and duplicate writers are difficult | Application-specific fencing and failure tests |

## Catalogue entry requirements

Before calling an application supported, record its upstream repository and licence, reviewed immutable version, maintenance status, dependencies, permissions, storage model, measured resources, deployment steps, update and rollback procedure, and backup/restore evidence. A GitHub listing alone proves none of these.

Candidate names from the discussion are Wanderer, Alliance Auth, AA Buyback, Indy Hub and AA Structures. The exact buyback project and every candidate's current compatibility remain to be verified. CorpTools and other modules were discussed earlier; they are not mandatory additions.

## Questions still open

- Who operates and pays for the central controller?
- How are CEO identity, delegation, succession and emergency recovery established?
- Which workloads are acceptable on volunteer hosts, and which need trusted infrastructure?
- Which operating systems, deployment runtime and cloud provider should the pilot support?
- How are cloud spending limits enforced, and what happens if costs or capacity exceed the plan?
- What are the acceptable recovery time and data-loss targets for each application?
- How does a hardware owner withdraw, including when their machine is already offline?
- Who may read each type of corporation data, and how is consent documented?
- What licensing and distribution model should the eventual product use?

These questions should guide discovery. They are not permission to expand the build scope automatically.
