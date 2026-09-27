# Version 1 VM build specification

LAB683 Version 1 is delivered through a Windows VM configured in Skillable Studio.

## Responsibility boundary

Skillable Studio configuration is not created by committing files to this folder. Lab profile identifiers, VM image selections, credentials, tenant identifiers, Microsoft Defender for Endpoint onboarding material, policy assignments, Microsoft Agent 365 environment settings, and private portal entry points must remain in Skillable Studio or the approved administration system.

This document records requirements for the operator building the Version 1 VM. It does not select an unsupported VM SKU, automate the build, or replace the [Skillable Studio setup guide](../docs/skillable-setup.md).

## Windows VM requirements

- TODO (lab administrator): Select and record the approved Windows version and build in the approved administration system.
- Choose CPU capacity that can run Visual Studio Code, GitHub Copilot CLI, the selected supported local AI agent, Defender protection, and browser-based investigation concurrently without disrupting the learner path.
- Choose RAM capacity for the combined workload and leave enough headroom for Defender scanning and the sanctioned scenario.
- Choose disk capacity for Windows, required software, updates, logs, and the sanctioned demonstration assets, with sufficient free space for reset and capture operations.
- Do not hardcode a VM family or SKU until the delivery and Skillable teams approve it.

## Networking and access requirements

- Provide internet access to the Microsoft and GitHub services required by the lab.
- Configure any approved proxy, DNS, firewall, or allowlist requirements in Skillable Studio or the VM image.
- Verify that Visual Studio Code, GitHub Copilot, GitHub Copilot CLI, the selected supported local AI agent, Microsoft Defender for Endpoint, and the Microsoft Defender portal can reach their required services.
- Restrict access to unrelated tenant resources, production systems, and other learners' environments.
- Do not place private endpoints, tenant identifiers, access tokens, or proxy credentials in this repository.

## Required software

- Visual Studio Code
- GitHub Copilot extension for Visual Studio Code
- GitHub Copilot CLI
- The selected supported local AI agent identified in the approved presenter and Skillable guidance
- A supported browser for the Microsoft Defender portal
- Microsoft Defender for Endpoint components required by the approved onboarding process

Pin approved versions in the controlled build record or Skillable configuration. Do not invent versions in this repository.

## Defender and runtime protection prerequisites

- Onboard the VM image to the authorized Microsoft Defender for Endpoint lab environment by using the approved administration process.
- Apply the approved Microsoft Defender for Endpoint policies, device grouping or tags, and learner investigation permissions.
- Configure the Microsoft Agent 365 and AI agent runtime protection prerequisites required by the official scenario.
- Confirm that the selected supported local AI agent is covered by the approved runtime protection configuration.
- Store onboarding packages, tenant details, policy identifiers, private portal links, and hunting content only in approved controlled systems.

## Reset and lifecycle requirements

- Start every learner assignment from a clean, isolated image or checkpoint.
- Configure reset and teardown so learner activity, cached sessions, temporary credentials, alert context, and personal notes do not carry into another assignment.
- Confirm that reset restores the software, onboarding readiness, sanctioned asset, and expected scenario starting state.
- Define the operator response when startup, reset, onboarding, portal access, or alert generation fails.

## Operator checklist before capture and publish

1. Apply current approved Windows updates and record the selected Windows version outside this repository.
2. Confirm that no production credentials, secrets, tokens, onboarding packages, tenant identifiers, private URLs, cached profiles, or learner data are present.
3. Verify that Visual Studio Code starts and that the GitHub Copilot extension is installed and enabled.
4. Verify that GitHub Copilot CLI starts through the learner-facing path.
5. Verify that the selected supported local AI agent starts and is the agent named in the approved guidance.
6. Verify Microsoft Defender for Endpoint onboarding and runtime protection readiness without capturing tenant details.
7. Run only the sanctioned scenario and confirm the expected Defender block event.
8. Open the Microsoft Defender portal with the learner role, investigate the alert, and confirm the approved threat-hunting results.
9. Test the [attendee instructions](../instructions/README.md) in both guided and self-paced use.
10. Reset the VM and confirm that it returns to the clean starting state.
11. Capture or publish the image through the approved Skillable Studio process, then perform a clean test launch.

## Security and automation restrictions

- Never include secrets or production credentials in the VM image, this repository, logs, screenshots, or learner instructions.
- Do not connect the lab to production deployments or production resources.
- Do not add build, onboarding, deployment, scenario, or cleanup scripts to this Version 1 specification.
- Complete VM and Lab Profile configuration in Skillable Studio and the approved administration systems, not through repository commits.

Review the [architecture](../docs/architecture.md) for component boundaries and the [Skillable Studio setup guide](../docs/skillable-setup.md) for profile configuration.
