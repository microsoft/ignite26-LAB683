# Prepare the Skillable investigation experience

This owner guide describes the intended browser-first delivery model. It does not claim that secure account assignment or the Skillable profile is already configured.

## Prepare access

1. Select the approved LAB683 delivery profile with the Skillable team. A per-learner attack VM is not a requirement.
2. Provide an individual account for each attendee in the team's dedicated lab tenant.
3. Configure secure credential assignment through the controlled lab experience and validate the actual token or assignment mechanism. Do not reuse another lab's administrator credential token.
4. Assign only the access needed for the investigation tasks. Validate that the account can read the intended evidence and run the approved hunting queries.
5. Define session sign-out, credential expiration, browser-session cleanup, and support procedures outside GitHub.

Keep passwords, account rosters, tenant identifiers, profile identifiers, onboarding packages, and private portal links in approved administration systems.

## Prepare the instructions

1. Keep the [attendee path](../instructions/README.md) aligned with the controlled Skillable version. The public pages now reflect the numbered sections, customer introductions, exact navigation, and findings used in the lab. Convert GitHub images and expandable details to Skillable's supported image paths and native Hint/Note syntax; do not paste GitHub HTML into Skillable without checking its rendering.
2. Supply controlled scenario links and a direct Local agents inventory fallback. Public exercises include alert titles, UTC windows, and process locators; learners copy device IDs from the portal. If evidence is refreshed, update all public query windows/process references and controlled links together.
3. Set the required activity duration to 75 minutes. Label sections 17-24 as an optional macOS bonus of about 20 minutes only if the existing timer permits it. Agent 365 observations remain optional extra credit.
4. Explain that evidence is pre-seeded and shared. Learners do not run attacks, change incident state, or perform response actions.
5. Provide a clear help path for sign-in failures, unavailable evidence, or missing permissions.

Keep the required timing at 5 minutes sign-in, 10 discovery, 25 XPIA, 30 misalignment, and 5 comparison. Put core comparison and completion before the optional macOS investigation. Do not append unrelated endpoint onboarding, policy configuration, incident mutation, or live attack exercises.

The controlled version uses a WIN1 selection token, conditional Ctrl+Alt+Delete action, assigned-account tokens, and native Hint/Note boxes. Keep Windows and Defender credentials separate. Preserve these only in the approved delivery profile; do not copy credentials, private links, or resource identifiers into GitHub.

## Prepare the evidence

1. Prepare Windows XPIA and Windows misalignment evidence before the session.
2. Validate the optional macOS MCP execution-chain path in the [content plan](content-plan.md). Supply approved run evidence, script-event locators, configuration observations, and exact action targets/results; do not reuse the earlier poisoned-brief references.
3. Confirm evidence remains available through all event sessions. Account for rolling time filters, retention, and delayed ingestion.
4. Prepare approved static or recorded fallback evidence where needed, clearly labeled as such.
5. Validate optional Agent 365 pivots independently of the required Defender path.

## Rehearse as an attendee

1. Launch a clean assignment using an ordinary attendee account, not an administrator session.
2. Confirm the account opens the correct tenant and all supplied scenario references resolve.
3. Walk every instruction with Playwright in read-only mode and record actual navigation, visible labels, expected evidence, and supported tabs.
4. Finish the discovery foundation, both Windows investigations, and their comparison within 75 minutes without entering the macOS bonus.
5. Separately test the stay-signed-in bonus path and confirm it and Agent 365 extra credit can be skipped without affecting completion.
6. Sign out, end the assignment, and verify another attendee cannot inherit the previous browser session.
7. Confirm account capacity and concurrent portal access with the delivery team before publishing.

Publishing GitHub instructions does not publish a Skillable profile or configure tenant access.

The November 17 authoring walkthrough verified the Windows credential branch, the four script rows before the LSASS prevention event, its quarantine/Success fields, and the original sales-document request. It did not validate the assigned-student experience. Rehearse all images and Hint/Note boxes, token resolution, permissions, clipboard transfer, value-cell result opening, and all four custom date/time fields in the actual WIN1 assignment before delivery. Test the preset-reset workaround if Custom range is stuck.
