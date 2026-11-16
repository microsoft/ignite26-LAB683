<a name="start-building"></a>

<p align="center">
<img src="img/banner-ignite-26.png" alt="Microsoft Ignite 2026" width="100%"/>
</p>

# [Microsoft Ignite 2026](https://ignite.microsoft.com)

## 🔥LAB683: Secure local AI agents with end-to-end threat protection
### Session description

AI agents can read files, run commands, and connect to tools. What happens when they follow malicious instructions or act beyond the user's intent?

Step into the role of a security analyst investigating AI agent activity on Windows and macOS. Discover the agents, follow the alert evidence, and use Advanced Hunting to answer questions the alert alone cannot resolve. Investigate an attempted credential theft through prompt injection, a document-search agent that starts scanning the network, and suspicious code execution behind a local MCP tool.

You'll work in a preconfigured environment where the suspicious activity has already taken place. Your job is to follow the alerts, reconstruct the agents' actions, and determine what the evidence says about Defender's response.

#### Lab delivery model

This is a 75-minute, L300, browser-first investigation lab. Use an individually assigned account in the lab environment. You do not need a Mac, a local agent installation, or API credentials.

No attendee endpoint provisioning, local agent installation, live attack generation, or Sentinel setup is required. Response actions, including isolation, remediation, Live Response, and policy changes, are out of scope. Optional extra credit observes Agent 365 elements of the investigation; it is not required to complete the lab.

The [attendee path](instructions/README.md) combines portal investigation and focused hunting in each scenario: **ask a question, inspect the evidence, hunt for supporting activity, and explain your findings**. Owners can find access, evidence-refresh, and rehearsal requirements in the [delivery plan](docs/content-plan.md).

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

- Discover local AI agents and distinguish their configuration from their observed activity
- Investigate Windows and macOS agent threats using alerts, prompt or script evidence, and process timelines
- Use Advanced Hunting to measure suspicious behavior and explain what was detected, executed, or prevented

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
