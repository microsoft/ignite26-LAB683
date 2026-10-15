---
title: Investigate Windows agent misalignment
description: Reconstruct dangerous agent behavior using prepared incident and endpoint evidence.
author: j0shbregman
ms.author: j0shbregman
ms.service: microsoft-defender-xdr
ms.topic: how-to
ms.custom: msecd-doc-authoring-1030
ms.date: 10/14/2026
ai-usage: ai-generated
#customer intent: As a SOC analyst, I want to reconstruct agent misalignment so that I can distinguish the intended task from dangerous behavior and observed impact.
---

# Investigate Windows agent misalignment

Trace a Windows local AI agent's departure from a benign user goal. Use the prepared incident, process evidence, device events, and timeline to reconstruct what happened rather than relying on a single alert or hunting query.

## Prerequisites

- Complete [Windows XPIA](01-windows-xpia.md).
- Obtain the approved goal context, incident reference, device reference, and evidence window.

**Review draft:** Research and the lab team must validate the exact event sequence and portal pivots. Discovery, credential access, and lateral movement are investigation themes, not claims that all three are present in the final dataset.

## Identify the departure from the user goal

1. Read the supplied legitimate task and its intended boundaries.
2. Open the supplied incident and review its related alerts and entities.
3. Identify the first evidenced behavior outside the task's boundaries.
4. Explain why that behavior is suspicious in this context. Keep your assessment separate from the product's detection label.

## Reconstruct the activity

1. Open the prepared process evidence and review the available parent-child relationships and command details.
2. Identify the evidence connecting the agent to the suspicious activity. Note gaps where a process relationship alone does not establish agent causality.
3. Open the device timeline using the validated lab pivot and apply the supplied evidence window.
4. Correlate relevant device events with the alerts and process evidence.
5. Use the approved Advanced Hunting query, if supplied, to answer a specific remaining question rather than repeating the entire investigation in KQL.

## Assess the observed impact

1. Build a short sequence: intended task, first dangerous behavior, subsequent observed activity, and result.
2. Identify which actions are shown to have executed and which are only attempted or inferred.
3. Explain the scope supported by the evidence. Do not assume another user, device, or session is affected without corroboration.

You have completed this scenario when you can explain where the agent departed from the task and support the sequence and impact with evidence from multiple Defender views. Do not isolate the device or edit the shared incident.

## Next step

> [!div class="nextstepaction"]
> [Investigate macOS runtime activity](03-macos-runtime.md)
