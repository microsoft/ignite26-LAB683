---
title: Discover local AI agents in Microsoft Defender
description: Learn how Defender recognizes local AI agents and connects their host processes, devices, and accounts to the investigations that follow.
author: j0shbregman
ms.author: j0shbregman
ms.service: microsoft-defender-xdr
ms.topic: how-to
ms.date: 11/15/2026
ai-usage: ai-generated
---

# Discover local AI agents in Microsoft Defender

Before you can investigate an AI agent, you need to recognize it in the activity on a device. Defender identifies supported local agents and connects them to their device, account, and configuration. That context is the starting point for the investigations that follow.

**Your mission:** Identify an agent's host process, device, and account in the portal, then find the same context in an inventory hunt. You will use that process context to follow the agent's actions in the next three investigations. Allow 5 minutes for sign-in and 10 minutes for discovery.

## Why discovery matters to the investigations

For process-based discovery, Defender recognizes a supported agent when it observes the agent's process running on an onboarded device. In this lab, look for GitHub Copilot CLI and its related process. Instead of seeing only an executable, you can start an investigation knowing that it hosts an AI agent.

You will then follow that agent's process into the endpoint evidence: its child processes, commands, network connections, and associated alerts. Discovery answers **"What agent is this, and where does it run?"** The investigations answer **"What did this particular execution do, and how did Defender respond?"**

An inventory entry is not a single process execution. Defender groups a local agent by **agent type, device, and user**; several runs can belong to the same entry. In the later exercises, match the device, PID, and process creation time to identify the execution you are investigating.

Defender supports discovery of **more than 50 local AI agent types**, including command-line agents, desktop applications, agentic IDEs, and VS Code extensions. Coverage evolves: open the public [AI agent support matrix](https://learn.microsoft.com/en-us/defender-endpoint/ai-agent-support-matrix#ai-agent-discovery-support) for the current agent list and its Windows, macOS, and MCP configuration coverage. Discovery support does not automatically mean runtime protection is supported.

Discovery methods also vary. Some VS Code agents are discovered from periodically collected installed-extension data rather than a running extension. A discovered agent does not by itself prove that a user submitted a prompt or successfully accessed an AI service. See [how local agent discovery works](https://learn.microsoft.com/en-us/defender-endpoint/local-agent-discovery-overview#local-ai-agent-discovery-on-endpoints).

## Sign in to the lab

1. Launch the assigned LAB683 environment. If it provides a VM, sign in with the supplied VM credentials and open its browser.
2. Open [Microsoft Defender](https://security.microsoft.com) and sign in with your assigned lab account. Use the sign-in method supplied by the lab, such as a Temporary Access Pass.
3. Confirm that you are in the assigned lab tenant. If a personal or production account is already signed in, sign out before continuing.
4. Open a separate browser tab for these instructions. Keep Defender open throughout the lab.

If you cannot access the assigned environment, contact the lab team. Do not use another tenant or change account permissions.

## Discover the local agents

**Question: How does Defender identify the agent behind a process on a device?**

1. In Defender, expand **Assets** > **AI agents** and select **Local agents**. Select **Show navigation** first if the navigation is collapsed.
2. Find **GitHub Copilot CLI**. Open an entry and record its agent name, device, account, and **Related process**. This links the recognizable agent to the host process you will investigate later; the application name alone does not identify a particular execution.
3. Inspect auto-approval, trust, and MCP configuration where available. Which details describe what the agent is configured to do, rather than what it has actually done?
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

4. Find an entry you inspected in the portal. Match its agent name, device, and `RelatedProcess` with your notes. Explain how recognizing that host process will help you follow the agent in a process tree or device timeline.
5. Explain the `summarize arg_max(Timestamp, *) by AgentId` line: it selects the latest observation per profile rather than displaying every historical observation.
6. Notice the observation time. An inventory record describes configuration observed at that time, not necessarily configuration during an older attack.

If the query returns 50 rows, narrow its scope before treating it as a complete inventory. `take 50` is this query's result limit, not the number of agent types Defender supports. Do not use a fixed profile count as the success criterion; inventory can change.

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

1. Which host process did Defender associate with GitHub Copilot CLI?
2. Why do the device and account matter when identifying an agent? What additional details identify a particular execution?
3. How will you use that process context in the next investigations, and why can't inventory alone tell you whether a command executed?

<details>
<summary>Explain the finding: connect the agent to its process context</summary>

Defender makes a supported local agent recognizable as an asset, associated with its device, user, and host process. The portal and `AgentsInfo` show that discovery context. Endpoint process, network, and alert evidence let you investigate a particular run and its descendants.

That is the bridge to the rest of the lab: identify the agent, locate the correct process execution, and follow its actions. Configuration describes what is set up; execution evidence shows what happened. Neither discovery nor a trusted-process setting proves that all subsequent behavior is safe.

</details>

## Next step

[Investigate a Windows prompt-injection attempt](01-windows-xpia.md)
