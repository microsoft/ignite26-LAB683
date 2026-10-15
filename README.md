## Before you're done

This repo has been created for your Microsoft Ignite 2026 session. Here's how to get it ready.

**Easiest path — use the agent (recommended):**

- Open GitHub Copilot Chat and say `help me initialize repo`. The agent will walk you through getting the README populated.
- When you're ready to publish, say `help me finalize repo`. The agent will clean up unused folders, validate everything, and remove this "Before you're done" section and other extra stuff that attendees don't need to see.
- Curious how it works? Read the [agent workflow](.github/AGENT-WORKFLOW.md).

**Doing it manually?**

Fill in the sections below yourself, then:

- Delete any placeholder folders you don't need (`data/`, `infra/`, etc.)
- Delete this "Before you're done" section
- Delete `.github/agents/`, `.github/tests/`, `.github/copilot-instructions.md`, and `.github/AGENT-WORKFLOW.md` — these are template tooling, not part of your published repo

**Folder conventions:**

- Attendee step-by-step guidance goes in `instructions/`. If you use MkDocs or a docs site instead, put it in `docs/` and link to it from this README.
- Reference material and background reading go in `docs/`.
- You can add a `.devcontainer/` folder if needed.

---

<a name="start-building"></a>

<p align="center">
<img src="img/banner-ignite-26.png" alt="Microsoft Ignite 2026" width="100%"/>
</p>

# [Microsoft Ignite 2026](https://ignite.microsoft.com)

## 🔥LAB683: Secure local AI agents with end-to-end threat protection
### Session description

Investigate three prepared local AI agent security scenarios in Microsoft Defender: Windows cross-prompt injection (XPIA), Windows agent misalignment, and macOS runtime prompt injection. Follow alerts, agent context, process evidence, device events, and timelines, with Advanced Hunting used where it helps answer the investigation question.

#### Lab delivery model

This is a 75-minute, L300, browser-first investigation lab. Attendees use individually assigned accounts in the team's dedicated lab tenant and investigate pre-seeded evidence. Skillable is the intended delivery and secure credential-assignment experience; the lab team must validate its configuration before delivery.

No attendee endpoint provisioning, local agent installation, live attack generation, or Sentinel setup is required. Response actions, including isolation, remediation, Live Response, and policy changes, are out of scope. Optional extra credit observes Agent 365 elements of the investigation; it is not required to complete the lab.

**Content status:** Review draft, not a delivery-ready manual. Exact scenario entry points, evidence windows, screenshots, and attendee permissions still require validation in the LAB683 tenant. The macOS scenario has an October 30, 2026 readiness gate; MCP/tool-chain compromise is the fallback if the macOS investigation is not ready.

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
- Investigate macOS runtime activity and explain the evidence and platform limitations shown in the prepared scenario

### 💻 Technologies used

- Microsoft Defender for Endpoint
- Microsoft Defender portal and Advanced Hunting
- Windows and macOS local AI agent evidence
- Microsoft Agent 365 (optional observational extra credit)

### 📚 Continue your learning

Pick your next step based on your learning style:

| Resource | What you'll get |
|----------|-----------------|
| **[Ignite 2026 Next Steps](https://aka.ms/ignite26-next-steps)** | Additional session repos and materials from Microsoft Ignite 2026 |
| **[Microsoft AI Skills Navigator](https://aka.ms/ignite26-asn)** | Discover AI skills, learning paths, and resources for your next step |
| **[Microsoft Learn](https://aka.ms/ignite26-learn)** | Official documentation and guided learning paths on these topics |
| **[Microsoft Foundry Community](https://aka.ms/MicrosoftFoundryDiscord-Ignite26)** | Connect with other learners and experts in our Discord community |

### 🌟 Microsoft Learn MCP Server

<!-- Remove this section if the Microsoft Learn MCP Server is not relevant to the session. -->

The Microsoft Learn MCP Server gives your AI agent direct access to Microsoft's official documentation — grounded, up-to-date answers about the topics in this session.

**GitHub Copilot CLI** — Install with:

```shell
copilot plugin install microsoftdocs/mcp
```

**VS Code** — One-click install:  
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Microsoft_Learn_MCP-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect/mcp/install?name=microsoftdocs%2Fmcp)

For more information, visit the [Learn MCP Server repo](https://aka.ms/learnmcp).

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
