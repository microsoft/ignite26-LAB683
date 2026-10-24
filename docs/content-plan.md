# Author the three investigation scenarios

This document tracks the tester draft and its remaining delivery work. Attendee pages now include concrete procedures, screenshots, hunting queries, and completion checks; they are not yet a fully rehearsed event manual.

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
| Windows misalignment | Where did the agent depart from the user's benign goal, and what happened next? | Original sales-document request, Copilot-child script launches, network scan, credential-access attempt, and AMSI prevention | Reconstruct the sequence without asserting successful credential theft or remote compromise |
| macOS runtime/XPIA | How does a poisoned brief attempt to override confidentiality, and what outcome is demonstrated? | Mac alert, source-agent correlation, user request, and synthetic tampered campaign brief | Distinguish Defender detection from the model's reported non-disclosure; require response evidence for the latter |

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

The October 23 recorded walkthrough, downloaded screenshots, and LAB683 API results now supply the scenario evidence. A current administrative browser session also verified the Local agents inventory and details pane, prompt-node selection, the Mac user request and poisoned brief, the exact Windows credential-disclosure prompt, and the alert-to-timeline controls. This does not validate ordinary attendee permissions, every timeline locator, or registry navigation.

## Prepare the controlled scenario reference sheet

Supply these fields in Skillable or approved private operator material, not in GitHub:

| Field | Required detail |
|---|---|
| Each scenario | Stable alert link/ID and device link/ID; direct Local agents inventory link for navigation fallback |
| Evidence window | UTC start/end for KQL and equivalent portal-local date/time values |
| Process | PID and creation time; scan child PID for misalignment |
| Rich prompt locator | Process instance, action type, event time and distinguishing text prefix |
| Response locator | Mac response event or approved labeled walkthrough reference |
| Optional disruption context | Exact action reference, entity, source and status; verified device association |
| Instructor fallback | Approved reference image/recording offset and support path |

Use the date/time format actually accepted by the attendee environment. Presenter screenshots have different local offsets; do not copy their displayed clock values blindly.

## Use the instructor checkpoints

| Exercise | Expected evidence-based answer | Avoid this unsupported conclusion |
|---|---|---|
| Discovery | Local agent profiles are device/account-associated observations; source identity links alert evidence to the profile GUID | A configured MCP was invoked, a trusted host implies safe behavior, or an empty identity field implies no agent |
| Windows XPIA | The prompt requests local credential-file access and a POST to the test collection destination. The blocked alert and network-prompt remediation corroborate prevention | No URL match alone proves nothing was disclosed |
| Misalignment | The user requested comprehensive sales-document search; Copilot launched scan, remote-file-search and credential-access scripts; LSASS-dumping execution was prevented | A successful TCP connection proves login, document retrieval or credential theft |
| Historical disruption | Automated user containment and RDP enforcement are observable on the later Windows identity | This proves agent-initiated RDP, automatic device isolation, or causality for the separate older-device misalignment run |
| Mac XPIA | The synthetic brief claims administrative authority and asks for internal cost/margin disclosure; Defender detection is observed | Defender blocked the request because the model reportedly did not disclose costs |
| Agent 365 extra credit | Matching profiles currently lack Entra identity values; registry context requires a separately verified pivot | All local agents already have a usable Agent 365 registry/identity path |

The Windows runs reuse a VM display name after a snapshot revert, as explained by the presenter. Their different device IDs remain distinct query scopes.

## Track current experience gaps

| Gap | Required fallback or delivery check |
|---|---|
| Alert heading can disagree with the selected XPIA ID | Match the exact ID and blocked-injection story node; document the mismatch for testers |
| Default Agents inventory fails before tabs load | Supply the verified direct Local agents link; use hunting as a labeled fallback, not proof the UI step succeeded |
| Repeated generic prompt-call labels | Use the controlled composite locator and text prefix, not row number or icon alone |
| Rich prompts absent from retrieved hunting rows | Use portal detail panes; do not promise KQL conversation reconstruction |
| Agent-page map or alert tab fails to load | Keep direct alert and device routes available |
| Mac response pane not independently rehearsed | Label model-outcome reference evidence; require live detection only until verified |
| Ordinary attendee access not yet tested | Rehearse every required click and query with the actual role |
| Intended activity-label changes | Recheck after changes actually appear; do not describe the proposed Monday improvements as shipped |

The exact live Windows destination is `example-attacker.test`, not the walkthrough's spoken shorthand `attacker.com`. Do not visit the destination or run the attack text.

## Record the query baseline

The documented queries were executed through Microsoft Graph hunting against the prepared evidence after checking the live schemas. With the private reference windows checked on October 23:

| Query | Baseline result |
|---|---|
| Latest local inventory | Four profiles |
| Windows alert-to-profile correlation | One matching row |
| Same correlation query with Mac alert | One matching row |
| Windows prompt-injection AV evidence | Four records |
| Windows test-destination network check | Zero matching URL records |
| Misalignment script launches | Four records |
| Misalignment scan aggregation | Four result groups |
| Misalignment LSASS-related evidence | Four records |

These are an instructor baseline, not immutable learner success counts. None reached its result cap. Recheck after evidence refresh and with the attendee role. No credentials, app secrets, raw result exports, or tenant-specific identifiers are included here.

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
