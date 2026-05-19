# Awesome OpenClaw - Developer-First Guide

**Languages:** **English** | [简体中文](README.zh-CN.md) | [हिन्दी](README.hi.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Français](README.fr.md) | [বাংলা](README.bn.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Bahasa Indonesia](README.id.md)

[![Stars](https://img.shields.io/github/stars/openclaw/openclaw?style=flat&logo=github&label=Stars&color=gold)](https://github.com/openclaw/openclaw/stargazers)
[![Forks](https://img.shields.io/github/forks/openclaw/openclaw?style=flat&label=Forks&color=silver)](https://github.com/openclaw/openclaw/network/members)
[![Contributors](https://img.shields.io/github/contributors/openclaw/openclaw?label=Contributors&color=green)](https://github.com/openclaw/openclaw/graphs/contributors)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0 1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

Developer-first curated guide to OpenClaw. This README prioritizes official docs, practical setup order, security baselines, and durable ecosystem links over hype, pricing tables, and fast-staling marketing claims.

---

## Table of Contents

1. [Product Overview](#product-overview)
2. [Quick Start & Setup Methods](#quick-start-setup-methods)
3. [Install Paths](#install-paths)
4. [Core Concepts & Commands](#core-concepts-commands)
5. [Channels: What to Connect First](#channels-what-to-connect-first)
6. [Deployment Choices](#deployment-choices)
7. [Security Baseline](#security-baseline)
8. [Official Docs by Goal](#official-docs-by-goal)
9. [Curated Ecosystem Links](#curated-ecosystem-links)
10. [Common Mistakes](#common-mistakes)
11. [Contributing](#contributing)

---

<a id="product-overview"></a>
## 1. Product Overview

**OpenClaw** is a personal AI assistant you run on your own devices. At the center is the **Gateway**, which acts as the control plane for agents, channels, sessions, tools, dashboard/web UI, and remote access. A strong way to think about it is: OpenClaw is not "just a bot" - it is a local-first assistant runtime that can live inside the chat surfaces you already use.

### What OpenClaw Actually Gives Developers

- A local Gateway with CLI, dashboard, WebChat, and remote access options
- Multi-channel messaging across surfaces like WhatsApp, Telegram, Slack, Discord, WebChat, and more
- Multiple agents with separate workspaces, sessions, bindings, and model policies
- Flexible model setup across hosted providers, OAuth-based auth, API keys, and local-model paths
- Skills, browser automation, nodes, cron jobs, and other tool-driven workflows
- A personal-assistant trust model, not a hostile multi-tenant SaaS security model

### Core Architecture (6 Layers)

| Layer | Purpose |
|-------|---------|
| **Gateway** | Central control plane - message routing, sessions, plugins, tool execution policy |
| **Channels** | Adapters normalizing Telegram/WhatsApp/Discord/iMessage into standard message shapes |
| **Routing + Sessions** | Determines which agent handles specific conversations |
| **Agent Runtime** | Processes context, calls model providers, streams responses, requests tools |
| **Tools** | Capabilities - web fetch, browser control, command execution, device pairing |
| **Surfaces** | Interaction points - chat apps, web dashboard, macOS menu bar, Live Canvas |

### Name History

| Date | Name | Reason |
|------|------|--------|
| Nov 2025 | **Clawdbot** | Original name at launch |
| Jan 27, 2026 | **Moltbot** | Anthropic trademark complaint (similarity to "Claude") |
| Jan 30, 2026 | **OpenClaw** | Final rebrand, community vote |

### Good Fit / Not a Good Fit

**Good fit if you want to:**

- run a personal assistant on your own laptop, desktop, home server, or VPS
- keep long-lived chat history, files, and automation inside one workspace
- connect the same assistant to multiple messaging channels you already use
- experiment with tools, skills, browser automation, or multi-agent routing

**Not the best fit if you need:**

- hostile multi-tenant isolation on one shared gateway
- a zero-maintenance consumer app with no setup or operational ownership
- enterprise compliance, SLAs, and vendor support out of the box

---

<a id="quick-start-setup-methods"></a>
## 2. Quick Start & Setup Methods

If you only do one thing: get the local dashboard working before you connect any external channel.

### System Requirements

| Item | Recommendation |
|------|----------------|
| Runtime | Node 24 recommended; Node 22.16+ minimum |
| OS | macOS or Linux; Windows via WSL2 is the recommended Windows path |
| First interface | Dashboard / WebChat |
| First setup flow | `openclaw onboard` |

### Quick Start (1 Minute)

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
openclaw dashboard
```

### Installation Methods

### Method 1: Official Installer Script

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
openclaw onboard --install-daemon
```

### Method 2: npm / pnpm

```bash
npm install -g openclaw@latest
# or
pnpm add -g openclaw@latest
```

### Method 3: Docker

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
./docker-setup.sh
```

### Method 4: One-Click Cloud Deploys

| Platform | Link | Notes |
|----------|------|-------|
| **OpenClaw Launch** | [1-Click Deploy](https://www.aigeamy.com/) | Official, fastest to get started |
| **Railway** | [Template](https://railway.com/deploy/openclaw) | Web-based setup wizard |
| **DigitalOcean** | [1-Click Deploy](https://marketplace.digitalocean.com/apps/openclaw) | Security-hardened, pre-configured |
| **Render** | [render.yaml](https://docs.openclaw.ai/render) | Infrastructure as Code |
| **SimpleClaw** | [simpleclaw.com](https://www.simpleclaw.com/) | Deploy in under 1 minute |
| **Zeabur** | [Template](https://zeabur.com/templates/VTZ4FX) | One-click Docker deploy |
| **Northflank** | [Stack](https://northflank.com/stacks/deploy-openclaw) | No server-side terminal needed |
| **Lightning.AI** | [Environment](https://lightning.ai/lightning-ai/environments/openclaw) | Browser-based, no local hardware |
| **Coolify** | [Template](https://github.com/essamamdani/openclaw-coolify) | Self-hosted PaaS template |
| **Elestio** | [Open Source](https://elest.io/open-source/openclaw) | Fully managed in under 3 minutes |

### Comparable AI Agent Products

| # | Product | Website | Type | Self-Host | Messaging Platforms |
|---|---------|---------|------|-----------|---------------------|
| 1 | **Hermes Agent** | [hermesagent.studio](https://hermesagent.studio/) | Autonomous agent + messaging hub | Yes | WhatsApp, Telegram, Slack, Discord, and more |
| 2 | **Multica** | [multica.uk](https://multica.uk/) | Multi-channel AI automation | Yes | Multi-platform |
| 3 | **GenericAgent** | [genericagent.org](https://www.genericagent.org/) | Agent workspace with browser, terminal, filesystem, and memory control | Not specified | Web workspace |
| 4 | **Ruflo AI** | [ruflo.online](https://ruflo.online/?utm_source=github&utm_medium=docs&utm_campaign=awesome_openclaw_related) | Hosted Ruflo-style multi-agent workspace launch layer | No | Web workspace |
| 5 | **AutoGPT** | [agpt.co](https://agpt.co/) | Autonomous task agent | Yes | API / web UI |
| 6 | **LangChain** | [langchain.com](https://www.langchain.com/) | LLM orchestration framework | Yes | Any (via custom integrations) |
| 7 | **n8n** | [n8n.io](https://n8n.io/) | Workflow automation + AI nodes | Yes | Slack, Telegram, Discord, and 400+ apps |
| 8 | **AgentGPT** | [agentgpt.reworkd.ai](https://agentgpt.reworkd.ai/) | Browser-based autonomous agent | Yes | Web UI |
| 9 | **CrewAI** | [crewai.com](https://www.crewai.com/) | Multi-agent role collaboration | Yes | API / custom integrations |
| 10 | **SuperAGI** | [superagi.com](https://superagi.com/) | Autonomous agent infrastructure | Yes | Slack, Email, API |

### First-Hour Checklist

1. Run `openclaw onboard` and pick QuickStart unless you already know the exact config you want.
2. Choose one model provider and one default model.
3. Keep the gateway local-only on the first run.
4. Open the dashboard and verify you can chat without any external channel.
5. Add exactly one channel after that.
6. Run `openclaw doctor` and `openclaw security audit` before exposing anything remotely.

### What a Sensible Learning Order Looks Like

1. Dashboard or WebChat first
2. One model provider
3. One channel
4. Security audit
5. Skills and browser automation
6. Remote access, VPS, or always-on deployment

---

<a id="install-paths"></a>
## 3. Install Paths

| Path | Best For | Why It Helps | Link |
|------|----------|--------------|------|
| CLI onboarding | Most developers | Fastest official path; configures gateway, workspace, channels, daemon, and skills | [Getting Started](https://docs.openclaw.ai/start/getting-started) / [Onboarding](https://docs.openclaw.ai/start/wizard) |
| Docker | VPS, cleaner runtime isolation | Easier to contain the runtime and redeploy cleanly | [Docker](https://docs.openclaw.ai/install/docker) |
| From source | Contributors and debuggers | Full `pnpm` build and watch workflow from the main repo | [openclaw/openclaw](https://github.com/openclaw/openclaw) |
| Nix | Reproducible environments | Declarative setup and updates | [nix-openclaw](https://github.com/openclaw/nix-openclaw) |
| macOS app path | Apple-device-heavy setups | Most useful if you specifically care about voice, canvas, and native platform features | [macOS Platform Docs](https://docs.openclaw.ai/platforms/macos) |

### Recommendation

For a normal developer, the default answer is still: install from npm, run onboarding, and validate everything in the dashboard before doing anything more ambitious.

---

<a id="core-concepts-commands"></a>
## 4. Core Concepts & Commands

### Concepts That Matter on Day One

| Concept | What It Means | Why It Matters |
|--------|----------------|----------------|
| Gateway | The local control plane | Owns config, sessions, channels, tools, dashboard, and auth |
| Agent | A logical assistant identity | Lets you separate use cases, workspaces, and model policies |
| Workspace | Files and prompts for an agent | Where skills, notes, and task artifacts live |
| Channel | A messaging integration | Determines how users reach the assistant |
| Session | A conversation context | Controls memory continuity and routing behavior |
| Skill | A packaged capability | Reusable prompt + files + scripts for common tasks |
| Tool profile | Allowed capability set | One of the biggest security and behavior levers |
| Model policy | Primary model plus fallbacks | Controls quality, cost, and tool-safety posture |

### Commands Worth Memorizing Early

| Task | Command |
|------|---------|
| Run guided setup | `openclaw onboard` |
| Reconfigure later | `openclaw configure` |
| Open browser dashboard | `openclaw dashboard` |
| Inspect health and migrations | `openclaw doctor` |
| Audit security posture | `openclaw security audit` |
| Deep security audit | `openclaw security audit --deep` |
| Add another agent | `openclaw agents add <name>` |
| Inspect config | `openclaw config get <path>` |
| Update config | `openclaw config set <path> <value>` |
| Check model auth or status | `openclaw models status` |
| Quick local prompt | `openclaw agent --message "Ship checklist"` |

### Practical Advice

- Use onboarding and `openclaw configure` before hand-editing a lot of JSON.
- Create a second agent early if you want to separate personal use from work automation.
- Check `openclaw models status` whenever a provider feels "configured but not working."

---

<a id="channels-what-to-connect-first"></a>
## 5. Channels: What to Connect First

Do not connect five channels on day one. Pick the surface that matches your real goal and setup tolerance.

| Channel | Best First Use | Notes | Docs |
|---------|----------------|-------|------|
| WebChat | Fastest smoke test | No third-party bot setup; ideal for first validation | [WebChat](https://docs.openclaw.ai/web/webchat) |
| Telegram | Easiest external bot path | Good first real channel for developers | [Telegram](https://docs.openclaw.ai/channels/telegram) |
| WhatsApp | Daily personal assistant | Great for real-world usage, but keep DM policies tight | [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) |
| Slack | Team or internal workflow | Learn trust boundaries before broad workspace access | [Slack](https://docs.openclaw.ai/channels/slack) |
| Discord | Private server or community experiments | Tighten DM and group rules before opening it up | [Discord](https://docs.openclaw.ai/channels/discord) |
| Signal | Privacy-oriented personal usage | Extra dependency, worth it if Signal is where you already live | [Signal](https://docs.openclaw.ai/channels/signal) |

### Useful Rule of Thumb

- Want the fastest success path: start with WebChat or Telegram.
- Want a real daily-driver: move to WhatsApp after the dashboard works.
- Want team usage: learn security and agent separation first, then use Slack or Discord.

---

<a id="deployment-choices"></a>
## 6. Deployment Choices

| Scenario | Recommended Path | Why |
|----------|------------------|-----|
| First evaluation | Local CLI onboarding + dashboard | Lowest complexity and easiest debugging |
| Personal always-on assistant | Home server / Mac mini / Linux box + daemon | Stable daily-driver setup with local ownership |
| Cheap VPS | Docker | Cleaner host boundary and simpler redeploy story |
| Reproducible personal infra | Nix | Declarative config and repeatable installs |
| Remote access | Tailscale or SSH tunnel | Safer than exposing the gateway blindly to the internet |
| Multiple trust boundaries | Separate gateways, and ideally separate OS users or hosts | OpenClaw is not designed as hostile multi-tenant isolation on one shared gateway |

### Read This Before You Deploy Remotely

Remote access is something to add after local setup, not before. The common failure mode is exposing a powerful assistant before pairing rules, allowlists, tool profiles, and agent boundaries are thought through.

---

<a id="security-baseline"></a>
## 7. Security Baseline

This is the section many "awesome" lists skip and developers actually need.

### Baseline Rules

- Treat inbound DMs, web content, shared chats, and uploaded files as untrusted input.
- Keep DM access in pairing or strict allowlist mode while you are still learning the system.
- If more than one person can DM the bot, use `session.dmScope: "per-channel-peer"` or a stricter equivalent.
- Keep group channels mention-gated unless you have a specific reason not to.
- Start with a restrictive tool profile and only widen access when you know exactly why.
- For shared or non-main sessions, prefer sandboxing rather than trusting prompt discipline alone.
- Keep the gateway local-only until you intentionally configure remote access and auth.
- Run `openclaw security audit` regularly, and use `--deep` when you are about to widen exposure.
- Separate personal and company trust boundaries into different agents, and preferably different gateways or hosts.

### High-Value Security Links

- [Security Guide](https://docs.openclaw.ai/gateway/security)
- [Sandboxing](https://docs.openclaw.ai/gateway/sandboxing)
- [Remote Access](https://docs.openclaw.ai/gateway/remote)
- [Tailscale](https://docs.openclaw.ai/gateway/tailscale)
- [Doctor](https://docs.openclaw.ai/gateway/doctor)

---

<a id="official-docs-by-goal"></a>
## 8. Official Docs by Goal

| Goal | Best Link |
|------|-----------|
| First install | [Getting Started](https://docs.openclaw.ai/start/getting-started) |
| Guided setup | [Onboarding (CLI)](https://docs.openclaw.ai/start/wizard) |
| Browser-first testing | [Dashboard](https://docs.openclaw.ai/web/dashboard) |
| Configuration | [Configuration](https://docs.openclaw.ai/gateway/configuration) |
| Model setup | [Models CLI](https://docs.openclaw.ai/concepts/models) |
| Channels overview | [Channels](https://docs.openclaw.ai/channels) |
| Skills | [Skills](https://docs.openclaw.ai/tools/skills) |
| Browser automation | [Browser Tool](https://docs.openclaw.ai/tools/browser) |
| Docker install | [Docker](https://docs.openclaw.ai/install/docker) |
| Security hardening | [Security](https://docs.openclaw.ai/gateway/security) |
| Remote exposure | [Remote Access](https://docs.openclaw.ai/gateway/remote) |
| Remote access via Tailscale | [Tailscale](https://docs.openclaw.ai/gateway/tailscale) |
| Troubleshooting | [FAQ](https://docs.openclaw.ai/help/faq) |

### Suggested Reading Order

1. Getting Started
2. Onboarding
3. Dashboard
4. Configuration
5. One channel doc
6. Security
7. Skills, browser automation, and remote access

---

<a id="curated-ecosystem-links"></a>
## 9. Curated Ecosystem Links


Browse these after you have one working install. They are much more useful once the official onboarding path already makes sense to you.



- [OpenHuman Online](https://openhuman.online/?utm_source=github&utm_medium=readme&utm_campaign=openhuman_public_repos&utm_content=awesome_openclaw) - inspectable AI memory tree planning for teams running assistants with human-readable source context.
### Official

| Resource | Why It Matters |
|----------|----------------|
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | Main codebase and the authoritative README |
| [docs.openclaw.ai](https://docs.openclaw.ai) | Official documentation hub |
| [openclaw/clawhub](https://github.com/openclaw/clawhub) | Official skill directory and package catalog |
| [openclaw/nix-openclaw](https://github.com/openclaw/nix-openclaw) | Nix packaging for reproducible installs |

### Community

| Resource | Why It Matters |
|----------|----------------|
| [essamamdani/openclaw-coolify](https://github.com/essamamdani/openclaw-coolify) | Coolify template for self-hosted PaaS users |
| [serhanekicii/openclaw-helm](https://github.com/serhanekicii/openclaw-helm) | Helm chart if your deployment world is Kubernetes |
| [lunarpulse/openclaw-mcp-plugin](https://github.com/lunarpulse/openclaw-mcp-plugin) | MCP-oriented integration starting point |
| [centminmod/explain-openclaw](https://github.com/centminmod/explain-openclaw) | Deep technical documentation and deployment or security notes |

---

<a id="common-mistakes"></a>
## 10. Common Mistakes

- Reading massive hosting tables before you have a local chat working
- Connecting too many channels at once, then debugging setup noise instead of one clear path
- Treating a shared tool-enabled agent as if it were a safe multi-tenant app
- Exposing the gateway remotely before pairing, allowlists, and auth are tested locally
- Mixing personal and company trust boundaries inside one powerful assistant runtime
- Expecting strong local-model performance on underpowered hardware without planning for it
- Hand-editing lots of config before onboarding has created a sane baseline

---

<a id="contributing"></a>
## 11. Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md).

When adding links, prefer resources that help a normal developer do one of these jobs well:

- install OpenClaw
- configure it correctly
- secure it sensibly
- debug it faster
- extend it with a real development payoff

---

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

This list is released under CC0 1.0 Universal (Public Domain).
