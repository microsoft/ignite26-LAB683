---
title: Start the LAB683 investigations in Microsoft Defender
description: Discover local AI agents in Microsoft Defender, compare instance configuration, and correlate alert evidence with inventory before the LAB683 investigations.
author: j0shbregman
ms.author: j0shbregman
ms.service: microsoft-defender-xdr
ms.topic: how-to
ms.custom: msecd-doc-authoring-1032
ms.date: 10/23/2026
ai-usage: ai-generated
#customer intent: As a SOC analyst, I want to access the prepared lab evidence so that I can investigate local AI agent threats.
---

# Start the LAB683 investigations in Microsoft Defender

Use your assigned Microsoft Defender account to discover local agents and run an inventory hunt before the three investigations. Check the prerequisites before signing in. The evidence already exists; you do not install software or generate attacks. Allow 5 minutes for sign-in and 12 minutes for discovery and hunting.

## Prerequisites

- An assigned LAB683 Skillable session.
- Individual lab credentials supplied securely through the lab experience.
- Assigned access to read the lab's alerts, devices, and agent inventory and to run Advanced Hunting queries.
- Scenario references supplied in the controlled instructions.

**Tester draft:** The walkthrough uses observed portal controls and API-validated evidence. The lab team still needs to rehearse it with attendee accounts and finish the controlled scenario reference sheet.

## Open the assigned environment

Sign in to the prepared tenant and locate the reference values that keep your investigation scoped to the lab.

