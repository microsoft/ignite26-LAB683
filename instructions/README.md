# Attendee instructions

Use these instructions during the guided lab or when repeating the lab at your own pace in an assigned Skillable environment.

## Lab boundaries

- Work only in the Windows VM assigned to you for LAB683.
- Use only the presenter-provided, sanctioned demonstration steps and assets.
- Do not substitute real attack payloads, production credentials, production tenants, or unrelated endpoints.
- Stop and ask the presenter or lab administrator for help if the VM, security connection, or demonstration state differs from the instructions.

## Understand the delivery model

Version 1 uses a Windows VM prepared in Skillable Studio. The VM image, lab duration, credentials, tenant connection, Microsoft Defender for Endpoint onboarding, Microsoft Agent 365 configuration, and sanctioned demonstration assets are configured by the lab administrator in Skillable Studio. They are not values that attendees set from this repository.

For background, review the [architecture](../docs/architecture.md). Lab administrators should use the separate [Skillable Studio setup guide](../docs/skillable-setup.md).

## Start the lab

1. Launch LAB683 from the event-provided Skillable entry point.
2. Wait for Skillable to report that the assigned Windows VM is ready.
3. Open the VM by using the connection method presented by Skillable.
4. Sign in with the temporary lab credentials supplied through the lab experience. Do not store those credentials in this repository or in personal notes.
5. Read any presenter announcement before continuing. It may identify a known delay or a session-specific starting state.

## Confirm the environment

Before beginning the scenario, verify each required tool:

- You are working in the assigned lab VM, not your local device.
- Open Visual Studio Code and confirm it starts normally.
- In Visual Studio Code, open the Extensions view and confirm the GitHub Copilot extension is installed and enabled. Do not sign in with a personal or production account.
- Open GitHub Copilot CLI by using the lab-provided shortcut or terminal instructions and confirm it starts without an installation or authentication error. Do not install or upgrade it.
- Open the selected supported local AI agent identified in the presenter guidance or Skillable learner instructions and confirm that its expected lab interface is available. Do not substitute a different agent.
- The Microsoft Agent 365 experience required by the presenter is available.
- The sanctioned demonstration asset identified by the presenter is present.

If any item is missing or reports an error, stop before running the scenario. Use the [troubleshooting steps](#troubleshoot-the-lab) or ask the lab team for help.

## Verify Defender for Endpoint onboarding

1. Open the lab-provided Microsoft Defender for Endpoint status view or shortcut.
2. Confirm that the assigned VM is shown as onboarded, connected, and ready for the lab.
3. Check only the device name and readiness state needed for this lab. Do not display, copy, record, or share tenant identifiers, device-group details, policy identifiers, onboarding packages, or private portal URLs.
4. If the VM is not onboarded or ready, stop and ask the presenter or lab administrator for help. Do not attempt to onboard it yourself.

## Establish the baseline

1. Open the local AI agent experience identified by the presenter.
2. Open the Microsoft Defender view provided in the lab environment.
3. Note the assigned VM name and the current time shown in the VM. Use these only to correlate activity during your lab session.
4. Confirm that no earlier learner activity is visible. If the VM appears to contain another learner's state, request a reset.

## Run the sanctioned scenario

1. Open the official [Microsoft Defender for Endpoint AI agent runtime protection walkthrough](https://learn.microsoft.com/en-us/defender-endpoint/defender-endpoint-demonstration-ai-agent-runtime-protection).
2. Follow only that official walkthrough and any presenter-sanctioned steps supplied for this lab.
3. Use only the supplied benign simulation or sanctioned demonstration asset. Never invent, create, download, substitute, or add malware or another payload.
4. If the official walkthrough and presenter guidance differ, stop and ask the presenter which sanctioned step to follow.
5. Observe how Microsoft Defender responds to the local AI agent activity.
6. Confirm that a Microsoft Defender block event appears and that the attempted activity does not continue.
7. Record the visible event time, protection action, and alert label for the investigation steps. Do not copy credentials, tokens, tenant identifiers, or other sensitive values.
8. Stop the scenario after confirming the expected block event. Do not modify or evade the protection configuration.

> [!IMPORTANT]
> This lab demonstrates defensive controls in an isolated, authorized environment. Do not recreate the scenario outside the assigned lab VM.

## Investigate the activity

1. Open the Microsoft Defender portal from the lab-provided shortcut or private entry point. Do not copy or share that entry point.
2. Open the alert associated with the block event by using the assigned VM name, event time, or alert label recorded earlier.
3. Investigate the alert by reviewing its summary, affected device, evidence, process details, and timeline.
4. Identify the selected local AI agent process and confirm the protection action shown by Microsoft Defender.
5. Open the portal's threat-hunting experience and perform threat hunting with the session-provided query or presenter-guided view.
6. Confirm that the hunting results correlate with the VM, event time, alert, and Defender block event. Do not expose tenant details in notes or screenshots.
7. Do not write or run an unsanctioned query intended to affect another device or environment.
8. Compare the evidence with the [architecture](../docs/architecture.md) and explain where detection, blocking, and investigation occur.

TODO (lab administrator): Add the exact investigation portal entry point and the approved hunting query location to the Skillable lab instructions or VM desktop.

## Complete the lab

1. Close any investigation and local AI agent windows.
2. Remove personal notes from the VM.
3. Use Skillable's end-lab or reset action when instructed.
4. Do not export the VM, security data, demonstration assets, or temporary credentials.

## Troubleshoot the lab

- **The VM is not ready:** Wait for the Skillable status to change to ready. If it does not, ask the lab team to check the assignment.
- **A required shortcut or tool is missing:** Do not install a replacement. Ask for a VM reset or a corrected assignment.
- **Microsoft Defender is not connected:** Stop the scenario and ask the lab administrator to verify onboarding and policy assignment.
- **The expected protection action does not appear:** Do not retry with a different asset. Confirm the baseline and ask the presenter whether the demonstration state needs a reset.
- **An investigation view is unavailable:** Confirm that you used the lab-provided account and entry point. Do not use a personal or production account.
