# Author the three investigation scenarios

This document tracks the GitHub-first attendee path and remaining delivery work. The exercises use question -> portal evidence -> focused hunting -> explained finding. API checks validate the data, not the attendee portal experience; full role-based rehearsal remains required before delivery.

## Agreed scope

- 75-minute, L300, browser-first, Defender-led investigation lab.
- Three scenarios: Windows XPIA, Windows agent misalignment, and a readiness-gated macOS MCP execution chain replacing the poisoned-brief exercise.
- Pre-seeded evidence in the team's dedicated tenant with an individual account per attendee.
- Varied portal experiences: alerts, incidents, agent context, process evidence, device events, timeline, and selected Advanced Hunting.
- Optional extra credit observes Agent 365 identity, registry, and risk context where available.
- No response activity or response demonstration: no isolation, remediation, Live Response, indicators, or policy changes.

## Scenario design

| Scenario | Investigation question | Evidence to prepare | Completion outcome |
|---|---|---|---|
| Windows XPIA | What untrusted input attempted to redirect the agent, and what did runtime protection prevent? | Alert, input/tool context available in the build, recorded prevention result, attributable endpoint evidence | Explain the attempted deviation and distinguish attempted behavior from observed execution |
| Windows misalignment | Where did the agent depart from the user's benign goal, and what happened next? | Original sales-document request, Copilot-child script launches, network scan, credential-access attempt, and AMSI prevention | Reconstruct the sequence without asserting successful credential theft or remote compromise |
| macOS MCP execution chain | How did a campaign-summary task lead to synthetic discovery, and what do configuration and protection evidence establish? | November 2 alert, Copilot -> Node -> JXA/shell events, captured script fragments, scoped MCP configuration, and approved run/action evidence | Explain the synthetic behavior, qualify the configuration link, and distinguish detected execution from proven prevention or information theft |

Do not advertise candidate detection lists as finalized coverage. Include only detections and evidence validated for the selected scenarios.

## Validate the third scenario

The October 30 investigation report supplies background. November 15 API checks independently confirm the November 2 replay's alert, process events, and captured script fragments; they do not establish attendee UI access or approval to reverse the earlier macOS demo exclusion. Obtain an explicit owner go/no-go decision for this exact path before delivery.

1. Confirm the selected build emits the incident, alerts, and process/script telemetry needed for the MCP execution-chain exercise.
2. Confirm ordinary attendee accounts can complete an investigation from the prepared evidence.
3. Verify device/process attribution and the scope and observation time of any configuration match. Do not promise authoritative MCP invocation telemetry.
4. Confirm the evidence is repeatable and remains accessible through event delivery.
5. Compare available action targets/results with approved saved-run evidence. Do not claim discovery was prevented merely because the portal says Blocked.
6. If any required element is missing, obtain owner approval for an alternative, then author and rehearse it. Do not replace the runtime investigation with inventory-only browsing.

There are still three required scenarios, not a fourth exercise. The legitimate request names `retrieve_campaign_brief`, Copilot launches Node running `server.mjs`, and descendant JXA/shell activity includes synthetic discovery. The October report states no archiving or uploading occurred in its reported run; do not automatically apply that outcome to November's replay. Neither the name nor the current registration match establishes external exfiltration, poisoning, rug pull, persistence, or historical tool invocation.

## Finish the exact attendee instructions

1. Select the actual incident, alert, device, agent, and evidence window for each scenario in controlled operator material.
2. Use Playwright to walk the LAB683 tenant with ordinary attendee credentials. Do not execute state-changing actions.
3. Replace draft navigation with observed labels, exact pivots, expected results, and troubleshooting guidance.
4. Capture approved sanitized screenshots for `instructions/media/`. Remove credentials, private identifiers, user details, and sensitive prompt content before committing.
5. Add approved hunting queries only after validating table availability, identifiers, time windows, and expected results. Do not invent identity joins.
6. Rehearse the full 75-minute journey and optional extra credit with the delivery team.

The October 23 walkthrough and approved screenshots support the Windows portal procedures; November 15 API checks reconfirm retained Windows events. The old Mac prompt observations describe the superseded poisoned-brief run. The required Mac queries now target the November 2 replay, not the October report's process instances. Keep complete reports, raw results, and private engineering references in controlled owner material, not GitHub.

