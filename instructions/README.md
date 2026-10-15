# Investigate local AI agent threats

Use this guided or self-paced path to investigate three prepared scenarios in Microsoft Defender. You review existing evidence rather than run attacks or change shared resources.

**Review draft:** The lab team is still validating scenario links, screenshots, evidence windows, and permissions in the LAB683 tenant. This draft describes the investigation tasks; it is not yet an exact-click delivery manual.

## Prerequisites

- An assigned LAB683 environment and individual lab account supplied through the controlled lab experience.
- Browser access to the lab tenant's Microsoft Defender portal.
- Prepared scenario references supplied by the instructor or controlled lab instructions.

Do not use personal or production accounts. Do not put credentials in GitHub, screenshots, or investigation notes.

## Follow the investigation path

| Activity | Time | Primary experience |
|---|---|---|
| [Get started](00-get-started.md) | 5 minutes | Account and evidence orientation |
| [Investigate Windows XPIA](01-windows-xpia.md) | 17 minutes | Alert details and runtime prevention evidence |
| [Investigate Windows agent misalignment](02-agent-misalignment.md) | 22 minutes | Incident, process evidence, device events and timeline |
| [Investigate macOS runtime activity](03-macos-runtime.md) | 22 minutes | Prepared macOS evidence and cross-platform comparison |
| Compare findings | 9 minutes | Evidence-based conclusions across all three scenarios |
| [Observe Agent 365 investigation context](optional-agent-365.md) | Extra credit | Available identity, registry, and risk context |

1. Complete **Get started**, then follow the three scenarios in order.
2. Keep findings in your own notes. Do not assign, classify, resolve, or otherwise edit shared incidents or alerts.
3. During the closing comparison, identify the user intent, untrusted input or dangerous behavior, agent attribution, and observed outcome for each scenario.
4. Complete extra credit only after the required investigations. It is outside the 75-minute schedule.
5. Sign out of the lab account and end the Skillable session when finished.

## Stay within the lab scope

Do not isolate devices, quarantine files, stop processes, launch Live Response, create indicators, or change policies. Response activities and response demonstrations are not part of this lab.

The third scenario remains subject to the macOS readiness gate. If it is not ready, the lab team will publish an MCP/tool-chain compromise replacement before delivery. Do not substitute inventory-only browsing for a runtime investigation.

## Related content

- [Lab architecture](../docs/architecture.md)
- [Authoring and readiness plan](../docs/content-plan.md)
