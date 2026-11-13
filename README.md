<a name="start-building"></a>
 
<p align="center">
<img src="img/banner-ignite-26.png" alt="Microsoft Ignite 2026" width="100%"/>
</p>

# [Microsoft Ignite 2026](https://ignite.microsoft.com)

## 🔥LAB721: Hands-on with the resiliency in Azure: Assess, recommend, recover
### Session description

In this hands-on lab, experience Azure resiliency across availability, data resiliency, and cyber recovery. Define resiliency goals for a sample workload, assess readiness against zonal and regional failures, identify gaps against RTO/RPO targets, and apply guided recommendations to improve resiliency. Configure data protection using Azure Backup on a variety of workloads and then perform clean-room recovery to restore trusted data after an attack and leave with a practical, repeatable approach using Azure resiliency capabilities and AI-assisted guidance.

### 🚀 Getting started

#### In a guided session

If you're following along during a live session:

You will simulate the journey of Caldova, a financial services firm, launching its payments application, **CaldovaPayApp**, on Azure with a focus on:

- Infrastructure Resiliency
- Data Resiliency
- Cyber Recovery
  
See [`instructions/`](instructions/README.md) for the step by step guidance for the lab.

#### On your own

If you're learning at your own pace:

1. Clone this repository
2. Set up your environment
3. Follow the session guidance in [`instructions/`](instructions/README.md), or
   use the linked docs-site entry point when this repository uses that pattern

### 🎯 Learning outcomes

By the end of this session, you will be able to:

- Goal 1: Learn how simple it is to configure IaC templates with resiliency built-in
- Goal 2: Understand how to configure backup and run a recovery after a cyber threat 
- Goal 3: Easily discovery app resources and assess your application’s resiliency posture 

## Story Overview

Caldova is launching **CaldovaPayApp** to support its expansion into a new market. With customer transactions expected to surge during the holiday season, Caldova must build resiliency into the application from day one rather than retrofit it later. The growing transaction volume also makes Caldova a more attractive target for cyber threats. You are the Platform Architect for Caldova and you will take key decisions to ensure Caldova is prepared for the upcoming challenge.


### By the end of this lab, Caldova will:

- 🏗️ Have deployed CaldovaPayApp from an IaC template with zonal resiliency built in from the start.
- ✅ Have its cloud-native workloads backed up in a vault hardened against ransomware.
- 🛡️ Be able to identify compromised recovery points and recover virtual machines in bulk from verified clean snapshots.
- 🌐 Have its application resources grouped and assessed against zonal resiliency goals.
- 🔁 Have a recovery plan in place to orchestrate recovery.


### 💻 Technologies used

- [Resiliency Agent](https://learn.microsoft.com/en-us/azure/resiliency/goals-recommendations-use-agent)
- [Azure Backup](https://learn.microsoft.com/en-us/azure/backup/backup-overview)
- [Cyber Recovery in Azure Backup](https://learn.microsoft.com/en-us/azure/backup/security-overview) 
- [Infrastructure Resiliency Manager ](https://learn.microsoft.com/en-us/azure/resiliency/infrastructure-resiliency-manager-overview)

### 👥 Content owners

<!-- TODO: Add yourself as a content owner
1. Change the src in the image tag to {your github url}.png
2. Change INSERT NAME HERE to your name
3. Change the github url in the final href to your url. -->

<table>
<tr>
    <td align="center"><a href="http://github.com/sagarkeswani">
        <img src="https://github.com/sagarkeswani.png" width="100px;" alt="Sagar Keswani"/><br />
        <sub><b>Sagar Keswani</b></sub></a><br />
        <a href="https://github.com/sagarkeswani" title="talk">📢</a>
    </td>
    <td align="center"><a href="http://github.com/tbhavya">
        <img src="https://github.com/tbhavya.png" width="100px;" alt="Bhavya Tadikonda"/><br />
        <sub><b>Bhavya Tadikonda</b></sub></a><br />
        <a href="https://github.com/tbhavya" title="talk">📢</a>
    </td>
    <td align="center"><a href="http://github.com/viveksheelsingh">
        <img src="https://github.com/viveksheelsingh.png" width="100px;" alt="Vivek Sheel Singh"/><br />
        <sub><b>Vivek Sheel Singh</b></sub></a><br />
        <a href="https://github.com/viveksheelsingh" title="talk">Lab Developer and Proctor</a>
    </td>
    <td align="center"><a href="http://github.com/divyajain19">
        <img src="https://github.com/divyajain19.png" width="100px;" alt="Divya Jain"/><br />
        <sub><b>Divya Jain</b></sub></a><br />
        <a href="https://github.com/divyajain19" title="talk">Lab Developer and Proctor</a>
    </td>
    <td align="center"><a href="http://github.com/Charmila1">
        <img src="https://github.com/Charmila1.png" width="100px;" alt="Charmila Rekha Somala"/><br />
        <sub><b>Charmila Rekha Somala</b></sub></a><br />
        <a href="https://github.com/Charmila1" title="talk">Lab Developer and Proctor</a>
    </td>
    <td align="center"><a href="http://github.com">
        <img src="https://github.com/yourgithublink.png" width="100px;" alt="Venkatesh Sargunesan"/><br />
        <sub><b>Venkatesh Sargunesan</b></sub></a><br />
        <a href="https://github.com/Charmila1" title="talk">Azure Resiliency Expert</a>
    </td>
    <td align="center"><a href="http://github.com/suryasraju">
        <img src="https://github.com/suryasraju.png" width="100px;" alt="Surya Sripathi Raju"/><br />
        <sub><b>Surya Sripathi Raju</b></sub></a><br />
        <a href="https://github.com/suryasraju" title="talk">Azure Resiliency Expert</a>
    </td>   
</tr>
</table>

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
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Microsoft_Learn_MCP-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect/mcp/install?name=microsoft-learn&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Flearn.microsoft.com%2Fapi%2Fmcp%22%7D)

For more information, visit the [Learn MCP Server repo](https://aka.ms/learnmcp).
### ⚖️ Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft trademarks or logos is subject to and must follow [Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general). Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship.

Any use of third-party trademarks or logos are subject to those third-party's policies.