1. Launch LAB683 from the event-provided Skillable entry point.
2. Open the supplied browser experience and sign in to [Microsoft Defender](https://security.microsoft.com) with your assigned lab account.
3. Confirm you are in the lab environment identified by the instructor. If an existing personal or production session opens, stop and ask for help.
4. Locate the **Scenario reference sheet** in the controlled lab instructions. It must supply the following values for each investigation:

   | Value | Why you need it |
   |---|---|
   | Alert link and alert ID | Open the correct starting evidence |
   | Device link and device ID | Distinguish devices that share a display name |
   | Start and end in UTC, plus portal-local equivalents | Apply the correct query and timeline windows |
   | Agent process ID and creation time | Select the correct process instance |
   | Prompt locator: action type, time and text prefix | Distinguish similarly named prompt events |

5. If a value is missing, ask the instructor for it. Do not substitute your own tenant, the current time, or another device with the same name.
6. If a view is inaccessible, ask the lab team to check access. Do not change permissions or use an administrator account.

## Prepare your investigation notes

Keep observations separate from hypotheses so your conclusions can be traced to evidence.

1. For each scenario, record the legitimate user goal, suspicious behavior, supporting evidence, and observed outcome.
2. Separate direct observations from hypotheses. An alert title alone does not prove that every described action executed.
3. Treat shared incidents and devices as read-only. Do not change status, assignment, classification, policies, or endpoint state.
4. Keep credentials and sensitive identifiers out of notes and screenshots.

You are ready when the assigned account opens the lab portal and the first scenario's prepared evidence is accessible.

## Discover the local agents

Use inventory to establish which agent instance you are investigating.

1. Expand **Assets** in the Defender navigation. If the full navigation is hidden, select **Show navigation** first.
2. Select **AI agents**, then **Local agents**.
   If the initial **Agents** view displays **Something went wrong** and the tabs are unavailable, open the instructor-provided **Local agents inventory** link. That direct local view was usable when the default view failed. If it also fails, report the issue and continue with the inventory hunt below; record the UI step as incomplete.
3. Locate **GitHub Copilot CLI** on the Windows or Mac device listed in your reference sheet. An agent name alone is not sufficient: compare device and account context.
4. Select the row to open its details pane.
5. Review the agent's related process and source agent identity. Review auto-approval, trust, risk, and MCP information where the pane exposes them.
6. Compare another instance if one is present. Record a configuration difference, or state that the relevant field is unavailable.
7. Do not interpret a configured MCP entry as proof that the agent invoked it. Do not interpret an empty field as a safe configuration.

**Expected result:** You can distinguish an agent application from an instance associated with a device/account. Inventory does not reconstruct the agent's conversation.

If **Open Agent page** is available, you can inspect it, but the required path does not depend on its map or an **Incidents and alerts** tab loading.

## Run an inventory hunt

This query shows the latest observed profile for each local agent in the selected window.

1. Open **Advanced hunting** from the navigation. Alternatively, use **Go hunt** from the agent pane if available.
2. If a guided-hunting tour opens, select **Not now**.
3. Open a **New query** tab and use the KQL editor. If your account opens a query-builder view instead, ask the instructor to help you open the advanced query editor.
4. Replace the editor contents with the following query.
5. Set the hunting time range to include the last seven days, then select **Run query**.

```kusto
AgentsInfo
| where Timestamp > ago(7d)
| where Platform == "LocalAgents"
| summarize arg_max(Timestamp, *) by AgentId
| where LifecycleStatus !in ("Deleted", "Uninstalled")
| extend Local = RawAgentInfo.localAgentMetadata
| project Timestamp, AgentId, Name, SourceAgentId, Version, LifecycleStatus,
    DeviceName = tostring(Local.deviceName),
    RelatedProcess = tostring(Local.relatedProcess),
    AutoApprove = tostring(Local.autoApprove),
    TrustedProcess = tostring(Local.trustedProcess)
| order by DeviceName asc, Name asc
| take 50
```

6. In the results, compare **Name**, **DeviceName**, **RelatedProcess**, and **AutoApprove**.
7. Note that **AgentId** is the profile GUID, while **SourceAgentId** is the source identity. Do not join these interchangeably.
8. If exactly 50 rows are returned, narrow the investigation; this is a capped result, not a complete inventory.

**Expected result:** In the prepared dataset, the Windows Copilot profiles report auto-approval as `"true"` and the Mac CLI profile reports `"false"`. These are profile observations, not proof of what every individual command did. Values and row counts can change when the dataset is refreshed.

## Correlate an alert with its discovered agent

This second query will also be used in the Windows and Mac exercises.

1. In a **New query** tab, paste the query below.
2. Replace `<SCENARIO_ALERT_ID>` with the Windows XPIA alert ID from the reference sheet.
3. Set the hunting time range to include both the prepared alert and recent profile observations, then select **Run query**.

```kusto
let scenarioAlertId = "<SCENARIO_ALERT_ID>";
let profiles =
    AgentsInfo
    | where Platform == "LocalAgents"
    | summarize arg_max(Timestamp, *) by AgentId
    | project ProfileAgentId = tostring(AgentId), SourceAgentId, Name,
        EntraAgentID, RawAgentInfo;
AlertEvidence
| where AlertId == scenarioAlertId
| where EntityType == "AIAgent"
| extend SourceAgentId = tostring(parse_json(AdditionalFields).AgentId)
| distinct AlertId, SourceAgentId
| join kind=leftouter profiles on SourceAgentId
| project AlertId, SourceAgentId, ProfileAgentId, Name, EntraAgentID,
    DeviceName = tostring(RawAgentInfo.localAgentMetadata.deviceName)
| take 50
```

4. Confirm the matching name and device. An empty profile side means the correlation was not established; ask for help rather than invent another join.
5. Keep the query open for reuse with the Mac alert ID.

**Expected result:** The prepared Windows XPIA and Mac alerts each correlate to a GitHub Copilot CLI profile through the source identity. Their matching **EntraAgentID** fields were empty when the evidence was checked. This does not prevent the required Defender investigations.

## Use the queries safely

Apply the reference values and time windows consistently to avoid misleading results.

1. Replace every `<...>` value in later queries with the corresponding reference-sheet value before running.
2. Enter UTC timestamps such as `2026-10-23T03:00:00Z` into KQL `datetime(...)` expressions. For portal fields labeled **(Local)**, use the separately supplied local equivalent.
3. Ensure the hunting time picker includes the query's explicit window. A narrower picker can exclude matching events.
4. If results are empty, check the account, device ID, window, and ingestion state. Empty results alone do not establish prevention.
5. If results reach a query's `take` limit, narrow or partition the window before drawing a conclusion.

Full prompt and response bodies shown in the portal were not exposed by the retrieved Advanced Hunting records. Use the prompt panels in the following exercises; do not expect these queries to return a full conversation.

## Next step

> [!div class="nextstepaction"]
> [Investigate Windows XPIA](01-windows-xpia.md)
