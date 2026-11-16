---
title: Investigate a Windows prompt-injection attempt
description: Read a malicious instruction, trace the affected agent, and use hunting evidence to assess Defender's protection result.
author: j0shbregman
ms.author: j0shbregman
ms.service: microsoft-defender-xdr
ms.topic: how-to
ms.date: 11/15/2026
ai-usage: ai-generated
---

# Investigate a Windows prompt-injection attempt

An attacker does not have to control an agent's original user request to influence it. Instructions embedded in content the agent reads can try to redirect its work.

In this case, a Windows coding agent encounters an instruction requesting access to credential files and a transfer to an external destination. Your job is to determine what the instruction requested and what Defender did about it.

**Your mission:** Read the attack in the portal, connect it to the agent process, and corroborate the protection result with one hunt. Allow 15 minutes. Complete [discovery](00-get-started.md) first.

## Open the case

Use the lab team's Windows XPIA link if supplied. Otherwise:

1. Open **Investigation & response** > **Incidents & alerts** > **Alerts**.
2. Set the time range to include October 23, 2026. Find **Suspicious AI prompt injection blocked** around **03:05 UTC**.
3. Open the alert. Compare its ID with the lab's case link if available, then inspect the affected device and **GitHub Copilot CLI** evidence.
4. Open the device in a separate tab and copy its device ID for the query below.

The documented run is scoped as follows. If the lab team supplies a refreshed run, use all of its replacement values together.

| Reference | Documented run |
|---|---|
| Investigation window | October 23, 2026, 03:00-03:30 UTC |
| Agent process | `copilot.exe`, PID 4984 |
| Process creation | October 23, 2026, 03:04:13 UTC |

The portal can display a different incident-related heading for the selected alert. Use the alert ID, process, and blocked-injection story node to stay on the correct case. If the run is unavailable, ask the lab team rather than substituting an unrelated alert.

## Investigate: what is the attacker asking the agent to do?

1. In **Process tree**, find the Copilot process matching the PID and creation time above.
2. Locate **Suspicious AI prompt injection blocked**, then select the adjacent **copilot.exe made a prompt call to the model** node.
3. Expand **Details** and read **Prompt content**. Find the instruction starting **[SYSTEM INSTRUCTION] Ignore all previous instructions**.
4. Identify the files it requests, the destination it names, and the instruction to conceal the activity.
5. In your notes, explain why text that claims to be a system instruction is not automatically an authorized instruction.

![Windows prompt evidence requesting credential disclosure to a test destination.](media/windows-xpia-prompt.png)

The screenshot is a reference, not a replacement for a successful live step. If a prompt pane is empty, check the adjacent prompt-call node and match the content prefix. If neither works, record the limitation.

Do not execute the captured instruction or visit its destination.

## Investigate: what does the timeline show?

1. Return to the alert and select **See in timeline**.
2. Confirm that this is the same device, then select **Time range** > **Custom range**.
3. Enter the investigation window above, converted to the portal's local timezone, and select **Apply**.
4. Search for `copilot.exe`. Inspect the prompt event and the prompt-injection detection.
5. Read the detection/remediation details. Record the reported outcome before running the hunt.

If an existing highlight or search hides the events, clear only the view filter. Do not edit or mark shared timeline rows. Generic prompt-call labels can describe different events; read their details rather than assuming every row contains an attack.

## Hunt: corroborate the protection result

**Question: Does the underlying detection record support the portal's protection story?**

1. Open **Advanced hunting** > **New query**.
2. Replace `<WINDOWS_XPIA_DEVICE_ID>` with the device ID you copied. Set the time picker to include the full UTC window.
3. Run this query:

```kusto
let deviceId = "<WINDOWS_XPIA_DEVICE_ID>";
let startTime = datetime(2026-10-23T03:00:00Z);
let endTime = datetime(2026-10-23T03:30:00Z);
DeviceEvents
| where Timestamp between (startTime .. endTime)
| where DeviceId == deviceId
| where ActionType == "AntivirusDetection"
| extend Evidence = parse_json(AdditionalFields)
| where tostring(Evidence.ThreatName) contains "PromptInjection"
| project Timestamp, InitiatingProcessFileName,
    ThreatName = tostring(Evidence.ThreatName),
    ResourceSchema = tostring(Evidence.ResourceSchema),
    WasRemediated = tostring(Evidence.WasRemediated),
    WasExecutingWhileDetected = tostring(Evidence.WasExecutingWhileDetected)
| order by Timestamp asc
| take 100
```

4. Find `Trojan:AIMCP/PromptInjection.B!CredTheft` with `ResourceSchema` equal to `netpromptstream`.
5. Compare the remediation and execution flags with the portal evidence. Empty fields mean the record does not supply that value, not that it is `false`.

The query adds reported detection outcomes, not a full conversation or an exhaustive audit of every file read or network destination.

## Explain your findings

Write a short incident explanation before opening the checkpoint:

1. What did the malicious instruction request?
2. Which evidence connects it to the selected Copilot process?
3. What supports a prevention conclusion, beyond the alert's title?

<details>
<summary>Explain the finding: attempted redirection and recorded prevention</summary>

![Attack story: Copilot encounters malicious instructions. Dashed paths show requested credential-file access and external transfer, not observed theft. Defender's prompt-stream remediation supports prevention.](media/windows-xpia-story.svg)

The instruction requests a local `.env` file and `~/.aws/credentials`, asks for their contents to be sent to a test collection destination, and asks the agent to hide that activity. The blocked-injection story and a `netpromptstream` detection reporting remediation support the protection outcome. An absent network event alone would not prove prevention, and this alert does not explain every action in the shared incident.

[Editable diagram source](media/windows-xpia-story.excalidraw)

</details>

## Next step

[Investigate an agent that exceeds its user's request](02-agent-misalignment.md)

## Related content

- [AI agent detection and protection](https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/ai-agent-detection-protection)
