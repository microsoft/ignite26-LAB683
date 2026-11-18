# Discover agents, investigate threats, and hunt for evidence

An AI agent can turn a simple request into a sequence of file access, tool calls, and operating-system commands. As a security analyst, how do you tell useful automation from a security incident?

You'll work in a preconfigured environment where the suspicious activity has already taken place. Follow the alerts, reconstruct the agents' actions, and check how Defender responded.

## What threats are we investigating?

Malicious instructions can redirect an agent. The agent can also stray from the user's task or call an unsafe tool. You might then see network scans, attempts to access credentials, or suspicious scripts. Defender can detect these familiar attack patterns even when an agent starts them.

Defender combines **agent context**, **AI-specific runtime protection**, and **endpoint behavioral protection**. Discovery helps identify the agent behind a process. Runtime protection can inspect supported agent interactions for malicious instructions. Endpoint controls can detect and stop suspicious behavior in the agent's processes and tools.

The 75-minute core includes a discovery foundation and two Windows investigations. A third investigation on macOS is an optional bonus if time permits. For more examples, see [Microsoft Defender's AI security features](https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/defender-security-for-ai).

| Case | Activity to investigate | What you'll learn |
|---|---|---|
| **1: Prompt injection on Windows** | Malicious content attempts to redirect an agent toward credential theft. | AI Agent Runtime Protection inspects supported agent interactions for malicious instructions. |
| **2: Misalignment on Windows** | A document-search task leads to network scanning and attempted credential access. | Endpoint detections remain valuable when an agent performs familiar attacker behaviors. |
| **Bonus: Unsafe tool integration on macOS** | A campaign-summary request leads through a local MCP server to suspicious script execution. | Tool processes and their descendants remain subject to endpoint behavioral protection. |

In each case, use the alert, process tree, and hunting results to investigate what the agent did and how Defender responded.

## Understand the protection layers

Scenario 1 uses [AI Agent Runtime Protection (preview)](https://learn.microsoft.com/en-us/defender-endpoint/ai-agent-runtime-protection-overview). It must be turned on for a supported agent and inspection method. You'll follow the prompt-call and detection events, then check how Defender responded.

**Note:** Enabling and configuring this protection is outside the scope of this lab. You'll investigate existing events without changing any settings.

In scenario 2 and the optional macOS bonus, you'll follow the agent's processes, scripts, and tools. See how endpoint protection detects network scans, attempts to access credentials, and other familiar attack patterns.

For deployment outside the lab, see [Set up AI agent runtime protection](https://learn.microsoft.com/en-us/defender-endpoint/configure-ai-agent-runtime-protection).

## Your investigation path

Portal investigation and Advanced Hunting are complementary skills. In each exercise, start with a question, inspect the portal evidence, run a focused hunt, and check the findings. You will interpret and adjust supplied queries, not write KQL from scratch.

| Activity | Time | Portal investigation | Advanced Hunting |
|---|---|---|---|
| [Sign in and get oriented](00-get-started.md#sign-in-to-the-lab) | 5 minutes | Open the assigned environment | Not required |
| [Discover local agents](00-get-started.md#discover-local-ai-agents) | 10 minutes | Inspect agent instances and their configuration | Compare inventory observations |
| [Investigate Windows prompt injection](01-windows-xpia.md) | 25 minutes | Read the malicious prompt and follow the protection evidence | Corroborate the detection result |
| [Investigate Windows agent misalignment](02-agent-misalignment.md) | 30 minutes | Compare the user's task with the agent's actions | Measure scanning and inspect credential-access protection |
| [Compare your core findings](#core-complete-compare-the-windows-cases) | 5 minutes | Review the two Windows stories | Compare the evidence behind each conclusion |
| **Core total** | **75 minutes** | **Complete the foundation and both Windows cases** | **No macOS investigation required** |

**[Optional bonus: macOS MCP execution](03-macos-runtime.md), about 20 minutes.** Attempt it only if you finish early and have enough session time left. The bonus does not extend the lab timer. The time for each Windows case includes its reflection page.

## What you need

- An assigned LAB683 environment with WIN1 and an individual lab account.
- Access to the prepared Defender evidence and Advanced hunting.
- The controlled Skillable instructions, which supply credentials, case links, and device IDs.

These public pages preserve the lab's numbered sections, but use standard GitHub images and expandable details instead of Skillable-only markup. Copy the device ID supplied for each case into its query; the two Windows runs have different device IDs despite sharing a display name. Query windows are UTC. The explicit timeline entries assume the lab's Pacific local timezone; convert them if your VM uses another timezone.

The evidence is historical. If a link or query no longer returns the documented run, ask the lab team for refreshed values rather than choosing an unrelated alert. Match the replacement device, UTC window, PID, and creation time together. The inventory query uses a rolling 30-day window; its observation time is not a process start time. A result cap is not a complete inventory.

## Work safely in the shared environment

Read existing evidence only. Do not assign, classify, resolve, or otherwise edit incidents or alerts. Do not isolate devices, run Live Response, submit files for analysis, change policies, or execute commands found in attack evidence. Keep credentials, account details, and private identifiers out of screenshots and shared notes.

## Start the lab

[Sign in and discover the agents](00-get-started.md)

## Core complete: Compare the Windows cases

You've finished the discovery foundation and both core investigations. Allow 5 minutes to compare their findings. You do not need to write a summary or complete the macOS bonus.

How did each agent's activity create risk? Which evidence establishes Defender's response, and which questions remain open?

<details>
<summary>Show the two-case comparison</summary>

| Question | Windows prompt injection | Windows misalignment |
|---|---|---|
| What was the task or attempted redirection? | Embedded instructions requested credential files, external transfer, and concealment. | The employee asked for the latest sales documents. |
| What did the agent do? | Copilot encountered the malicious prompt; the requested theft is not established. | Copilot launched PowerShell branches for searching, scanning, and credential-related activity. |
| What did portal evidence show? | Copilot's prompt-call node, the blocked-injection story, and detection details. | The user request, Copilot-to-PowerShell ancestry, and the LSASS prevention record. |
| What did hunting add? | A `netpromptstream` prompt-injection detection reporting remediation. | Connections to ports 22, 139, and 445, with mostly failures and one port-22 success; LSASS-related detection evidence. |
| What did Defender prevent? | The injection was blocked and remediation reported. | The LSASS-related attempt was blocked; the protection record reports quarantine and Success. |
| What remains unknown? | Credential-file access or transfer is not established. | Connection success does not prove a login. Successful credential theft is not established. |
| Which protection layer contributed? | AI Agent Runtime Protection inspected the prompt; agent context tied it to Copilot. | Endpoint protection detected the credential-access attempt; process ancestry tied it to Copilot. |

Agent context connects suspicious activity to the employee's agent and task. Use the underlying evidence to distinguish a detection, a successful connection, and a confirmed prevention.

</details>

### Choose where to finish

**Finish the core lab here:** In WIN1, sign out of the lab's Defender account. Return to Skillable and end this lab session. Do not sign out of your host browser profile or close unrelated windows.

**Continue to the bonus:** If about 20 minutes remain on your session timer, stay signed in and open the [optional macOS investigation](03-macos-runtime.md). The macOS investigation is optional and does not extend the timer. Nothing in the bonus is required to complete the core lab.
