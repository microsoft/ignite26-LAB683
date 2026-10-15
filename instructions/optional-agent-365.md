---
title: Observe Agent 365 investigation context
description: Inspect available identity, registry, and risk context without changing agent or policy state.
author: j0shbregman
ms.author: j0shbregman
ms.service: microsoft-defender-xdr
ms.topic: how-to
ms.custom: msecd-doc-authoring-1030
ms.date: 10/14/2026
ai-usage: ai-generated
#customer intent: As a SOC analyst, I want to observe Agent 365 investigation context so that I can relate endpoint evidence to available agent identity and risk information.
---

# Observe Agent 365 investigation context

Extend one of the completed investigations by observing available Agent 365 elements. This extra-credit activity explores identity, registry, and risk context without changing policies or agent state.

## Prerequisites

- Complete the three required investigations.
- Use only the scenario and observational pivots approved by the lab team.
- Allow additional time outside the required 75 minutes.

**Review draft:** Registry and risk pivots still require tenant validation. Where a capability is unavailable, use only approved screenshots or recorded evidence labeled as reference material. Extra credit is not required for lab completion.

## Inspect the available agent identity

1. Open the approved scenario's agent page using its validated link.
2. Review the source agent identity and any Entra agent identity displayed.
3. Note which identity values are present or absent. Do not treat source, Entra, session, or registry identifiers as interchangeable.
4. Describe how the displayed identity relates to the endpoint investigation, using only the verified link.

## Observe registry and risk context

1. Follow the approved Agent 365 registry or risk pivot if one is available for this scenario.
2. Compare the displayed agent context with the Defender investigation. Record only relationships supported by the prepared evidence.
3. If a pivot is unavailable, inspect the approved reference material or record the limitation. Do not create a registration or change access to make the pivot work.
4. Explain what the additional context contributes and what it does not establish about the local agent's activity.

You have completed extra credit when you can distinguish endpoint evidence from identity, registry, and risk context. Do not change Conditional Access, revoke access, disable agents, or perform any response action.

## Related content

- [AI agent inventory](https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/ai-agent-inventory)
- [Transition agent security to Agent 365](https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/transition-agent-security-to-agent-365)