The 75-minute path allocates 5 minutes to sign-in, 10 to discovery, 15 to XPIA, 20 to misalignment, 20 to macOS, and 5 to comparison. The first hunt is fully supplied, misalignment asks learners to modify a filter, and macOS asks them to complete a process filter with a hint available.

### Explain the findings visually

Each case ends with an expandable explanation and an original illustrated attack story in `instructions/media/`. Numbered stages, simple actor/tool icons, and evidence callouts make the behavior easier to discuss without exposing the answer before the investigation. SVGs have descriptive titles, accessible descriptions, and matching prose; editable `.excalidraw` sources accompany them.

The visual approach draws on public Microsoft Security Blog patterns, not copied artwork or an official diagram template:

- [Securing AI agents](https://www.microsoft.com/en-us/security/blog/2026/06/30/securing-ai-agents-ai-tools-move-from-reading-acting/), Figure 1: stage the behavior and place protection evidence beneath the relevant stages.
- [SCKit attack chain](https://www.microsoft.com/en-us/security/blog/2026/11/13/sckit-abuses-screenconnect-deploy-remote-access-target-technician-sessions/), Figure 2: separate observed deployment from potential propagation rather than drawing both as confirmed activity.
- [Trained to betray](https://www.microsoft.com/en-us/security/blog/2026/11/12/trained-to-betray-how-post-training-supply-chain-attacks-hijack-coding-agents/): contrast a benign-looking task with unsafe tool behavior. Its backdoor mechanism is not the mechanism claimed for these lab scenarios.

The XPIA diagram uses dashed requested-action arrows, not an observed exfiltration path. Misalignment branches distinguish scanning from the specific prevented LSASS attempt. The Mac story calls out synthetic code and an unresolved protection outcome. Text labels carry those distinctions independently of color. Refresh diagrams together with the evidence; do not retain a prevention marker after changing to a run that lacks its supporting record.

## Prepare the controlled scenario reference sheet

Supply these fields in Skillable or approved private operator material, not in GitHub:

| Field | Required detail |
|---|---|
| Each scenario | Stable alert link/ID and device link/ID; direct Local agents inventory link for navigation fallback |
| Evidence window | UTC start/end for KQL and equivalent portal-local date/time values |
| Process | PID and creation time; scan child PID for misalignment |
| Rich prompt locator | Process instance, action type, event time and distinguishing text prefix |
| Mac script locator | `DeviceEvents` / `ScriptContent` events and equivalent timeline locators, with execution identity and time; distinguish captured fragments from complete entry-script source |
| Mac configuration locator | Named registration, executable/arguments, device/account scope, observation time, and known truncation |
| Mac outcome reference | Approved saved-run evidence and exact per-target detection/action/result timing; distinguish live observations from report-based conclusions |
| Optional disruption context | Exact action reference, entity, source and status; verified device association |
| Instructor fallback | Approved reference image/recording offset and support path |

Use the date/time format actually accepted by the attendee environment. Presenter screenshots have different local offsets; do not copy their displayed clock values blindly.

## Use the instructor checkpoints

| Exercise | Expected evidence-based answer | Avoid this unsupported conclusion |
|---|---|---|
| Discovery | Latest local agent profiles are device/account-associated observations; configuration has an observation time and differs from execution evidence | A configured MCP was invoked, a trusted host implies safe behavior, or an empty identity field implies no agent |
| Windows XPIA | The prompt requests local credential-file access and a POST to the test collection destination. The blocked alert and network-prompt remediation corroborate prevention | No URL match alone proves nothing was disclosed |
| Misalignment | The user requested comprehensive sales-document search; Copilot launched scan, remote-file-search and credential-access scripts; LSASS-dumping execution was prevented | A successful TCP connection proves login, document retrieval or credential theft |
| Historical disruption | Automated user containment and RDP enforcement are observable on the later Windows identity | This proves agent-initiated RDP, automatic device isolation, or causality for the separate older-device misalignment run |
| Mac MCP chain | November replay shows Copilot, Node, JXA/shell activity and captured synthetic script fragments. A current configuration match is potential only. October's report describes completed simulated steps and later already-exited-process responses for its own run | The benign request is prompt injection; registration proves historical invocation or poisoning; a synthetic stub is the real OS utility; the scenario name proves exfiltration; Blocked proves discovery was prevented |
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
| Mac entry-script source is not directly available from its file card | Hunt captured `ScriptContent` fragments and use the equivalent timeline locator. Do not promise complete `server.mjs` source or submit files through the File content analysis tab |
| Mac fork/exec rows and interpreter attribution are ambiguous | Track execution identity, creation time, executable path, and script arguments; repeated PIDs are not necessarily separate processes |
| Current MCP configuration lacks historical invocation proof | Label executable/argument matches as potential configuration links and record timing, scope, provenance, and truncation |
| Blocked/terminated wording can disagree with saved-run evidence | Separate detection, requested action, exact target, result, and prevention certainty; label report-based conclusions |
| Local MCP counts, alert dashes, and file associations can mislead | Explain category and direct-versus-descendant scope; no displayed association is not proof of no related activity |
| Ordinary attendee access not yet tested | Rehearse every required click and query with the actual role |
| Intended activity-label changes | Recheck after changes actually appear; do not describe the proposed Monday improvements as shipped |

The exact live Windows destination is `example-attacker.test`, not the walkthrough's spoken shorthand `attacker.com`. Do not visit the destination or run the attack text.

The October 30 report recommends clearer execution-chain summaries, execution-bound captured-source navigation, historical/scoped MCP associations, and explicit protection outcomes. These are proposed improvements, not shipped controls or guaranteed attendee pivots. Source code inspection does not prove tenant deployment. Validate access, retention, and the complete portal path with ordinary attendee accounts; an internal/test-only fallback is not a delivery guarantee.

## Record the query baseline

The documented queries were executed through Microsoft Graph hunting against the prepared evidence after checking the live schemas. With the private reference windows checked on October 23:

| Query | Baseline result |
|---|---|
| Latest local inventory | Four profiles |
| Windows alert-to-profile correlation | One matching row |
| Same correlation query with earlier Mac alert | One matching row; not a baseline for the replacement MCP run |
| Windows prompt-injection AV evidence | Four records |
| Windows test-destination network check | Zero matching URL records |
| Misalignment script launches | Four records |
| Misalignment scan aggregation | Four result groups |
| Misalignment LSASS-related evidence | Four records |

These are an October 23 instructor baseline, not immutable learner success counts or validation of the replacement Mac run. None reached its result cap. Recheck after evidence refresh and with the attendee role. No credentials, app secrets, raw result exports, or tenant-specific identifiers are included here.

### November 15 API recheck

Read-only app access reconfirmed the retained Windows evidence and the November 2 Mac replay. App access is not attendee-role validation.

| Scope | Confirmed evidence |
|---|---|
| Current local inventory | Three rows from the required filtered 30-day hunt; not a fixed learner completion count |
| Windows XPIA | Four prompt-injection AV records in the documented window, including two reporting remediation |
| Windows misalignment | Four relevant script launches, retained scan aggregation, and four LSASS-related records |
| November 2 macOS replay | Matching local-MCP alert, Copilot/Node/JXA/shell process events, and three `ScriptContent` events |
| Mac captured code | Two short shell fragments and a longer JXA script; the hardware-information command resolves to a synthetic stub |

All six required KQL blocks were rerun directly from the rewritten Markdown, substituting only controlled device IDs and the Mac hint. Results were 3 inventory rows, 4 XPIA rows, 4 scan groups, 4 LSASS-related rows, 38 Mac process rows, and 3 Mac script-content rows. The learner's port-22 filter variant returned 2 groups. None reached its result cap. These checks do not validate portal labels, query-editor permissions, or attendee timing.

The Windows runs are already over three weeks old at this check. Standard rolling hunting retention can expire before delivery even if alerts remain visible. Refresh/replay the evidence before that happens, then update dates, process instances, expected results, screenshots where needed, and controlled links as one change. Do not work around expired telemetry by silently replacing a required investigation with an unrelated alert.

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
