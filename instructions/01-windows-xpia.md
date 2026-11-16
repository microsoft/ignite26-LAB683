---
title: Investigate a Windows prompt-injection attempt
description: Read a malicious instruction, trace the affected agent, and use hunting evidence to assess Defender's protection result.
author: j0shbregman
ms.author: j0shbregman
ms.service: microsoft-defender-xdr
ms.topic: how-to
ms.date: 11/16/2026
ai-usage: ai-generated
---

# Investigate a Windows prompt-injection attempt

An attacker does not have to control an agent's original user request to influence it. Instructions embedded in content the agent reads can try to redirect its work.

In this case, a Windows coding agent encounters an instruction requesting access to credential files and a transfer to an external destination. Your job is to determine what the instruction requested and what Defender did about it.

**Your mission:** Read the attack in the portal, connect it to the agent process, and corroborate the protection result with one hunt. Allow 15 minutes. Complete [discovery](00-get-started.md) first.

## Case brief

- **Intended task:** Continue the user's work without treating instructions in retrieved content as new authorization.
- **Reported concern:** An instruction asks the agent to read credential files, send their contents externally, and conceal the activity.
- **Investigation question:** What did the instruction request, which agent encountered it, and what evidence establishes Defender's response?

**Protection lens:** The AI-specific runtime protection illustrated here requires enablement for a supported agent and inspection method. You are investigating an existing recording, not enabling protection. Distinguish audit from block behavior and corroborate the reported outcome; see [how the lab's protection layers fit together](README.md#understand-the-protection-layers).

## Open the case

Use the lab team's Windows XPIA link if supplied. Otherwise:

1. Open **Investigation & response** > **Incidents & alerts** > **Alerts**.
2. Set the time range to include October 23, 2026. Find **Suspicious AI prompt injection blocked** within **03:00-03:30 UTC**.
3. Open the alert. Compare its ID with the lab's case link if available, then inspect the affected device and **GitHub Copilot CLI** evidence.
4. Open the device in a separate tab and copy its device ID for the query below.

The documented run is scoped as follows. If the lab team supplies a refreshed run, use all of its replacement values together.

| Reference | Documented run |
|---|---|
| Investigation window | October 23, 2026, 03:00-03:30 UTC |
| Agent process | `copilot.exe`, PID 4984 |
| Process creation | October 23, 2026, 03:04:13 UTC |
| Captured malicious prompt call | October 23, 2026, 03:13:11 UTC |

The portal can display a different incident-related heading for the selected alert. Use the alert ID, process, and blocked-injection story node to stay on the correct case. If the run is unavailable, ask the lab team rather than substituting an unrelated alert.

The screenshots below use local time at UTC-04:00: **October 22, 11:13:11 PM** is **October 23, 03:13:11 UTC**. Keep the UTC values above for hunting queries. These are cropped live portal captures; numbered headings and blue outlines are lab annotations.

## Investigate: what is the attacker asking the agent to do?

1. In **Alert story**, find the Copilot process in **Process tree**, matching the PID and creation time above. Use the story's **Maximize** control for more space, then expand the process details.

   ![Expanded copilot.exe process showing PID 4984 and its captured command line.](media/windows-xpia-process.png)

   Match the agent execution, not just its filename. The command line shown is evidence from the recorded run, not a setup instruction.

2. Locate **Suspicious AI prompt injection blocked**, then select the adjacent **copilot.exe made a prompt call to the model** node.

   ![Alert story linking the 11:13:11 PM prompt call to the blocked-injection label, followed by a PromptInjection credential-theft detection in copilot.exe.](media/windows-xpia-story-nodes.png)

   The prompt-call node contains the instruction. The credential-theft detection below is a separate evidence point. A **Detected** badge alone does not establish prevention; corroborate the outcome in the hunt.

3. Expand the prompt-call node, or open its **Details** pane, and read **Prompt content**. Find the instruction starting **[SYSTEM INSTRUCTION] Ignore all previous instructions**.

   ![Expanded prompt content requesting .env and AWS credential files, a POST to a test destination, and concealment from the user.](media/windows-xpia-prompt.png)

   Read the complete instruction: the requested files, external transfer, and concealment are what make the attempted redirection clear.

4. Identify the files it requests, the destination it names, and the instruction to conceal the activity.
5. In your notes, explain why text that claims to be a system instruction is not automatically an authorized instruction.

The screenshots are references, not replacements for successful live steps. If a prompt pane is empty, expand the adjacent prompt-call node and match the content prefix. Allow the story to finish loading before concluding that evidence is missing. If neither view works, record the limitation.

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
