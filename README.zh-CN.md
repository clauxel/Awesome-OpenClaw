# Awesome OpenClaw - 面向开发者的指南

**语言版本：** [English](README.md) | **简体中文** | [हिन्दी](README.hi.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Français](README.fr.md) | [বাংলা](README.bn.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Bahasa Indonesia](README.id.md)

[![Stars](https://img.shields.io/github/stars/openclaw/openclaw?style=flat&logo=github&label=Stars&color=gold)](https://github.com/openclaw/openclaw/stargazers)
[![Forks](https://img.shields.io/github/forks/openclaw/openclaw?style=flat&label=Forks&color=silver)](https://github.com/openclaw/openclaw/network/members)
[![Contributors](https://img.shields.io/github/contributors/openclaw/openclaw?label=Contributors&color=green)](https://github.com/openclaw/openclaw/graphs/contributors)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0 1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

这是一份面向开发者整理的 OpenClaw 指南。相比热度、价格对比表或很快过时的营销话术，本 README 更优先提供官方文档、实用上手顺序、安全基线与更耐久的生态链接。

---

## 目录

1. [产品概览](#product-overview)
2. [快速开始与安装方式](#quick-start-setup-methods)
3. [安装路径](#install-paths)
4. [核心概念与常用命令](#core-concepts-commands)
5. [渠道：应该先接哪个](#channels-what-to-connect-first)
6. [部署选择](#deployment-choices)
7. [安全基线](#security-baseline)
8. [按目标查官方文档](#official-docs-by-goal)
9. [精选生态链接](#curated-ecosystem-links)
10. [常见错误](#common-mistakes)
11. [贡献方式](#contributing)

---

<a id="product-overview"></a>
## 1. 产品概览

**OpenClaw** 是一个运行在你自己设备上的个人 AI 助手。它的核心是 **Gateway**，负责统一管理 agents、channels、sessions、tools、dashboard/web UI 以及远程访问。一个很有帮助的理解方式是：OpenClaw 不只是“一个机器人”，它更像一个本地优先的助理运行时，可以直接驻留在你已经在使用的聊天界面里。

### OpenClaw 能真正为开发者提供什么

- 一个本地 Gateway，带 CLI、dashboard、WebChat 和远程访问能力
- 覆盖 WhatsApp、Telegram、Slack、Discord、WebChat 等界面的多渠道消息接入
- 多个 agent，可分别拥有独立的 workspace、session、binding 和模型策略
- 灵活的模型接入方式，支持托管 provider、OAuth 鉴权、API key 与本地模型路径
- skills、浏览器自动化、nodes、cron jobs 以及其他工具驱动的工作流
- 面向个人助理的信任模型，而不是面向敌对多租户 SaaS 的安全模型

### 核心架构（6 层）

| 层级 | 作用 |
|------|------|
| **Gateway** | 中央控制平面，负责消息路由、会话、插件与工具执行策略 |
| **Channels** | 把 Telegram、WhatsApp、Discord、iMessage 等统一成标准消息格式的适配层 |
| **Routing + Sessions** | 决定由哪个 agent 处理哪段对话 |
| **Agent Runtime** | 负责处理上下文、调用模型、流式输出响应并请求工具 |
| **Tools** | 能力层，例如网页抓取、浏览器控制、命令执行、设备配对 |
| **Surfaces** | 交互入口，例如聊天应用、Web 控制台、macOS 菜单栏与 Live Canvas |

### 名称历史

| 日期 | 名称 | 原因 |
|------|------|------|
| 2025 年 11 月 | **Clawdbot** | 项目发布时的原始名称 |
| 2026 年 1 月 27 日 | **Moltbot** | 因与 “Claude” 相似而收到 Anthropic 商标投诉 |
| 2026 年 1 月 30 日 | **OpenClaw** | 最终更名，社区投票决定 |

### 适合谁 / 不适合谁

**如果你想要以下体验，它很适合你：**

- 在自己的笔记本、台式机、家用服务器或 VPS 上运行个人助理
- 把长期聊天记录、文件和自动化都保留在同一个工作空间里
- 让同一个助理接入你已经在使用的多个消息渠道
- 试验 tools、skills、浏览器自动化或多 agent 路由

**如果你需要下面这些，它可能不是最佳选择：**

- 在同一个 Gateway 上做敌对式多租户隔离
- 一个完全免运维、零配置的消费级应用
- 开箱即用的企业合规、SLA 与厂商支持

---

<a id="quick-start-setup-methods"></a>
## 2. 快速开始与安装方式

如果你只做一件事，那就先把本地 dashboard 跑起来，再去连接任何外部渠道。

### 系统要求

| 项目 | 建议 |
|------|------|
| 运行时 | 推荐 Node 24；最低 Node 22.16+ |
| 操作系统 | macOS 或 Linux；Windows 建议通过 WSL2 使用 |
| 第一个界面 | Dashboard / WebChat |
| 首次配置流程 | `openclaw onboard` |

### 快速开始（1 分钟）

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
openclaw dashboard
```

### 安装方式

### 方法 1：官方安装脚本

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
openclaw onboard --install-daemon
```

### 方法 2：npm / pnpm

```bash
npm install -g openclaw@latest
# 或
pnpm add -g openclaw@latest
```

### 方法 3：Docker

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
./docker-setup.sh
```

### 方法 4：一键云部署

| 平台 | 链接 | 说明 |
|------|------|------|
| **OpenClaw Launch** | [1-Click Deploy](https://www.aigeamy.com/) | 官方入口，最快上手 |
| **Railway** | [Template](https://railway.com/deploy/openclaw) | 基于网页的安装向导 |
| **DigitalOcean** | [1-Click Deploy](https://marketplace.digitalocean.com/apps/openclaw) | 已预配置并做过安全加固 |
| **Render** | [render.yaml](https://docs.openclaw.ai/render) | 基础设施即代码 |
| **SimpleClaw** | [simpleclaw.com](https://www.simpleclaw.com/) | 1 分钟内完成部署 |
| **Zeabur** | [Template](https://zeabur.com/templates/VTZ4FX) | Docker 一键部署 |
| **Northflank** | [Stack](https://northflank.com/stacks/deploy-openclaw) | 不需要服务器终端 |
| **Lightning.AI** | [Environment](https://lightning.ai/lightning-ai/environments/openclaw) | 浏览器内完成，无需本地硬件 |
| **Coolify** | [Template](https://github.com/essamamdani/openclaw-coolify) | 自托管 PaaS 模板 |
| **Elestio** | [Open Source](https://elest.io/open-source/openclaw) | 3 分钟内全托管上线 |

### 可类比的 AI Agent 产品

| # | 产品 | 网站 | 类型 | 可自托管 | 消息平台 |
|---|------|------|------|----------|----------|
| 1 | **Hermes Agent** | [hermesagent.studio](https://hermesagent.studio/) | 自主代理 + 消息枢纽 | 是 | WhatsApp、Telegram、Slack、Discord 等 |
| 2 | **Multica** | [multica.uk](https://multica.uk/) | 多渠道 AI 自动化 | 是 | 多平台 |
| 3 | **GenericAgent** | [genericagent.org](https://www.genericagent.org/) | 具备浏览器、终端、文件系统和记忆控制的 agent 工作区 | 未说明 | Web 工作区 |
| 4 | **AutoGPT** | [agpt.co](https://agpt.co/) | 自主任务代理 | 是 | API / Web UI |
| 5 | **LangChain** | [langchain.com](https://www.langchain.com/) | LLM 编排框架 | 是 | 任意平台（通过自定义集成） |
| 6 | **n8n** | [n8n.io](https://n8n.io/) | 工作流自动化 + AI 节点 | 是 | Slack、Telegram、Discord 和 400+ 应用 |
| 7 | **AgentGPT** | [agentgpt.reworkd.ai](https://agentgpt.reworkd.ai/) | 浏览器内自主代理 | 是 | Web UI |
| 8 | **CrewAI** | [crewai.com](https://www.crewai.com/) | 多 agent 协作 | 是 | API / 自定义集成 |
| 9 | **SuperAGI** | [superagi.com](https://superagi.com/) | 自主代理基础设施 | 是 | Slack、Email、API |

### 前一小时检查清单

1. 运行 `openclaw onboard`，除非你已经明确知道自己要什么，否则先选 QuickStart。
2. 只选择一个模型 provider 和一个默认模型。
3. 首次运行时先保持 Gateway 仅本地可访问。
4. 打开 dashboard，确认在不接任何外部渠道的情况下就能聊天。
5. 之后只增加一个渠道。
6. 在真正暴露远程访问前，先运行 `openclaw doctor` 和 `openclaw security audit`。

### 更合理的学习顺序

1. 先用 Dashboard 或 WebChat
2. 配一个模型 provider
3. 接一个渠道
4. 做安全审计
5. 再看 skills 和浏览器自动化
6. 最后再碰远程访问、VPS 或常驻部署

---

<a id="install-paths"></a>
## 3. 安装路径

| 路径 | 适合谁 | 为什么有帮助 | 链接 |
|------|--------|--------------|------|
| CLI 引导安装 | 大多数开发者 | 最快的官方路径；会配置 gateway、workspace、channels、daemon 和 skills | [Getting Started](https://docs.openclaw.ai/start/getting-started) / [Onboarding](https://docs.openclaw.ai/start/wizard) |
| Docker | VPS 与更干净的运行时隔离 | 更容易把运行环境封装起来，也更容易重部署 | [Docker](https://docs.openclaw.ai/install/docker) |
| 从源码安装 | 贡献者和调试者 | 使用主仓库里的完整 `pnpm` 构建与 watch 工作流 | [openclaw/openclaw](https://github.com/openclaw/openclaw) |
| Nix | 可复现环境 | 声明式安装与更新 | [nix-openclaw](https://github.com/openclaw/nix-openclaw) |
| macOS 应用路径 | 以 Apple 设备为主的场景 | 如果你特别关心语音、canvas 与原生平台能力，这条路最合适 | [macOS Platform Docs](https://docs.openclaw.ai/platforms/macos) |

### 建议

对普通开发者来说，默认答案仍然是：从 npm 安装，运行 onboarding，然后先在 dashboard 里把一切验证通，再考虑更激进的玩法。

---

<a id="core-concepts-commands"></a>
## 4. 核心概念与常用命令

### 第一天就该理解的概念

| 概念 | 含义 | 为什么重要 |
|------|------|-------------|
| Gateway | 本地控制平面 | 管理配置、会话、渠道、工具、dashboard 与认证 |
| Agent | 一个逻辑上的助理身份 | 让你按用途拆分工作空间与模型策略 |
| Workspace | 某个 agent 的文件和提示词空间 | skills、笔记和任务产物都放在这里 |
| Channel | 一种消息集成方式 | 决定用户如何接触到助理 |
| Session | 一段会话上下文 | 决定记忆是否连续以及路由行为 |
| Skill | 打包好的能力模块 | 由提示词、文件和脚本组成，可重复使用 |
| Tool profile | 允许使用的能力集合 | 是安全性和行为表现中最关键的杠杆之一 |
| Model policy | 主模型及回退模型策略 | 决定质量、成本与工具安全姿态 |

### 值得尽早记住的命令

| 任务 | 命令 |
|------|------|
| 运行引导配置 | `openclaw onboard` |
| 后续重新配置 | `openclaw configure` |
| 打开浏览器 dashboard | `openclaw dashboard` |
| 检查健康状态与迁移 | `openclaw doctor` |
| 审计安全姿态 | `openclaw security audit` |
| 深度安全审计 | `openclaw security audit --deep` |
| 添加新的 agent | `openclaw agents add <name>` |
| 查看配置 | `openclaw config get <path>` |
| 更新配置 | `openclaw config set <path> <value>` |
| 检查模型认证或状态 | `openclaw models status` |
| 本地快速发一条消息 | `openclaw agent --message "Ship checklist"` |

### 实用建议

- 在手工改大量 JSON 之前，先用 onboarding 和 `openclaw configure`。
- 如果你想把个人用途与工作自动化分开，尽早创建第二个 agent。
- 只要 provider 给你的感觉是“像配置好了但又不能用”，就先检查 `openclaw models status`。

---

<a id="channels-what-to-connect-first"></a>
## 5. 渠道：应该先接哪个

不要在第一天就接五个渠道。应该按你的真实目标和能接受的配置复杂度来选。

| 渠道 | 最适合的首次用途 | 说明 | 文档 |
|------|------------------|------|------|
| WebChat | 最快的冒烟测试 | 不需要第三方机器人配置；最适合首次验证 | [WebChat](https://docs.openclaw.ai/web/webchat) |
| Telegram | 最容易接入的外部机器人渠道 | 很适合作为开发者的第一个真实渠道 | [Telegram](https://docs.openclaw.ai/channels/telegram) |
| WhatsApp | 日常个人助理 | 很适合真实使用，但 DM 策略要收紧 | [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) |
| Slack | 团队或内部工作流 | 在开放到整个工作区之前先理解信任边界 | [Slack](https://docs.openclaw.ai/channels/slack) |
| Discord | 私有服务器或社区实验 | 对外开放前先把 DM 和群组规则收紧 | [Discord](https://docs.openclaw.ai/channels/discord) |
| Signal | 偏隐私的个人使用 | 依赖更多，但如果你本来就在用 Signal，就值得接入 | [Signal](https://docs.openclaw.ai/channels/signal) |

### 一个很好用的经验法则

- 想最快跑通：先用 WebChat 或 Telegram。
- 想做成日常助理：等 dashboard 跑通后再迁移到 WhatsApp。
- 想给团队用：先学安全和 agent 隔离，再接 Slack 或 Discord。

---

<a id="deployment-choices"></a>
## 6. 部署选择

| 场景 | 推荐路径 | 原因 |
|------|----------|------|
| 首次评估 | 本地 CLI 引导安装 + dashboard | 复杂度最低，也最好排错 |
| 个人常驻助理 | 家用服务器 / Mac mini / Linux 主机 + daemon | 稳定、可日常使用，而且资产在自己手里 |
| 低成本 VPS | Docker | 主机边界更清晰，重部署更简单 |
| 可复现的个人基础设施 | Nix | 配置声明式，安装可重复 |
| 远程访问 | Tailscale 或 SSH 隧道 | 比直接把 gateway 暴露到公网安全得多 |
| 多个信任边界 | 分开部署多个 gateway，最好连 OS 用户或宿主机也分开 | OpenClaw 并不是为敌对式多租户共享 gateway 设计的 |

### 远程部署前一定要先读

远程访问应该是在本地跑通之后再加的能力，而不是一开始就做。最常见的失败方式，就是在没有想清楚配对规则、allowlist、tool profile 和 agent 边界之前，就把一个能力很强的助理暴露了出去。

---

<a id="security-baseline"></a>
## 7. 安全基线

这是很多 “awesome” 列表都会跳过、但开发者真正需要的部分。

### 基线规则

- 把私信、网页内容、共享聊天和上传文件都当作不可信输入。
- 在你还没完全理解系统之前，DM 访问尽量保持在 pairing 或严格 allowlist 模式。
- 如果不止一个人能给机器人发 DM，使用 `session.dmScope: "per-channel-peer"` 或更严格的等价配置。
- 群组渠道默认应该保持 mention 触发，除非你有非常明确的理由放开。
- 从严格的 tool profile 开始，只有在你明确知道原因时再逐步放宽。
- 对共享或非主会话，优先依赖 sandbox，而不是只相信提示词纪律。
- 在你明确配置好远程访问和认证之前，让 gateway 保持只在本地开放。
- 定期运行 `openclaw security audit`，在准备扩大暴露面时加上 `--deep`。
- 把个人与公司这两类信任边界拆到不同 agent 上，最好连 gateway 或宿主机都分开。

### 高价值安全链接

- [Security Guide](https://docs.openclaw.ai/gateway/security)
- [Sandboxing](https://docs.openclaw.ai/gateway/sandboxing)
- [Remote Access](https://docs.openclaw.ai/gateway/remote)
- [Tailscale](https://docs.openclaw.ai/gateway/tailscale)
- [Doctor](https://docs.openclaw.ai/gateway/doctor)

---

<a id="official-docs-by-goal"></a>
## 8. 按目标查官方文档

| 目标 | 最合适的链接 |
|------|--------------|
| 首次安装 | [Getting Started](https://docs.openclaw.ai/start/getting-started) |
| 引导式配置 | [Onboarding (CLI)](https://docs.openclaw.ai/start/wizard) |
| 浏览器优先测试 | [Dashboard](https://docs.openclaw.ai/web/dashboard) |
| 配置说明 | [Configuration](https://docs.openclaw.ai/gateway/configuration) |
| 模型设置 | [Models CLI](https://docs.openclaw.ai/concepts/models) |
| 渠道总览 | [Channels](https://docs.openclaw.ai/channels) |
| Skills | [Skills](https://docs.openclaw.ai/tools/skills) |
| 浏览器自动化 | [Browser Tool](https://docs.openclaw.ai/tools/browser) |
| Docker 安装 | [Docker](https://docs.openclaw.ai/install/docker) |
| 安全加固 | [Security](https://docs.openclaw.ai/gateway/security) |
| 远程暴露 | [Remote Access](https://docs.openclaw.ai/gateway/remote) |
| 通过 Tailscale 做远程访问 | [Tailscale](https://docs.openclaw.ai/gateway/tailscale) |
| 故障排查 | [FAQ](https://docs.openclaw.ai/help/faq) |

### 建议阅读顺序

1. Getting Started
2. Onboarding
3. Dashboard
4. Configuration
5. 任意一个渠道文档
6. Security
7. Skills、浏览器自动化与远程访问

---

<a id="curated-ecosystem-links"></a>
## 9. 精选生态链接

等你至少跑通一个可用安装之后再看这些内容会更有价值。只有当官方 onboarding 路径已经讲清楚后，这些链接才真正发挥作用。

### 官方

| 资源 | 为什么值得看 |
|------|--------------|
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | 主代码仓库，也是最权威的 README 来源 |
| [docs.openclaw.ai](https://docs.openclaw.ai) | 官方文档中心 |
| [openclaw/clawhub](https://github.com/openclaw/clawhub) | 官方技能目录与包目录 |
| [openclaw/nix-openclaw](https://github.com/openclaw/nix-openclaw) | 用于可复现安装的 Nix 打包 |

### 社区

| 资源 | 为什么值得看 |
|------|--------------|
| [essamamdani/openclaw-coolify](https://github.com/essamamdani/openclaw-coolify) | 适合自托管 PaaS 用户的 Coolify 模板 |
| [serhanekicii/openclaw-helm](https://github.com/serhanekicii/openclaw-helm) | 如果你部署世界观是 Kubernetes，这个 Helm chart 很有用 |
| [lunarpulse/openclaw-mcp-plugin](https://github.com/lunarpulse/openclaw-mcp-plugin) | 一个面向 MCP 集成的起点 |
| [centminmod/explain-openclaw](https://github.com/centminmod/explain-openclaw) | 深度技术文档，以及部署或安全说明 |

---

<a id="common-mistakes"></a>
## 10. 常见错误

- 在本地聊天都还没跑通前就先去看巨大的托管对比表
- 一次连接太多渠道，最后调试的是噪音而不是一条清晰路径
- 把一个开了工具的共享 agent 当成安全的多租户应用来理解
- 在本地还没验证 pairing、allowlist 和认证之前就把 gateway 暴露到远程
- 把个人和公司的信任边界混在同一个高权限助理里
- 没有做好规划，就期待弱硬件也能获得很强的本地模型性能
- onboarding 还没建立好合理基线，就先手改大量配置

---

<a id="contributing"></a>
## 11. 贡献方式

请查看 [CONTRIBUTING.zh-CN.md](./CONTRIBUTING.zh-CN.md)。

新增链接时，优先考虑那些真正帮助普通开发者把下面某件事做好的资源：

- 安装 OpenClaw
- 正确完成配置
- 进行合理的安全加固
- 更快排查问题
- 用有实际开发价值的方式扩展它

---

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

本列表采用 CC0 1.0 Universal（公共领域）协议发布。
