# Lab architecture

LAB683 uses browser-based investigations of pre-seeded evidence in the team's dedicated Microsoft Defender lab tenant. Each attendee receives an individual user account. Devices and scenario evidence are prepared by the lab team, not provisioned or attacked by attendees.

This delivery model supersedes the earlier per-learner Windows VM and live-attack scaffold.

## Components and ownership

| Component | Purpose | Owner responsibility |
|---|---|---|
| Skillable experience | Delivers instructions, browser access, and intended secure account assignment | Validate account delivery, sign-in, session cleanup, and capacity |
| Dedicated lab tenant | Hosts the shared investigation experience | Prepare access, permissions, evidence retention, and refresh |
| Prepared Windows endpoints | Supply XPIA and misalignment evidence | Generate approved evidence before delivery |
| Prepared macOS endpoint | Supplies the replacement MCP execution-chain investigation, subject to owner approval | Validate the exact build, process/script evidence, configuration scope, and portal journey |
| Microsoft Defender | Presents alerts, incidents, device events, timelines, agent context, and hunting | Verify each scenario with an ordinary attendee account |
| Agent 365 context | Adds optional identity, registry, and risk observations | Validate each supported pivot without changing policy |
| GitHub repository | Holds reusable instructions and approved sanitized assets | Keep credentials, private identifiers, and raw telemetry out of commits |

## Required investigation flow

1. Launch the supplied lab experience and sign in with an assigned account.
2. Discover local agent instances in the portal and compare their inventory observations with Advanced Hunting.
3. Investigate Windows XPIA in the portal and corroborate the protection evidence with a supplied hunt.
4. Reconstruct Windows misalignment, then measure scanning and inspect credential-access protection with focused hunts.
5. Trace the macOS MCP execution chain and inspect captured script content, subject to the readiness decision.
6. Compare evidence and confidence across the scenarios.
7. Optionally observe available Agent 365 investigation context.
8. Sign out and end the lab session.

Every investigation follows question -> portal evidence -> focused hunt -> explained finding. Query scaffolding decreases across the three scenarios. The required path is Defender-led. Agent 365 extra credit does not require a separate administrative configuration exercise.

## Shared-state boundaries

Attendee accounts are individual; that does not imply devices or incidents are private to one attendee. The required activities are observational and must not alter shared incident, endpoint, identity, or policy state.

Isolation, remediation, Live Response, indicators, policy changes, and live response demonstrations are out of scope. Attendees do not install agents, onboard endpoints, provision Azure resources, configure Sentinel, or generate attacks.

## Readiness boundaries

- The macOS exercise uses the November 2 replay, independently checked through read-only hunting on November 15. The October 30 report is background, not proof of the replay's outcome or ordinary attendee access. Validate the exact replacement investigation with attendee accounts before delivery.
- Current configuration matching does not prove historical MCP invocation; a Blocked label does not prove completed discovery was prevented. Do not infer exfiltration from the scenario name.
- A working Windows agent entity does not establish macOS support or universal identity correlation.
- Source agent IDs, Entra agent IDs, and other identifiers must not be treated as interchangeable.
- Tenant-specific links and identifiers belong in controlled delivery material. Public pages provide UTC windows and process locators; learners copy device IDs from their selected case. Refresh those references together when replaying evidence. Sanitized screenshots can be committed only after approval.

See the [content plan](content-plan.md) for remaining authoring and validation work.
