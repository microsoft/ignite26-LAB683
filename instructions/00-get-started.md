---
title: Discover local AI agents in Microsoft Defender
description: Find local AI agents, inspect their configuration, and compare inventory observations before investigating threats.
author: j0shbregman
ms.author: j0shbregman
ms.service: microsoft-defender-xdr
ms.topic: how-to
ms.date: 11/15/2026
ai-usage: ai-generated
---

# Discover local AI agents in Microsoft Defender

Before investigating an agent's behavior, establish what it is, where it runs, and which tools it is configured to use. The same agent application can have several instances on different devices or accounts.

**Your mission:** Find the lab's local agents and compare their configuration using both the portal and an inventory hunt. Allow 5 minutes for sign-in and 10 minutes for discovery.

## Sign in to the lab

1. Launch the assigned LAB683 environment. If it provides a VM, sign in with the supplied VM credentials and open its browser.
2. Open [Microsoft Defender](https://security.microsoft.com) and sign in with your assigned lab account. Use the sign-in method supplied by the lab, such as a Temporary Access Pass.
3. Confirm that you are in the assigned lab tenant. If a personal or production account is already signed in, sign out before continuing.
4. Open a separate browser tab for these instructions. Keep Defender open throughout the lab.

If you cannot access the assigned environment, contact the lab team. Do not use another tenant or change account permissions.

## Discover the local agents

**Question: Which agent instances are present, and what are they configured to do?**

1. In Defender, expand **Assets** > **AI agents** and select **Local agents**. Select **Show navigation** first if the navigation is collapsed.
2. Find **GitHub Copilot CLI**. Open an instance and note its device and account context; the application name alone does not identify a particular execution.
3. Inspect the related process, auto-approval, trust, and MCP configuration where available.
4. Compare a second instance. Record one configuration difference, or identify a field that is not available.
5. If **Open agent page** is available, inspect it, then return to the inventory. You do not need its map or an alerts tab to complete this lab.

If the default Agents view fails before the tabs appear, use the lab team's direct **Local agents inventory** link. If neither route works, continue with the inventory hunt and record that the portal step was unavailable.

Do not treat an MCP configuration entry as proof that a tool was called. You will look for execution evidence later.

## Hunt: compare the inventory observations

**Question: Can you find the same instances in the hunting data?**

1. Open **Investigation & response** > **Hunting** > **Advanced hunting**, or select **Go hunt** from an agent pane.
2. Dismiss any introductory tour with **Not now**. Open **New query** and select **Query in editor** if prompted.
3. Set the time picker to **Last 30 days**, paste the query below, and select **Run query**.

```kusto
AgentsInfo
| where Timestamp > ago(30d)
| where Platform == "LocalAgents"
| summarize arg_max(Timestamp, *) by AgentId
| where LifecycleStatus !in ("Deleted", "Uninstalled")
| extend Local = RawAgentInfo.localAgentMetadata
| project Timestamp, AgentId, Name, SourceAgentId, Version,
    DeviceName = tostring(Local.deviceName),
    RelatedProcess = tostring(Local.relatedProcess),
    AutoApprove = tostring(Local.autoApprove),
    TrustedProcess = tostring(Local.trustedProcess)
| order by DeviceName asc, Name asc
| take 50
```

4. Find an instance you inspected in the portal. Compare its name, device, related process, and auto-approval value.
5. Explain the `summarize arg_max(Timestamp, *) by AgentId` line: it selects the latest observation per profile rather than displaying every historical observation.
6. Notice the observation time. An inventory record describes configuration observed at that time, not necessarily configuration during an older attack.

If the query returns 50 rows, narrow its scope before treating it as a complete inventory. Do not use a fixed profile count as the success criterion; inventory can change.

## Keep your investigation scoped

The next exercises use historical evidence. Follow these conventions throughout:

- **Device:** Copy the device ID from the selected alert's device page. If it is not shown in details, the device page address contains it after `/machines/v2/`. Do not copy the tenant's `tid` value. The two Windows runs have different device IDs even though their display names match.
- **Time:** Queries use explicit UTC windows. Portal timeline fields may be labeled **Local**; convert the UTC window to the timezone shown by your browser/VM. Do not assume a fixed Pacific offset.
- **Query inputs:** Replace every `<...>` input before running. Keep device IDs inside quotation marks. Leave `datetime(...)` values unquoted.
- **Missing results:** Check the account, device ID, time picker, and evidence retention before drawing conclusions. A time picker narrower than the query window can exclude the events.
- **Result limits:** If results reach a query's `take` limit, narrow or partition the window.

For each investigation, keep four short notes: **user goal, observed behavior, Defender response, and supporting evidence**. Record uncertainty rather than guessing.

## Explain your findings

Before continuing, answer:

1. What distinguishes an agent application from an instance on a device?
2. Which configuration difference did you observe?
3. Why can't inventory alone tell you whether an agent executed a command?

## Next step

[Investigate a Windows prompt-injection attempt](01-windows-xpia.md)
