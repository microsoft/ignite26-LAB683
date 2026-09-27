# Skillable Studio setup

This guide is for the LAB683 lab administrator. It describes the Version 1 delivery configuration without placing environment-specific or sensitive values in the repository.

Configuration is completed in Skillable Studio, not by repository commits. The repository documents the required learner experience; an administrator applies and publishes the corresponding settings in Skillable Studio.

## Keep configuration in the correct location

| Store in Skillable Studio or the approved administration system | Commit to this repository |
|---|---|
| Lab profile and template identifiers | Attendee instructions |
| VM image selection and version | Architecture documentation |
| Temporary learner credentials | Non-sensitive source and data usage notes |
| Tenant and subscription identifiers | Approved links between repository documents |
| Microsoft Defender for Endpoint onboarding material | No secrets, credentials, onboarding packages, or private identifiers |
| Device group, tag, policy, and role assignments | No real attack payloads |
| Private portal entry points | Safe, sanctioned-demo wording |
| Sanctioned demonstration asset placement and access controls | A description of where an approved asset is expected |

Do not copy administrator-owned values into Markdown, source files, issue comments, or commit history.

## Understand the setup

A Lab Profile defines what a learner launches and how the lab behaves. For Version 1, create or update a Lab Profile in Skillable Studio that provides one isolated Windows VM to each learner. Select an approved custom image when the lab requires software and security configuration beyond the available base Windows image.

Use the Skillable Studio fields and options available to your organization. This guide intentionally does not name tenant-specific screens, subscriptions, identifiers, or credentials.

## Complete the lab profile

- TODO (lab administrator): Record the Skillable lab profile identifier in the approved administration system.
- TODO (lab administrator): Select an approved Windows VM or custom image and record its version in the approved administration system.
- TODO (lab administrator): Set the lab duration, startup allowance, extension policy, and teardown behavior.
- TODO (lab administrator): Configure the attendee connection method and temporary credential delivery.
- TODO (lab administrator): Configure the reset path and confirm that each learner receives an isolated starting state.

## Add learner instructions

1. Add a short welcome that identifies LAB683 and explains that each learner receives an isolated, preconfigured Windows VM.
2. Tell learners how to launch and connect to the VM using the connection method configured for the profile.
3. Link or copy the approved learner path from the [attendee instructions](../instructions/README.md).
4. Include the lab boundaries, sanctioned-scenario warning, expected Defender block event, investigation path, and cleanup steps.
5. Keep tenant-specific URLs, identifiers, credentials, and support-only notes in controlled Skillable fields or the approved administration system.

## Configure networking and access

- Allow the VM to reach only the internet and Microsoft service endpoints required by Visual Studio Code, GitHub Copilot, GitHub Copilot CLI, the selected supported local AI agent, Microsoft Defender for Endpoint, and the Microsoft Defender portal.
- Apply the approved proxy, firewall, DNS, and access configuration for the lab environment without documenting private values in this repository.
- Provide the learner role only the Defender portal access needed to investigate the alert and perform the approved threat hunting.
- Confirm that learners cannot reach production credentials, unrelated tenant resources, or another learner's VM.

## Configure the VM lifecycle and reset

- Start each assignment from the approved clean image or checkpoint.
- Give each learner one isolated VM and prevent state from being shared between assignments.
- Configure end-lab, expiration, teardown, and reset behavior according to the event's approved retention policy.
- Verify that a reset removes learner activity, personal notes, cached sessions, temporary credentials, and scenario state before the next assignment.
- Document the learner-visible reset action and the support escalation path in Skillable.

## Prepare the security environment

- TODO (lab administrator): Identify the authorized lab tenant or equivalent security environment outside this repository.
- TODO (lab administrator): Onboard the VM image to Microsoft Defender for Endpoint using the approved administration process.
- TODO (lab administrator): Assign the required protection policies, device group or tags, and attendee investigation permissions.
- TODO (lab administrator): Configure the Microsoft Agent 365 experience required for the session.
- TODO (lab administrator): Add the approved investigation portal entry point to the Skillable instructions or VM desktop.
- TODO (lab administrator): Place the approved threat-hunting query in the controlled lab experience.

Never commit an onboarding package, tenant identifier, access token, temporary password, private portal URL, or exported security data.

## Prepare the VM

- TODO (lab administrator): Install or stage the exact approved versions of the local AI tooling listed for the session.
- TODO (lab administrator): Add clear desktop shortcuts for the local AI agent experience, security status, investigation entry point, and attendee instructions.
- TODO (lab administrator): Place only the sanctioned demonstration asset in the controlled location expected by the lab flow.
- TODO (lab administrator): Confirm that no production credentials, cached user profiles, or earlier learner data are present in the image.
- TODO (lab administrator): Configure the expected starting state and a reliable reset checkpoint.

## Configure the sanctioned scenario

- TODO (lab administrator): Obtain approval for the demonstration asset and record the approving owner outside this repository.
- TODO (lab administrator): Document the expected Microsoft Defender protection action and alert label in the controlled presenter notes.
- TODO (lab administrator): Define the expected evidence and hunting result used to confirm success.
- TODO (lab administrator): Add a stop condition so attendees end the scenario after the expected block or containment action.
- TODO (lab administrator): Provide a fallback walkthrough that uses approved screenshots or prepared evidence if the live security signal is delayed.

Do not provide real attack payloads or instructions for weakening, bypassing, or evading the configured controls.

## Validate before publishing

1. Use Skillable Studio's test-launch capability to start a clean assignment through the same path attendees will use.
2. Confirm that the VM reaches the ready state within the planned startup allowance.
3. Confirm that temporary credentials work only for the intended lab access.
4. Verify that Visual Studio Code, the GitHub Copilot extension for VS Code, GitHub Copilot CLI, the selected supported local AI agent, Microsoft Defender for Endpoint status, and the Microsoft Agent 365 experience are ready.
5. Run the sanctioned scenario once and confirm the expected protection action.
6. Confirm that the alert and approved hunting evidence are available to the attendee role.
7. End or reset the assignment and verify that attendee activity and credentials do not persist.
8. Test the [attendee instructions](../instructions/README.md) from a clean assignment.

## Publish and operate Version 1

- TODO (lab administrator): Record the approved Skillable profile version and VM image version outside this repository.
- TODO (lab administrator): Assign the presenter and lab-support escalation contacts in Skillable.
- TODO (lab administrator): Define the response for VM startup, onboarding, portal-access, and delayed-alert failures.
- TODO (lab administrator): Confirm the rollback profile or prior approved image before publishing Version 1.
- TODO (lab administrator): Confirm teardown and retention behavior with the event and security owners.

Repository commits update the documentation and approved session materials. A Skillable Studio administrator must separately publish profile, image, access, and environment changes.
