# Architecture

## Version 1 overview

LAB683 Version 1 uses Skillable to provide one isolated, preconfigured Windows VM per learner. The VM provides the environment for the local AI agent workflow, Microsoft Defender for Endpoint protection, Microsoft Agent 365 experience, and sanctioned demonstration assets used during the lab.

This repository is the source of truth for attendee instructions and setup documentation. It does not contain the Skillable lab profile, temporary credentials, tenant identifiers, production configuration, or real attack payloads.

A shared Microsoft tenant supplies Microsoft Defender portal access and the protection policies required by the lab. Tenant-specific access, identifiers, policies, and onboarding material remain in the approved administration systems and are not stored in this repository.

## Components

| Component | Purpose | Configuration location |
|---|---|---|
| Skillable Studio lab profile | Assigns and controls the attendee lab experience | Skillable Studio |
| Windows VM | Hosts the local AI tooling and sanctioned scenario | VM image selected in Skillable Studio |
| Local AI agent tooling | Runs the guided local agent workflow | VM image and lab instructions |
| Microsoft Defender for Endpoint | Observes and protects the assigned VM at runtime | Lab security environment and VM onboarding |
| Microsoft Agent 365 | Supports the session's agent protection experience | Lab environment |
| Investigation and hunting experience | Presents alerts, timelines, and approved hunting views | Lab security environment |
| This repository | Provides attendee steps, architecture context, and delivery notes | Git commits |

## Version 1 scope

Version 1 does not include:

- Cloud Slice
- Learner-created Azure resources
- Automated tenant provisioning
- Secrets, credentials, onboarding packages, or private tenant details in the repository
- Production deployment or use of production environments

## Activity flow

1. Skillable assigns an attendee an isolated Windows VM.
2. The attendee confirms that the local AI tooling and security connection are ready.
3. The attendee runs only the presenter-provided, sanctioned demonstration flow.
4. Microsoft Defender for Endpoint observes the runtime activity and applies the configured protection.
5. The attendee uses the lab-provided investigation and hunting experience to review the resulting evidence.
6. The attendee ends or resets the lab through Skillable.

## Trust boundaries

- **Attendee boundary:** The attendee works only inside the assigned VM and uses temporary access supplied by the lab.
- **Skillable boundary:** Skillable Studio controls VM assignment, timing, connection, reset, and teardown.
- **Security boundary:** The lab's Microsoft Defender for Endpoint and Microsoft Agent 365 configuration belongs to the authorized demonstration environment, not a learner's personal or production environment.
- **Repository boundary:** Git commits contain documentation and approved session materials only. They must not contain credentials, tenant identifiers, onboarding packages, private portal links, or sensitive telemetry.

## Configuration ownership

The [Skillable Studio setup guide](skillable-setup.md) lists administrator-owned values. Those values remain in Skillable Studio or the approved lab administration system. Repository updates should include only reusable instructions and approved, non-sensitive session assets.

## Safety model

The scenario is a sanctioned defensive demonstration. Attendees use only the supplied benign simulation or approved demonstration asset, stop after the expected protection action, and investigate the generated evidence. The repository intentionally provides no real attack payload and no steps for bypassing security controls.
