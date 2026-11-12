<a name="start-building"></a>

<p align="center">
<img src="img/banner-ignite-26.png" alt="Microsoft Ignite 2026" width="100%"/>
</p>

# [Microsoft Ignite 2026](https://ignite.microsoft.com)

## 🔥LAB683: Secure local AI agents with end-to-end threat protection
### Session description

Investigate three prepared local AI agent security scenarios in Microsoft Defender: Windows cross-prompt injection (XPIA), Windows agent misalignment, and a macOS MCP execution chain. Follow alerts, agent context, process evidence, device events, and timelines, with Advanced Hunting used where it helps answer the investigation question.

#### Lab delivery model

This is a 75-minute, L300, browser-first investigation lab. Attendees use individually assigned accounts in the team's dedicated lab tenant and investigate pre-seeded evidence. Skillable is the intended delivery and secure credential-assignment experience; the lab team must validate its configuration before delivery.

No attendee endpoint provisioning, local agent installation, live attack generation, or Sentinel setup is required. Response actions, including isolation, remediation, Live Response, and policy changes, are out of scope. Optional extra credit observes Agent 365 elements of the investigation; it is not required to complete the lab.

**Content status:** Tester draft with investigation guidance, sanitized Windows evidence screenshots, and hunting queries. The final exercise now uses the October 30 macOS MCP investigation report instead of the earlier poisoned brief. It traces synthetic discovery, qualifies the MCP configuration link, and leaves prevention unestablished despite the portal's Blocked label. This content change does not approve macOS for event delivery: owner approval, attendee permissions, controlled references, evidence retention, and full-session timing still require rehearsal.

### 🚀 Getting started

#### In a guided session

If you're following along during a live session:

1. Launch the assigned LAB683 environment in Skillable
2. Open the supplied browser experience and sign in with your assigned lab account
3. Follow the [attendee instructions](instructions/README.md)

#### On your own

If you're learning at your own pace:

1. Launch an assigned LAB683 environment in Skillable
2. Use the supplied browser experience and assigned lab account, not a personal or production tenant
3. Follow the [attendee instructions](instructions/README.md)

#### Session resources

- [Attendee instructions](instructions/README.md)
- [Authoring and readiness plan](docs/content-plan.md)
- [Architecture](docs/architecture.md)
- [Skillable Studio setup](docs/skillable-setup.md)
- [Infrastructure notes](infra/README.md)
- [Source materials](src/README.md)
- [Data materials](data/README.md)

### 🎯 Learning outcomes

By the end of this session, you will be able to:

- Investigate Windows XPIA evidence and distinguish a recorded prevention outcome from an attempted attack
- Reconstruct Windows agent misalignment by correlating alerts, process evidence, and device timeline activity
- Trace a macOS MCP-related execution chain and distinguish configuration, observed behavior, and protection-outcome evidence

### 💻 Technologies used

- [Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/)
- [Microsoft Defender portal](https://learn.microsoft.com/en-us/defender-xdr/microsoft-365-defender-portal) and [Advanced Hunting](https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-overview)
- [Windows](https://learn.microsoft.com/en-us/windows/) and macOS local AI agent evidence
- [Microsoft Agent 365](https://learn.microsoft.com/en-us/microsoft-agent-365/) (optional observational extra credit)

### 📚 Continue your learning

Pick your next step based on your learning style:

| Resource | What you'll get |
|----------|-----------------|
| **[Ignite 2026 Next Steps](https://aka.ms/ignite26-next-steps)** | Additional session repos and materials from Microsoft Ignite 2026 |
| **[Microsoft AI Skills Navigator](https://aka.ms/ignite26-asn)** | Discover AI skills, learning paths, and resources for your next step |
| **[Microsoft Learn](https://aka.ms/ignite26-learn)** | Official documentation and guided learning paths on these topics |
| **[Microsoft Foundry Community](https://aka.ms/MicrosoftFoundryDiscord-Ignite26)** | Connect with other learners and experts in our Discord community |

### 👥 Content owners

<table>
<tr>
    <td align="center"><a href="http://github.com/j0shbregman">
        <img src="https://github.com/j0shbregman.png" width="100px;" alt="Josh Bregman"/><br />
        <sub><b>Josh Bregman</b></sub></a><br />
            <a href="https://github.com/j0shbregman" title="talk">📢</a>
    </td>
</tr></table>

### ⚖️ Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft trademarks or logos is subject to and must follow [Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general).

Any use of third-party trademarks or logos are subject to those third-party's policies.
