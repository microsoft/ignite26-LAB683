# Investigate local AI agent threats

Use this guided or self-paced path to investigate three prepared scenarios in Microsoft Defender. You review existing evidence rather than run attacks or change shared resources.

**Tester draft:** The Windows exercises include observed click paths, prompt-panel screenshots, queries, and completion checks. The replacement macOS exercise uses the October 30 MCP investigation report. Final attendee-role rehearsal, Skillable reference values, owner approval, and refreshed-evidence checks remain required before event delivery.

## Prerequisites

- An assigned LAB683 environment and individual lab account supplied through the controlled lab experience.
- Browser access to the lab tenant's Microsoft Defender portal.
- Prepared scenario references supplied by the instructor or controlled lab instructions.

Do not use personal or production accounts. Do not put credentials in GitHub, screenshots, or investigation notes.

## Follow the investigation path

| Activity | Time | Primary experience |
|---|---|---|
| [Get started](00-get-started.md) | 5 minutes | Account and evidence orientation |
| [Discover agents and run the hunting warm-up](00-get-started.md#discover-the-local-agents) | 12 minutes | Local-agent inventory and source-identity correlation |
| [Investigate Windows XPIA](01-windows-xpia.md) | 17 minutes | Alert details and runtime prevention evidence |
| [Investigate Windows agent misalignment](02-agent-misalignment.md) | 22 minutes | Incident, process evidence, device events and timeline |
| [Investigate a macOS MCP execution chain](03-macos-runtime.md) | 15 minutes | Copilot-to-script chain, potential MCP configuration link, and protection-outcome limits |
| [Compare findings](#compare-your-findings) | 4 minutes | Evidence-based conclusions across all three scenarios |
| [Observe Agent 365 investigation context](optional-agent-365.md) | Extra credit | Available identity, registry, and risk context |

1. Complete **Get started**, then follow the three scenarios in order.
2. Keep findings in your own notes. Do not assign, classify, resolve, or otherwise edit shared incidents or alerts.
3. During the closing comparison, identify the user intent, untrusted input or dangerous behavior, agent attribution, and observed outcome for each scenario.
4. Complete extra credit only after the required investigations. It is outside the 75-minute schedule.
5. Sign out of the lab account and end the Skillable session when finished.

## Stay within the lab scope

Do not isolate devices, quarantine files, stop processes, launch Live Response, create indicators, or change policies. Response activities and response demonstrations are not part of this lab.

Reviewing existing protection and disruption evidence is allowed; initiating a response action is not.

The replacement Mac investigation uses alert, process, script, and inventory reference evidence. It is not approval to include macOS in the event demo. The lab team must confirm the owner readiness decision and rehearse this exact path with ordinary attendee access before delivery. If it cannot be delivered, an owner-approved alternative must be authored and rehearsed; inventory-only browsing is not a substitute.

## Compare your findings

Use the closing discussion to distinguish the evidence and outcomes across the three investigations.

1. For each scenario, identify the original task, suspicious behavior, agent/process attribution, and observed outcome.
2. Explain why the Windows XPIA and misalignment exercises are separate runs even though the devices share a display name.
3. Distinguish Windows prevention, recorded containment, and Mac detection with unestablished prevention. Explain why the Mac Blocked label alone does not prove discovery was prevented.
4. Identify one question Advanced Hunting answered and one prompt or script question that required portal or labeled reference evidence. Explain why a current MCP configuration match is not proof of historical tool invocation.
5. Sign out and end the Skillable session. Extra credit is optional and outside the required 75 minutes.

## Related content

- [Lab architecture](../docs/architecture.md)
- [Authoring and readiness plan](../docs/content-plan.md)
