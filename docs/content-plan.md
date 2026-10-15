# Author the three investigation scenarios

This review draft records the agreed LAB683 scope. It is suitable for Research and PMM review, but not yet a delivery-ready attendee manual.

## Agreed scope

- 75-minute, L300, browser-first, Defender-led investigation lab.
- Three scenarios: Windows XPIA, Windows agent misalignment, and readiness-gated macOS runtime/XPIA.
- Pre-seeded evidence in the team's dedicated tenant with an individual account per attendee.
- Varied portal experiences: alerts, incidents, agent context, process evidence, device events, timeline, and selected Advanced Hunting.
- Optional extra credit observes Agent 365 identity, registry, and risk context where available.
- No response activity or response demonstration: no isolation, remediation, Live Response, indicators, or policy changes.

## Scenario design

| Scenario | Investigation question | Evidence to prepare | Completion outcome |
|---|---|---|---|
| Windows XPIA | What untrusted input attempted to redirect the agent, and what did runtime protection prevent? | Alert, input/tool context available in the build, recorded prevention result, attributable endpoint evidence | Explain the attempted deviation and distinguish attempted behavior from observed execution |
| Windows misalignment | Where did the agent depart from the user's benign goal, and what happened next? | Approved goal context, incident/alert, process chain, device events and timeline; discovery, credential access, or lateral-movement evidence only where actually present | Reconstruct the sequence and support agent attribution and impact with evidence |
| macOS runtime/XPIA | What can the macOS runtime investigation establish, and how does it compare with Windows? | Actual Mac runtime alert and supporting events; agent entity only if supported by the chosen build | State the observed outcome and explain evidence or platform gaps without assuming parity |

Do not advertise candidate detection lists as finalized coverage. Include only detections and evidence validated for the selected scenarios.

## Validate the third scenario

Make the macOS go/no-go decision by **October 30, 2026**.

1. Confirm the selected build emits the required runtime alert and telemetry.
2. Confirm ordinary attendee accounts can complete an investigation from the prepared evidence.
3. Verify device attribution and any claimed agent-entity linkage.
4. Confirm the evidence is repeatable and remains accessible through event delivery.
5. If any required element is missing, publish MCP/tool-chain compromise as the third scenario instead. Do not replace the runtime investigation with inventory-only browsing.

The fallback remains a planning option, not a fourth required scenario. Its final instructions must be authored and rehearsed before it replaces the macOS path.

## Finish the exact attendee instructions

1. Select the actual incident, alert, device, agent, and evidence window for each scenario in controlled operator material.
2. Use Playwright to walk the LAB683 tenant with ordinary attendee credentials. Do not execute state-changing actions.
3. Replace draft navigation with observed labels, exact pivots, expected results, and troubleshooting guidance.
4. Capture approved sanitized screenshots for `instructions/media/`. Remove credentials, private identifiers, user details, and sensitive prompt content before committing.
5. Add approved hunting queries only after validating table availability, identifiers, time windows, and expected results. Do not invent identity joins.
6. Rehearse the full 75-minute journey and optional extra credit with the delivery team.

Read-only exploration in the Zava demo verified an inventory-to-local-agent Overview journey, including source/Entra identity fields and a Go hunt entry point. That is a reference, not validation of LAB683 evidence, macOS support, every agent-page tab, or an Agent 365 registry pivot.

## Review responsibilities

| Review area | Required confirmation |
|---|---|
| Research | Actual detections, causal evidence, prevention result, and claim accuracy |
| PMM | Scenario framing, product terminology, and available-versus-preview distinctions |
| macOS engineering | Build and end-to-end runtime evidence at the readiness gate |
| Tenant and Skillable owners | Individual account delivery, RBAC, capacity, retention, and session cleanup |
| Content owner | Exact steps, sanitized assets, timing, and final third-scenario selection |

Do not publish internal chat links, customer names, test-tenant identifiers, or private source-code references in attendee material.

## Related content

- [Attendee path](../instructions/README.md)
- [Discover local AI agents](https://learn.microsoft.com/en-us/defender-endpoint/discover-local-ai-agents)
- [AI agent inventory](https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/ai-agent-inventory)
