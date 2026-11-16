# Discover agents, investigate threats, and hunt for evidence

An AI agent can turn a simple request into a sequence of file access, tool calls, and operating-system commands. As a security analyst, how do you tell useful automation from a security incident?

In this lab, investigate three stories in Microsoft Defender:

- **A malicious instruction:** Someone tries to make a Windows agent disclose credentials.
- **A task that goes too far:** An agent asked to find sales documents starts scanning the network and attempting credential access.
- **Code behind a tool:** A campaign-summary task on macOS leads to a local MCP server and unexpected script execution.

You'll work in a preconfigured environment where the suspicious activity has already taken place. Follow the alerts, reconstruct the agents' actions, and explain how Defender responded.

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

Explain one conclusion you could not safely draw from an alert title alone. Then sign out of the lab account and end your lab session.

## Start the lab

[Sign in and discover the agents](00-get-started.md)
