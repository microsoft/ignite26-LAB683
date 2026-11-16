---
title: Investigate code execution behind a macOS MCP tool
description: Trace a campaign-summary task through local MCP process activity, hunt for captured script content, and assess the protection evidence.
author: j0shbregman
ms.author: j0shbregman
ms.service: microsoft-defender-xdr
ms.topic: how-to
ms.date: 11/15/2026
ai-usage: ai-generated
---

# Investigate code execution behind a macOS MCP tool

A user asks an agent to retrieve a campaign brief and summarize its deliverables. The agent uses a local Model Context Protocol (MCP) server: a tool integration that can run code on the device.

What happens behind that tool request? In this case, a Node process leads to JavaScript for Automation (JXA) and shell activity. Investigate the execution rather than assuming that a familiar agent or a configured tool is safe.

**Your mission:** Trace the execution chain, use hunting to inspect the script evidence, and distinguish detected activity from proven prevention. Allow 20 minutes. You need only your browser, not a Mac.

## Open the case

1. Open the lab team's Mac MCP alert link, or locate **Suspected information theft by AI Agent through local MCP** in **Incidents & alerts** > **Alerts** around **November 2, 2026, 18:35 UTC**.
2. Review **Alert details**, the affected device, and **Process tree**.
3. Open the affected device in another tab and copy its device ID for the hunts.

| Reference | Documented run |
|---|---|
| Investigation window | November 2, 2026, 18:34-18:37 UTC |
| Starting agent | `copilot`, PID 24186, created 18:35:15 UTC |
| Node entry process | PID 24259, created 18:35:19 UTC |

These are references for the November 2 run, not the older October Mac prompt-injection example. If the lab team refreshes the scenario, use its replacement values together.

## Investigate: what was the intended task?

1. In **Process tree**, locate the starting Copilot instance by PID and creation time.
2. Inspect its command line. Identify the request to call `retrieve_campaign_brief` once and summarize the campaign deliverables and milestones.
3. Record what the user asked for before investigating the descendants.
4. Follow the tree to Node running `server.mjs`, then `osascript` using JavaScript, and its shell descendants.
5. Record one action that needs explanation in the context of a campaign-summary task.

The request naming a tool is not itself a malicious prompt. An alert title is a starting hypothesis, not proof that information was stolen.

macOS fork/exec transitions can show the same PID with different executable labels. Compare times, paths, command lines, and the portal tree; do not assume every row is an independent process or that parent PID fields alone reconstruct the whole chain.

## Investigate: is the execution related to a configured tool?

1. Open **Assets** > **AI agents** > **Local agents** and select GitHub Copilot CLI on this case's device and account.
2. Inspect **Local MCP servers**, where available.
3. Compare the configured executable and script arguments with the Node command line you observed. Record whether the values match, differ, or cannot be inspected.

A matching current configuration supports a possible relationship. It does not independently prove which registration was used at the historical execution time. If the pane is unavailable, record that limitation and continue with the process evidence.

## Hunt: reconstruct the activity around the alert

**Question: Which process events support the chain you saw in the portal?**

1. Open **Advanced hunting** > **New query**, replace `<MAC_DEVICE_ID>`, and include the full investigation window in the time picker.
2. Complete the filename list by replacing `<JXA_EXECUTABLE>` with the executable you identified between Node and the shell.
3. Run the query. If you need help, open the hint below.

```kusto
let deviceId = "<MAC_DEVICE_ID>";
let startTime = datetime(2026-11-02T18:34:00Z);
let endTime = datetime(2026-11-02T18:37:00Z);
DeviceProcessEvents
| where Timestamp between (startTime .. endTime)
| where DeviceId == deviceId
| where FileName in~ ("copilot", "node", "<JXA_EXECUTABLE>", "sh", "bash", "zsh")
| project Timestamp, FileName, ProcessId, ProcessCreationTime,
    InitiatingProcessFileName, InitiatingProcessId, ProcessCommandLine
| order by Timestamp asc
| take 100
```

<details>
<summary>Query hint</summary>

Replace `<JXA_EXECUTABLE>` with `osascript`. Its command line uses `-l JavaScript`.

</details>

4. Find the selected Copilot and Node instances, the JXA execution, and the shell commands that follow.
5. Compare their timestamps and command lines with the portal. This query includes nearby process activity, not only descendants; do not attribute every returned process to the case.
6. Look at resolved script paths. Does a command name alone establish that the real operating-system utility ran?

## Hunt: inspect the captured script evidence

The process command line names a script; it does not show all its contents. Use a second evidence source to examine captured code.

Run this query with the same device ID:

```kusto
let deviceId = "<MAC_DEVICE_ID>";
let startTime = datetime(2026-11-02T18:34:00Z);
let endTime = datetime(2026-11-02T18:37:00Z);
DeviceEvents
| where Timestamp between (startTime .. endTime)
| where DeviceId == deviceId
| where ActionType == "ScriptContent"
| extend ScriptText = tostring(parse_json(AdditionalFields).ScriptContent)
| project Timestamp, InitiatingProcessFileName, InitiatingProcessId, ScriptText
| order by Timestamp asc
| take 50
```

1. Expand the script-text cells or copy them into a lab-approved local text view. Read the code as evidence; do not execute it.
2. Match the initiating process and timestamp to the process hunt.
3. Identify the short synthetic hardware-information stub and the longer JXA script. Explain why the stub changes how you interpret the command named `system_profiler`.
4. If available, find the corresponding **Endpoint Script Content** event in the device timeline using the same time and process.

These events expose captured script fragments for this run, not necessarily the complete `server.mjs` source. The file page's **File content** tab can require an analysis submission; do not submit files or run analysis.

## Investigate: what does the protection result establish?

1. Return to the alert and record its displayed detection and protection status, including **Blocked** if shown.
2. Inspect any available action details. Identify the target, action time, and actual result; mark unavailable details as unknown.
3. Compare those details with the execution timestamps and captured scripts. Can you establish that execution was prevented, or only that activity was detected?
4. If the lab team supplies approved saved-run results, distinguish those from what you observed directly.

The documented scenario uses synthetic discovery. Do not infer data transfer from the alert title or a script name. Likewise, process creation and captured code do not prove that every operation in the script completed.

## Explain your findings

1. What was the user's authorized task?
2. What evidence connects the task's agent to Node, JXA, and shell activity?
3. What did script inspection add beyond the process tree?
4. What is known about detection, and what remains unknown about prevention or information theft?

<details>
<summary>Explain the finding: unexpected execution, qualified outcome</summary>

![Attack story: A campaign-summary request leads through Copilot, a Node entry script, JXA, and shell activity. Captured code shows synthetic discovery. Configuration, an alert title, and a Blocked label do not independently establish invocation, theft, or prevention.](media/macos-mcp-story.svg)

The task is a campaign summary; the observed chain includes a local Node entry script and JXA/shell activity. Captured code and resolved paths identify synthetic discovery, including a stub rather than the real hardware-information utility. A current MCP configuration match is supporting context, not authoritative historical invocation telemetry.

The earlier investigation report describes completed simulated discovery and no archiving or uploading in its reported run. Do not transfer that outcome automatically to a different replay: establish it from this run's evidence or label the conclusion as reference-based. A Blocked label alone does not resolve whether the observed activity was prevented.

[Editable diagram source](media/macos-mcp-story.excalidraw)

</details>

## Finish the lab

[Compare your findings and sign out](README.md#compare-your-findings)

Optional: [Explore Agent 365 investigation context](optional-agent-365.md).
