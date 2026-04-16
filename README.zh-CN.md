# Awesome OpenClaw - 面向开发者的指南

**语言版本：** [English](README.md) | **简体中文**

[![Stars](https://img.shields.io/github/stars/openclaw/openclaw?style=flat&logo=github&label=Stars&color=gold)](https://github.com/openclaw/openclaw/stargazers)
[![Forks](https://img.shields.io/github/forks/openclaw/openclaw?style=flat&label=Forks&color=silver)](https://github.com/openclaw/openclaw/network/members)
[![Contributors](https://img.shields.io/github/contributors/openclaw/openclaw?label=Contributors&color=green)](https://github.com/openclaw/openclaw/graphs/contributors)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0 1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

面向开发者整理的 OpenClaw 指南。本 README 优先提供官方文档、实用的上手顺序、安全基线和更耐久的生态链接，而不是炒作、价格对比表或很快过时的营销信息。

---

## 目录

1. [产品概览](#product-overview)
2. [快速开始与安装方式](#quick-start-setup-methods)
3. [安装路径](#install-paths)
4. [核心概念与命令](#core-concepts-commands)
5. [Channels：先接什么](#channels-what-to-connect-first)
6. [部署选择](#deployment-choices)
7. [安全基线](#security-baseline)
8. [按目标查官方文档](#official-docs-by-goal)
9. [精选生态链接](#curated-ecosystem-links)
10. [常见错误](#common-mistakes)
11. [贡献方式](#contributing)

---

<a id="product-overview"></a>
## 1. 产品概览

**OpenClaw** 是一个运行在你自己设备上的个人 AI 助手。其核心是 **Gateway**，它充当 agents、channels、sessions、tools、dashboard/web UI 与远程访问的控制平面。一个很有帮助的理解方式是：OpenClaw 不只是“一个机器人”，它更像是一个本地优先的助理运行时，可以直接驻留在你已经在使用的聊天界面里。

### OpenClaw 实际能给开发者什么

- 一个本地 Gateway，带 CLI、dashboard、WebChat 和远程访问能力
- 跨 WhatsApp、Telegram、Slack、Discord、WebChat 等界面的多渠道消息能力
- 多个 agent，各自拥有独立的 workspace、session、binding 和 model policy
- 灵活的模型配置方式，支持托管 provider、基于 OAuth 的认证、API key 和本地模型路径
- skills、浏览器自动化、nodes、cron jobs 以及其他工具驱动工作流
- 个人助手式的信任模型，而不是面向敌对多租户 SaaS 的安全模型

### 核心架构（6 层）

| 层级 | 用途 |
|------|------|
| **Gateway** | 中央控制平面，负责消息路由、sessions、plugins 和工具执行策略 |
| **Channels** | 把 Telegram / WhatsApp / Discord / iMessage 统一成标准消息形态的适配层 |
| **Routing + Sessions** | 决定哪一个 agent 处理具体对话 |
| **Agent Runtime** | 处理上下文、调用模型提供商、流式输出响应并请求工具 |
| **Tools** | 能力层，包括网页获取、浏览器控制、命令执行、设备配对等 |
| **Surfaces** | 交互入口，包括聊天应用、Web 控制台、macOS 菜单栏和 Live Canvas |

### 名称演变

| 日期 | 名称 | 原因 |
|------|------|------|
| 2025 年 11 月 | **Clawdbot** | 上线时的原始名称 |
| 2026 年 1 月 27 日 | **Moltbot** | Anthropic 商标投诉（与 “Claude” 相似） |
| 2026 年 1 月 30 日 | **OpenClaw** | 最终更名，社区投票决定 |

### 适合什么 / 不适合什么

**如果你想要下面这些，OpenClaw 很合适：**

- 在自己的笔记本、台式机、家用服务器或 VPS 上运行个人助手
- 把长期聊天记录、文件和自动化都放在同一个 workspace 里
- 把同一个助手接入你已经在使用的多个消息渠道
- 试验 tools、skills、浏览器自动化或多 agent 路由

**如果你需要下面这些，它就不是最合适的选择：**

- 在同一个共享 gateway 上实现敌对多租户隔离
- 完全零维护、无需配置也无需运维责任的消费级应用
- 开箱即用的企业合规、SLA 和厂商支持

---

<a id="quick-start-setup-methods"></a>
## 2. 快速开始与安装方式

如果你只做一件事：先把本地 dashboard 跑通，再去连接任何外部 channel。

### 系统要求

| 项目 | 建议 |
|------|------|
| Runtime | 推荐 Node 24；最低 Node 22.16+ |
| 操作系统 | macOS 或 Linux；Windows 推荐通过 WSL2 使用 |
| 第一个界面 | Dashboard / WebChat |
| 第一个安装流程 | `openclaw onboard` |

### 快速开始（1 分钟）

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
openclaw dashboard
```

### 安装方式

### 方式 1：官方安装脚本

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
openclaw onboard --install-daemon
```

### 方式 2：npm / pnpm

```bash
npm install -g openclaw@latest
# 或
pnpm add -g openclaw@latest
```

### 方式 3：Docker

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
./docker-setup.sh
```

### 方式 4：一键云部署

| 平台 | 链接 | 说明 |
|------|------|------|
| **OpenClaw Launch** | [1-Click Deploy](https://www.aigeamy.com/) | 官方入口，最快上手 |
| **Railway** | [Template](https://railway.com/deploy/openclaw) | 基于 Web 的部署向导 |
| **DigitalOcean** | [1-Click Deploy](https://marketplace.digitalocean.com/apps/openclaw) | 预先强化安全并已配置好 |
| **Render** | [render.yaml](https://docs.openclaw.ai/render) | 基础设施即代码 |
| **SimpleClaw** | [simpleclaw.com](https://www.simpleclaw.com/) | 1 分钟内完成部署 |
| **Zeabur** | [Template](https://zeabur.com/templates/VTZ4FX) | 一键 Docker 部署 |
| **Northflank** | [Stack](https://northflank.com/stacks/deploy-openclaw) | 不需要服务器端终端 |
| **Lightning.AI** | [Environment](https://lightning.ai/lightning-ai/environments/openclaw) | 基于浏览器，无需本地硬件 |
| **Coolify** | [Template](https://github.com/essamamdani/openclaw-coolify) | 自托管 PaaS 模板 |
| **Elestio** | [Open Source](https://elest.io/open-source/openclaw) | 3 分钟内全托管上线 |

### 可比较的 AI Agent 产品

| # | 产品 | 网站 | 类型 | 自托管 | 消息平台 |
|---|------|------|------|--------|----------|
| 1 | **Hermes Agent** | [hermesagent.studio](https://hermesagent.studio/) | 自主 agent + 消息中枢 | ✅ | WhatsApp、Telegram、Slack、Discord 等 |
| 2 | **Multica** | [multica.uk](https://multica.uk/) | 多渠道 AI 自动化 | ✅ | 多平台 |
| 3 | **AutoGPT** | [agpt.co](https://agpt.co/) | 自主任务 agent | ✅ | API / Web UI |
| 4 | **LangChain** | [langchain.com](https://www.langchain.com/) | LLM 编排框架 | ✅ | 任意平台（通过自定义集成） |
| 5 | **n8n** | [n8n.io](https://n8n.io/) | 工作流自动化 + AI 节点 | ✅ | Slack、Telegram、Discord 和 400+ 应用 |
| 6 | **AgentGPT** | [agentgpt.reworkd.ai](https://agentgpt.reworkd.ai/) | 基于浏览器的自主 agent | ✅ | Web UI |
| 7 | **CrewAI** | [crewai.com](https://www.crewai.com/) | 多 agent 角色协作 | ✅ | API / 自定义集成 |
| 8 | **SuperAGI** | [superagi.com](https://superagi.com/) | 自主 agent 基础设施 | ✅ | Slack、Email、API |

### 第一小时检查清单

1. 运行 `openclaw onboard`，除非你已经非常确定自己的配置，否则优先选择 QuickStart。
2. 选定一个模型提供商和一个默认模型。
3. 第一次运行时让 gateway 保持仅本地可访问。
4. 打开 dashboard，确认在没有任何外部 channel 的情况下也能正常聊天。
5. 然后只添加一个 channel。
6. 在暴露任何远程访问能力前，运行 `openclaw doctor` 和 `openclaw security audit`。

### 更合理的学习顺序

1. 先熟悉 Dashboard / WebChat
2. 配好一个模型提供商
3. 接一个 channel
4. 做一次安全审计
5. 再学习 skills 和浏览器自动化
6. 最后再做远程访问 / VPS / 常驻部署

---

<a id="install-paths"></a>
## 3. 安装路径

| 路径 | 最适合谁 | 为什么有帮助 | 链接 |
|------|----------|--------------|------|
| CLI onboarding | 大多数开发者 | 最快的官方路径；会配置 gateway、workspace、channels、daemon 和 skills | [Getting Started](https://docs.openclaw.ai/start/getting-started) / [Onboarding](https://docs.openclaw.ai/start/wizard) |
| Docker | VPS 用户、希望更干净隔离的人 | 更容易把运行时封装起来并干净重部署 | [Docker](https://docs.openclaw.ai/install/docker) |
| 从源码安装 | 贡献者和调试者 | 可以完整使用主仓库的 `pnpm` 构建与 watch 工作流 | [openclaw/openclaw](https://github.com/openclaw/openclaw) |
| Nix | 追求可复现环境的人 | 声明式安装与更新 | [nix-openclaw](https://github.com/openclaw/nix-openclaw) |
| macOS 应用路径 | 以苹果设备为主的场景 | 如果你特别重视语音、canvas 和原生平台特性，它最有价值 | [macOS Platform Docs](https://docs.openclaw.ai/platforms/macos) |

### 建议

对普通开发者来说，默认答案仍然是：从 npm 安装，运行 onboarding，然后先在 dashboard 中验证一切正常，再做更激进的事情。

---

<a id="core-concepts-commands"></a>
## 4. 核心概念与命令

### 第一天真正重要的概念

| 概念 | 它的含义 | 为什么重要 |
|------|----------|------------|
| Gateway | 本地控制平面 | 负责配置、sessions、channels、tools、dashboard 和鉴权 |
| Agent | 逻辑上的助理身份 | 便于隔离不同用例、workspace 和 model policy |
| Workspace | 某个 agent 的文件和提示词空间 | skills、笔记和任务产物都在这里 |
| Channel | 一种消息集成 | 决定用户通过什么入口接触助手 |
| Session | 一段对话上下文 | 控制记忆连续性和路由行为 |
| Skill | 打包好的能力 | 可复用的 prompt + 文件 + 脚本组合 |
| Tool profile | 允许使用的能力集合 | 对安全性和行为影响最大的一组杠杆之一 |
| Model policy | 主模型加回退模型 | 控制质量、成本和工具安全姿态 |

### 值得尽早记住的命令

| 任务 | 命令 |
|------|------|
| 运行引导式安装 | `openclaw onboard` |
| 之后重新配置 | `openclaw configure` |
| 打开浏览器 dashboard | `openclaw dashboard` |
| 检查健康状态与迁移 | `openclaw doctor` |
| 审计安全姿态 | `openclaw security audit` |
| 深度安全审计 | `openclaw security audit --deep` |
| 添加另一个 agent | `openclaw agents add <name>` |
| 查看配置 | `openclaw config get <path>` |
| 更新配置 | `openclaw config set <path> <value>` |
| 查看模型鉴权 / 状态 | `openclaw models status` |
| 本地快速提问 | `openclaw agent --message "Ship checklist"` |

### 实用建议

- 在手动改很多 JSON 之前，先用 onboarding 和 `openclaw configure`。
- 如果你想把个人使用和工作自动化分开，尽早创建第二个 agent。
- 当某个 provider 看起来“已经配好了但就是不工作”时，优先检查 `openclaw models status`。

---

<a id="channels-what-to-connect-first"></a>
## 5. Channels：先接什么

第一天不要一口气接五个 channel。应该选择最符合你真实目标和可接受配置复杂度的那个入口。

| Channel | 最佳首个用途 | 说明 | 文档 |
|---------|--------------|------|------|
| WebChat | 最快的冒烟测试 | 不需要第三方 bot 配置；最适合第一次验证 | [WebChat](https://docs.openclaw.ai/web/webchat) |
| Telegram | 最容易接入的外部 bot 路线 | 很适合开发者作为第一个真实 channel | [Telegram](https://docs.openclaw.ai/channels/telegram) |
| WhatsApp | 日常个人助手 | 很适合真实使用，但要严格收紧私信策略 | [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) |
| Slack | 团队或内部工作流 | 在大范围开放 workspace 访问前先学清楚信任边界 | [Slack](https://docs.openclaw.ai/channels/slack) |
| Discord | 私有服务器或社区实验 | 在真正开放前先收紧私信与群组规则 | [Discord](https://docs.openclaw.ai/channels/discord) |
| Signal | 注重隐私的个人使用 | 需要额外依赖；如果你本来就主要用 Signal，则值得接入 | [Signal](https://docs.openclaw.ai/channels/signal) |

### 一个好记的经验法则

- 想最快成功：从 WebChat 或 Telegram 开始。
- 想做成日常主力：等 dashboard 跑通后再接 WhatsApp。
- 想给团队使用：先学安全与 agent 隔离，再接 Slack 或 Discord。

---

<a id="deployment-choices"></a>
## 6. 部署选择

| 场景 | 推荐路径 | 原因 |
|------|----------|------|
| 第一次评估 | 本地 CLI onboarding + dashboard | 复杂度最低，也最容易调试 |
| 常驻个人助手 | 家用服务器 / Mac mini / Linux 主机 + daemon | 稳定、适合日常使用，而且控制权在自己手里 |
| 低成本 VPS | Docker | 主机边界更清晰，重部署更简单 |
| 可复现的个人基础设施 | Nix | 声明式配置，可重复安装 |
| 远程访问 | Tailscale 或 SSH 隧道 | 比直接把 gateway 暴露到公网更安全 |
| 多个信任边界 | 分开部署不同 gateway，最好也分离 OS 用户 / 主机 | OpenClaw 并不是为同一 gateway 上的敌对多租户隔离设计的 |

### 远程部署前请先读这一段

远程访问应该在本地完成配置之后再加，而不是一开始就先做。最常见的失败方式，是在还没有想清楚 pairing 规则、allowlist、tool profile 和 agent 边界前，就把一个高权限助手暴露出去了。

---

<a id="security-baseline"></a>
## 7. 安全基线

很多 “awesome” 列表会跳过这一部分，但开发者真正需要它。

### 基线规则

- 把传入的私信、网页内容、共享聊天和上传文件都视为不可信输入。
- 在你还在熟悉系统时，让私信访问保持在 pairing 或严格 allowlist 模式。
- 如果不止一个人可以私信 bot，请使用 `session.dmScope: "per-channel-peer"` 或更严格的等价配置。
- 群组 channel 默认保持 mention-gated，除非你有非常明确的理由放开。
- 从严格的 tool profile 开始，只有在完全清楚原因时再扩大权限。
- 对共享 session 或非主 session，优先使用 sandboxing，而不是只靠提示词纪律。
- 在你有意配置远程访问和鉴权之前，让 gateway 始终保持仅本地可访问。
- 定期运行 `openclaw security audit`；当你准备扩大暴露面时，用 `--deep`。
- 把个人与公司信任边界分到不同 agents，最好也分到不同 gateway / 主机。

### 高价值安全链接

- [Security Guide](https://docs.openclaw.ai/gateway/security)
- [Sandboxing](https://docs.openclaw.ai/gateway/sandboxing)
- [Remote Access](https://docs.openclaw.ai/gateway/remote)
- [Tailscale](https://docs.openclaw.ai/gateway/tailscale)
- [Doctor](https://docs.openclaw.ai/gateway/doctor)

---

<a id="official-docs-by-goal"></a>
## 8. 按目标查官方文档

| 目标 | 最佳链接 |
|------|----------|
| 首次安装 | [Getting Started](https://docs.openclaw.ai/start/getting-started) |
| 引导式安装 | [Onboarding (CLI)](https://docs.openclaw.ai/start/wizard) |
| 先在浏览器里测试 | [Dashboard](https://docs.openclaw.ai/web/dashboard) |
| 配置 | [Configuration](https://docs.openclaw.ai/gateway/configuration) |
| 模型配置 | [Models CLI](https://docs.openclaw.ai/concepts/models) |
| Channels 总览 | [Channels](https://docs.openclaw.ai/channels) |
| Skills | [Skills](https://docs.openclaw.ai/tools/skills) |
| 浏览器自动化 | [Browser Tool](https://docs.openclaw.ai/tools/browser) |
| Docker 安装 | [Docker](https://docs.openclaw.ai/install/docker) |
| 安全加固 | [Security](https://docs.openclaw.ai/gateway/security) |
| 远程暴露 | [Remote Access](https://docs.openclaw.ai/gateway/remote) |
| 通过 Tailscale 远程访问 | [Tailscale](https://docs.openclaw.ai/gateway/tailscale) |
| 故障排查 | [FAQ](https://docs.openclaw.ai/help/faq) |

### 建议阅读顺序

1. Getting Started
2. Onboarding
3. Dashboard
4. Configuration
5. 任意一个 channel 文档
6. Security
7. Skills / browser / remote access

---

<a id="curated-ecosystem-links"></a>
## 9. 精选生态链接

等你已经完成一次可工作的安装之后，再来看这些资源。只有在官方 onboarding 路径已经对你说得通的时候，它们才真正有价值。

### 官方资源

| 资源 | 为什么值得看 |
|------|--------------|
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | 主代码仓库与权威 README |
| [docs.openclaw.ai](https://docs.openclaw.ai) | 官方文档中心 |
| [openclaw/clawhub](https://github.com/openclaw/clawhub) | 官方 skill 目录与包目录 |
| [openclaw/nix-openclaw](https://github.com/openclaw/nix-openclaw) | 面向可复现安装的 Nix 打包 |

### 社区资源

| 资源 | 为什么值得看 |
|------|--------------|
| [essamamdani/openclaw-coolify](https://github.com/essamamdani/openclaw-coolify) | 面向自托管 PaaS 用户的 Coolify 模板 |
| [serhanekicii/openclaw-helm](https://github.com/serhanekicii/openclaw-helm) | 如果你主要用 Kubernetes 部署，它提供 Helm chart |
| [lunarpulse/openclaw-mcp-plugin](https://github.com/lunarpulse/openclaw-mcp-plugin) | 面向 MCP 集成的良好起点 |
| [centminmod/explain-openclaw](https://github.com/centminmod/explain-openclaw) | 深入的技术说明与部署 / 安全笔记 |

---

<a id="common-mistakes"></a>
## 10. 常见错误

- 在本地聊天还没跑通前，就先去研究庞大的托管平台列表
- 一次接入太多 channels，结果调的是配置噪声，而不是一条清晰路径
- 把一个启用了工具的共享 agent 当作安全的多租户应用来看待
- 在本地尚未验证 pairing、allowlist 和鉴权之前就先暴露远程访问
- 把个人与公司的信任边界混在同一个高权限助手运行时里
- 没有提前规划硬件，就期待本地模型在弱机器上也有很强表现
- 在 onboarding 建出合理基线之前就手动改大量配置

---

<a id="contributing"></a>
## 11. 贡献方式

参见 [CONTRIBUTING.zh-CN.md](./CONTRIBUTING.zh-CN.md)。

当你添加链接时，优先考虑那些能帮助普通开发者把下面这些事情做好的资源：

- 安装 OpenClaw
- 正确配置它
- 以合理方式做好安全防护
- 更快排查问题
- 让它带来真实开发收益的扩展能力

---

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

本列表基于 CC0 1.0 Universal（公共领域）发布。
