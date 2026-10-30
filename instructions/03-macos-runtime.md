---
title: Investigate a macOS MCP execution chain in Microsoft Defender
description: Trace a Copilot-launched Node script through JXA and synthetic discovery. Qualify MCP configuration links and distinguish detection from prevention.
author: j0shbregman
ms.author: j0shbregman
ms.service: microsoft-defender-xdr
ms.topic: how-to
ms.custom: msecd-doc-authoring-1032
ms.date: 10/30/2026
ai-usage: ai-generated
#customer intent: As a SOC analyst, I want to investigate a macOS execution chain so that I can distinguish observed behavior, possible MCP associations, and protection outcomes.
---

# Investigate a macOS MCP execution chain in Microsoft Defender

Use Microsoft Defender to investigate the prepared `northstar-campaign-assets-infosteal` scenario. A legitimate campaign-brief request leads to a Copilot-launched Node script and descendant discovery activity. The scenario name does not prove information theft: the supplied run performed synthetic discovery, with no archiving or uploading. Allow 15 minutes.

## Prerequisites

- Complete [Windows agent misalignment](02-agent-misalignment.md).
- Open the **macOS MCP execution chain** reference-sheet row with its incident, alerts, device, process instances, evidence window, and approved run-evidence reference.
- Use a browser; you do not need a Mac or local agent installation.

**Tester draft:** This replaces the earlier poisoned-brief exercise using the October 30 investigation report. The report's portal captures and saved-run interpretation are reference evidence, not a fresh attendee-role validation. Owner approval for macOS delivery, ordinary-account access, evidence retention, and the complete 15-minute journey remain required.

## Identify the task and execution chain

Start from the supplied incident and establish what the user asked the agent to do.

1. Open the incident from the controlled reference sheet, then open its supplied Mac alert.
2. Confirm the incident, alert, device, and time window. A matching display name alone is not enough.
3. Open **Process tree** and locate **GitHub Copilot CLI** using the supplied PID and creation time.
4. Inspect the captured command line. The legitimate request is to use the named MCP server's `retrieve_campaign_brief` tool to retrieve the latest Zava campaign brief and summarize its deliverables.
5. Follow the chain from `copilot` to `node` running `server.mjs`, then to `osascript` with JavaScript for Automation (JXA) and its shell descendants.
6. Record the process IDs, creation times, executable paths, and script arguments. The source run shows Copilot PID 7536 and Node PID 7585; use refreshed reference values if the lab team supplies a newer run.

**Expected result:** You can explain the observed Copilot -> Node -> JXA -> shell chain separately from the authorized campaign-summary task. The benign user request is not prompt injection, and this evidence does not establish a poisoned tool response or MCP rug pull.

The tree can show repeated PIDs or changing executable labels across macOS fork/exec transitions. Do not count each displayed row as an independent process or mistake the launcher for the executed interpreter.

## Inspect the script and discovery evidence

Distinguish a script reference from source captured for that execution.

1. Expand the Node process. Review **Command line**, **Image file path**, and the **Referenced in commandline** card for `server.mjs`.
2. Record the script path, hash, and timestamps where available. Interpreter metadata describes Node, not the contents or provenance of `server.mjs`.
3. Open the supplied device timeline and set **Time range** > **Custom range** to the reference sheet's portal-local window.
4. Use the supplied locator for the **Endpoint Script Content** event. Inspect available captured script content and its relationship to the execution. If the event is unavailable, record that limitation and use only the approved, labeled reference evidence.
5. Follow the JXA and shell events. Compare resolved executable paths with command names before describing what ran.

**Expected result:** The report describes synthetic discovery. In this run, the command named `system_profiler` is a generated synthetic stub; its name alone does not establish execution of the real operating-system utility.

The file page's **File content** tab required an analysis submission in the inspected experience; it is not an execution-time source viewer. Do not submit a file or run analysis for this lab. Script content exists in a separate timeline event, so an unavailable file-tab view does not mean source is absent everywhere.

## Qualify the MCP association

Compare configuration with execution without treating configuration as invocation telemetry.

1. Open **Assets** > **AI agents** > **Local agents**, or use the supplied direct inventory link if the default view fails.
2. Select **GitHub Copilot CLI** on the supplied Mac device and account.
3. Expand **Local MCP servers**, where available, and locate the scenario's named registration.
4. Compare the configured executable and script arguments with the Node process. Record the device/account scope, observation time, and any truncation or missing values.
5. State whether you found a potential configuration link. If exact values cannot be inspected, leave the match unestablished.

**Expected result:** A current executable-and-argument match supports a **potential configuration link**, not proof that this configuration was consumed historically or that the named tool was invoked. The request names a tool, but authoritative MCP invocation telemetry is not established by this exercise.

Different **MCP servers** and **Local MCP servers** counts describe different categories; zero in one does not negate entries in the other. A dash in an alerts field, a low agent-risk label, or a trusted host does not establish absence of suspicious descendant activity.

## Distinguish detection, remediation, and prevention

Record what each evidence source establishes rather than adopting the alert's outcome label.

1. Record the alert's displayed detection and protection status, including **Blocked** where shown.
2. Review available action details. Separate the detection time, requested action, exact process/file target, actual result, and whether prevention is demonstrated. Mark unavailable values as unknown.
3. Compare the approved run-evidence reference. The October 30 report says saved execution logs show the simulated steps completed and later termination responses encountered already-exited processes. Label this as report-based unless you can inspect the supplied underlying logs.
4. Separate discovery from data access, collection, and transfer. The report states that this run performed no archiving or uploading; it does not demonstrate external exfiltration.
5. Do not infer that terminating a descendant stopped Copilot, disabled its MCP registration, or prevented a later launch.

**Expected result:** Detection is observed, but the **Blocked** label alone does not prove the synthetic discovery was prevented. If the live view does not resolve the action/result discrepancy, keep prevention unestablished. Do not use missing network rows alone to prove absence of transfer.

## Complete the investigation

Explain the chain and the limits of the available evidence.

1. State the legitimate campaign-summary task and observed Copilot -> Node -> JXA/shell activity.
2. Cite the process and script evidence, identifying live observations separately from approved reference material.
3. Qualify the current MCP configuration match; do not claim historical invocation, poisoning, rug pull, or persistence.
4. Distinguish synthetic discovery, unestablished data-access/collection stages, no archiving/uploading in the reported run, and the unresolved prevention outcome.

You are finished when those conclusions are evidence-based. No response action, file submission, Mac provisioning, or attack execution is required.

## Next step

> [!div class="nextstepaction"]
> [Compare your findings and finish the lab](README.md#compare-your-findings)

## Related content

- [Observe Agent 365 investigation context](optional-agent-365.md)
