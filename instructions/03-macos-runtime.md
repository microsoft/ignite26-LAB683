---
title: Investigate macOS runtime activity
description: Review prepared macOS prompt-injection evidence and compare it with the Windows investigation.
author: j0shbregman
ms.author: j0shbregman
ms.service: microsoft-defender-xdr
ms.topic: how-to
ms.custom: msecd-doc-authoring-1030
ms.date: 10/14/2026
ai-usage: ai-generated
#customer intent: As a SOC analyst, I want to investigate macOS runtime evidence so that I can explain its outcome and platform-specific evidence limits.
---

# Investigate macOS runtime activity

Review a prepared macOS runtime/XPIA investigation in Microsoft Defender. Compare the available evidence with Windows while distinguishing demonstrated behavior from capabilities that have not been validated.

## Prerequisites

- Complete [Windows agent misalignment](02-agent-misalignment.md).
- Obtain the prepared macOS alert, device reference, and evidence window.
- Confirm the lab team has approved this scenario for delivery.

**Readiness-gated draft:** End-to-end macOS alert evidence and exact portal steps are not yet validated for LAB683. The go/no-go deadline is October 30, 2026. If the scenario is not ready, the lab team will publish the MCP/tool-chain compromise replacement. Inventory-only browsing does not complete this scenario.

## Examine the macOS runtime evidence

1. Open the supplied macOS alert or incident.
2. Confirm the affected device and event time match the prepared scenario.
3. Review the available runtime protection result and supporting evidence.
4. Identify the attempted redirection and state whether the recorded outcome indicates prevention, detection, or an unresolved result.

## Compare the investigation surfaces

1. Follow the validated macOS device and timeline pivots supplied in the lab instructions.
2. Correlate the available events with the alert's time window.
3. Open an agent entity only if the chosen build and alert actually expose one. Do not assume Windows agent linking or prompt/tool views are available on macOS.
4. Compare the evidence with scenario 1: what can you establish on each platform, and what cannot you establish from the supplied data?

## Summarize your findings

1. Describe the attempted behavior and recorded protection outcome.
2. Identify the strongest evidence connecting the activity to the Mac and, where supported, the agent.
3. State any attribution or telemetry limits without treating missing data as proof of safety.

You have completed this scenario when you can support the macOS investigation outcome and explain its evidence limits. No Mac provisioning, live attack, or response action is required.

## Next step

> [!div class="nextstepaction"]
> [Return to the closing comparison in the attendee path](README.md)

## Related content

- [Observe Agent 365 investigation context](optional-agent-365.md)
