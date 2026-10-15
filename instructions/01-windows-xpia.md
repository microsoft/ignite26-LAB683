---
title: Investigate Windows XPIA evidence
description: Review a prepared Windows runtime prompt-injection investigation in Microsoft Defender.
author: j0shbregman
ms.author: j0shbregman
ms.service: microsoft-defender-xdr
ms.topic: how-to
ms.custom: msecd-doc-authoring-1030
ms.date: 10/14/2026
ai-usage: ai-generated
#customer intent: As a SOC analyst, I want to investigate Windows XPIA evidence so that I can explain the attempted deviation and observed prevention outcome.
---

# Investigate Windows XPIA evidence

Investigate a prepared cross-prompt injection (XPIA) scenario in which untrusted content attempts to redirect a Windows local AI agent. Use the alert and supporting evidence to explain what was attempted and what runtime protection prevented.

## Prerequisites

- Complete [Get started](00-get-started.md).
- Obtain the scenario's alert or incident reference and evidence time window from the controlled lab instructions.

**Review draft:** The lab team must supply the exact alert, screenshots, and validated pivots. Do not run a prompt-injection simulation yourself.

## Examine the runtime alert

1. Open the supplied Windows XPIA alert or incident in Microsoft Defender.
2. Review the summary, event time, affected device, and available evidence.
3. Examine the prepared user goal and untrusted content provided for this scenario.
4. Identify the instruction that attempts to redirect the agent away from the user's goal. Use displayed prompt or tool context only where it is available.
5. Identify the recorded protection result. Distinguish an attempted operation from one shown to have executed.

## Correlate the agent and endpoint evidence

1. Review the agent entity if the alert provides one. Otherwise use the prepared device and process evidence; do not assume every alert has an agent link.
2. Follow the validated device or process pivot supplied in the lab instructions.
3. Compare timestamps and the available events with the recorded block. State what the evidence supports and what remains unknown.
4. If an approved hunting query is supplied, use its scenario window and correlate the results with the alert. A missing result is not by itself proof that an action never occurred.

## Explain your conclusion

1. Describe the legitimate user goal and the attempted redirection.
2. Cite the evidence connecting the activity to the device and agent, including any attribution limits.
3. State the recorded prevention outcome and whether supporting evidence shows subsequent execution.

You have completed this scenario when you can explain the attempted deviation and observed protection result without treating the alert title as proof of impact. No response action is required.

## Next step

> [!div class="nextstepaction"]
> [Investigate Windows agent misalignment](02-agent-misalignment.md)

## Related content

- [AI agent detection and protection](https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/ai-agent-detection-protection)
