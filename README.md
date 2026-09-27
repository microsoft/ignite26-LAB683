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

Set up a demonstration VM to explore runtime protection for local AI agents. See Microsoft Defender block a threat, then use threat hunting and investigation to understand what happened.

#### Version 1 delivery model

Version 1 runs in a Windows VM prepared for this lab in Skillable Studio. The lab administrator configures the VM image, access, Microsoft Defender for Endpoint connection, Microsoft Agent 365 experience, and sanctioned demonstration assets in Skillable Studio; attendees do not provision those values from this repository.

Use only the assigned lab VM and the presenter-provided, sanctioned demonstration flow. Do not use production tenants, production credentials, or unapproved payloads.

### 🚀 Getting started

#### In a guided session

If you're following along during a live session:

1. Launch the assigned LAB683 environment in Skillable
2. Open the prepared Windows VM and confirm the required tooling is ready
3. Follow the [attendee instructions](instructions/README.md)

#### On your own

If you're learning at your own pace:

1. Launch an assigned LAB683 environment in Skillable
2. Open the prepared Windows VM; do not substitute a personal or production environment
3. Follow the [attendee instructions](instructions/README.md)

#### Session resources

- [Attendee instructions](instructions/README.md)
- [Architecture](docs/architecture.md)
- [Skillable Studio setup](docs/skillable-setup.md)
- [Infrastructure notes](infra/README.md)
- [Source materials](src/README.md)
- [Data materials](data/README.md)

### 🎯 Learning outcomes

By the end of this session, you will be able to:

- Configure a Windows VM environment for local AI agent runtime protection testing
- Observe Microsoft Defender block or contain malicious AI-agent behavior at runtime
- Investigate alerts and perform threat hunting to understand the attack path and impact

### 💻 Technologies used

- Microsoft Defender for Endpoint
- Microsoft Agent 365
- Windows virtual machine
- GitHub Copilot
- GitHub Copilot CLI
- Visual Studio Code with the GitHub Copilot extension

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
