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
2. Review the prepared Windows XPIA alert and recorded prevention evidence.
3. Reconstruct Windows agent misalignment through incident and endpoint evidence.
4. Investigate the macOS MCP execution chain, subject to the readiness decision.
5. Compare evidence and confidence across the scenarios.
6. Optionally observe available Agent 365 investigation context.
7. Sign out and end the lab session.

The required path is Defender-led. Agent 365 extra credit does not require a separate administrative configuration exercise.

## Shared-state boundaries

Attendee accounts are individual; that does not imply devices or incidents are private to one attendee. The required activities are observational and must not alter shared incident, endpoint, identity, or policy state.

Isolation, remediation, Live Response, indicators, policy changes, and live response demonstrations are out of scope. Attendees do not install agents, onboard endpoints, provision Azure resources, configure Sentinel, or generate attacks.

## Readiness boundaries

- The October 30 macOS MCP report replaces the poisoned-brief content, not the owner readiness decision. Validate the exact replacement investigation with ordinary attendee accounts before delivery.
- Current configuration matching does not prove historical MCP invocation; a Blocked label does not prove completed discovery was prevented. Do not infer exfiltration from the scenario name.
- A working Windows agent entity does not establish macOS support or universal identity correlation.
- Source agent IDs, Entra agent IDs, and other identifiers must not be treated as interchangeable.
- Exact LAB683 links and evidence windows belong in controlled delivery material. Sanitized screenshots can be committed only after approval.

See the [content plan](content-plan.md) for remaining authoring and validation work.
