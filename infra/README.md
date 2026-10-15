# Prepare the lab evidence environment

The lab team prepares Windows and macOS evidence in a dedicated tenant. Attendees use the browser to investigate; they do not build endpoints or run attack simulations.

This specification supersedes the earlier per-learner Windows VM build requirements. It does not select a runtime, image, VM SKU, or provisioning system.

## Prepare the endpoints and evidence

1. Record approved endpoint builds, local agent versions, onboarding, protection configuration, and evidence-generation procedures in controlled operator material.
2. Generate approved Windows XPIA evidence with a recorded prevention outcome.
3. Generate Windows misalignment evidence that connects benign user intent to dangerous agent activity and attributable endpoint events.
4. Prepare macOS runtime evidence and validate alert emission, agent attribution where available, and the attendee portal journey.
5. Prepare the MCP/tool-chain compromise fallback if the macOS readiness gate is not met.
6. Record stable scenario references and evidence windows in controlled delivery instructions.

Use approved lab simulations only. Do not commit payloads, onboarding material, credentials, private identifiers, or raw endpoint exports.

## Maintain the shared investigation state

- Keep scenario evidence available for the full delivery period.
- Validate permissions with ordinary attendee accounts.
- Ensure time filters and evidence refresh do not invalidate the instructions.
- Keep scenario reset and maintenance separate from attendee activities.
- Do not require isolation, process termination, quarantine, Live Response, indicators, or policy changes.
- Provide a recovery procedure for missing evidence or failed account access in controlled operator notes.

## Related content

- [Lab architecture](../docs/architecture.md)
- [Skillable setup](../docs/skillable-setup.md)
- [Authoring and readiness plan](../docs/content-plan.md)
