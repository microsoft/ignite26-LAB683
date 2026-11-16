# Discover agents, investigate threats, and hunt for evidence

An AI agent can turn a simple request into a sequence of file access, tool calls, and operating-system commands. As a security analyst, how do you tell useful automation from a security incident?

You'll work in a preconfigured environment where the suspicious activity has already taken place. Follow the alerts, reconstruct the agents' actions, and explain how Defender responded.

## What threats are we investigating?

AI agents can be redirected by malicious instructions, become misaligned with the user's task, or invoke an unsafe tool. The resulting activity can resemble a human attacker: discovering the network, accessing credentials, or executing suspicious scripts. A new way to trigger harmful behavior does not make familiar endpoint protections irrelevant.

Defender combines **agent context**, **AI-specific runtime protection**, and **endpoint behavioral protection**. Discovery helps identify the agent behind a process. Runtime protection can inspect supported agent interactions for malicious instructions. Endpoint controls can detect and stop suspicious behavior in the agent's processes and tools.

These are three examples from broader, evolving detection coverage, not a complete detection catalog or one exercise per detection. For the wider picture, see [Microsoft Defender's AI security capabilities](https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/defender-security-for-ai).

| Case | Reported concern | Protection lesson |
|---|---|---|
| **1: Prompt injection on Windows** | Malicious content attempts to redirect an agent toward credential theft. | AI Agent Runtime Protection inspects supported agent interactions for malicious instructions. |
| **2: Misalignment on Windows** | A document-search task leads to network scanning and attempted credential access. | Endpoint detections remain valuable when an agent performs familiar attacker behaviors. |
| **3: Unsafe tool integration on macOS** | A campaign-summary request leads through a local MCP server to suspicious script execution. | Tool processes and their descendants remain subject to endpoint behavioral protection. |

Treat these briefs as the concerns to investigate, not proof of the cause or outcome. Correlate the agent with the activity and establish what Defender actually detected or stopped.

### Understand the protection layers

The prompt-injection protection illustrated in scenario 1 requires [AI Agent Runtime Protection (preview)](https://learn.microsoft.com/en-us/defender-endpoint/ai-agent-runtime-protection-overview) to be enabled for a supported agent and inspection method. Audit and block modes have different outcomes; do not infer prevention from an alert title alone.

That setting is not a master switch for all endpoint protection. Scenarios 2 and 3 illustrate additional detection and protection layers when suspicious activity reaches processes, scripts, and tools. Coverage and prevention still depend on the platform, configuration, and observed behavior; not every harmful agent action is guaranteed to be detected or blocked.

**No configuration changes are required in this lab.** Investigate the existing recordings, including the runtime-protection evidence in scenario 1. For deployment outside the lab, see [Set up AI agent runtime protection](https://learn.microsoft.com/en-us/defender-endpoint/configure-ai-agent-runtime-protection).

## Your investigation path

Portal investigation and Advanced Hunting are complementary skills. In each exercise, start with a question, inspect the portal evidence, run a focused hunt, and explain what you found. You will interpret and adjust supplied queries, not write KQL from scratch.

| Activity | Time | Portal investigation | Advanced Hunting |
|---|---|---|---|
| [Sign in and get oriented](00-get-started.md#sign-in-to-the-lab) | 5 minutes | Open the assigned environment | Not required |
| [Discover local agents](00-get-started.md#discover-the-local-agents) | 10 minutes | Inspect agent instances and their configuration | Compare inventory observations |
| [Investigate Windows prompt injection](01-windows-xpia.md) | 15 minutes | Read the malicious prompt and follow the protection evidence | Corroborate the detection result |
| [Investigate Windows agent misalignment](02-agent-misalignment.md) | 20 minutes | Compare the user's task with the agent's actions | Measure scanning and inspect credential-access protection |
| [Investigate a macOS MCP execution chain](03-macos-runtime.md) | 20 minutes | Trace the task, tool process, and script activity | Reconstruct execution and inspect captured script content |
| [Compare your findings](#compare-your-findings) | 5 minutes | Explain the three stories | Support each conclusion with evidence |

Optional [Agent 365 exploration](optional-agent-365.md) is outside the 75-minute path.

## What you need

- An assigned LAB683 environment and an individual lab account.
- A browser with access to the lab's Microsoft Defender portal, local-agent inventory, alerts, device timelines, and Advanced Hunting.
- The lab team's current scenario links if they have refreshed the recordings. Each exercise also explains how to locate the documented run by alert title and UTC time.

Use the assigned lab account, not a personal or production tenant. A VM may host your browser, but you will not install agents, onboard endpoints, or generate attacks.

## Work safely in the shared environment

Read existing evidence only. Do not assign, classify, resolve, or otherwise edit incidents or alerts. Do not isolate devices, run Live Response, submit files for analysis, change policies, or execute commands found in attack evidence.

Keep credentials and sensitive identifiers out of screenshots and shared notes. The public instructions intentionally omit tenant IDs and direct tenant-specific links.

## Compare your findings

Complete this table in your own notes:

| Question | Windows prompt injection | Windows misalignment | macOS MCP activity |
|---|---|---|---|
| What was the authorized task or attempted redirection? | | | |
| What did the agent actually do? | | | |
| Which portal evidence supports your explanation? | | | |
| What did your hunt add? | | | |
| What did Defender detect or prevent? What remains unknown? | | | |
| Which protection layer contributed, and what did agent context add? | | | |

Explain one conclusion you could not safely draw from an alert title alone. Why can familiar endpoint protections still help when an agent, rather than a human attacker, initiates the activity? Then sign out of the lab account and end your lab session.

## Start the lab

[Sign in and discover the agents](00-get-started.md)
