# Awesome OpenClaw — Complete Reference Guide

[![Stars](https://img.shields.io/github/stars/openclaw/openclaw?style=flat&logo=github&label=Stars&color=gold)](https://github.com/openclaw/openclaw/stargazers)
[![Forks](https://img.shields.io/github/forks/openclaw/openclaw?style=flat&label=Forks&color=silver)](https://github.com/openclaw/openclaw/network/members)
[![Contributors](https://img.shields.io/github/contributors/openclaw/openclaw?label=Contributors&color=green)](https://github.com/openclaw/openclaw/graphs/contributors)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/openclaw/openclaw/blob/main/LICENSE)

> Fastest-growing GitHub repo ever — 9K to 195K stars in 66 days (18x faster than Kubernetes)

The most comprehensive, curated collection of OpenClaw resources: hosting guides, cost comparisons, security hardening, skills, tutorials, and community links.

---

## Table of Contents

1. [Product Overview](#1-product-overview)
2. [Quick Start & Setup Methods](#2-quick-start--setup-methods)
   - [Comparable AI Agent Products](#comparable-ai-agent-products)
3. [Hosting & Deployment](#3-hosting--deployment)
   - [Free Tier](#31-free-tier-0month)
   - [Budget VPS](#32-budget-vps-2-8month)
   - [Mid-Range VPS](#33-mid-range-5-25month)
   - [Serverless & PaaS](#34-serverless--paas)
   - [Managed Hosting Services](#35-managed-hosting-services)
   - [Setup-as-a-Service](#36-setup-as-a-service-freelancers)
   - [Master Cost Comparison Table](#37-master-cost-comparison-table)
4. [Platform-Specific Deployment Guides](#4-platform-specific-deployment-guides)
5. [Cost Analysis](#5-cost-analysis)
6. [Configuration](#6-configuration)
7. [Features & Integrations](#7-features--integrations)
8. [Security](#8-security)
9. [Skills & Ecosystem](#9-skills--ecosystem)
10. [Browser Automation](#10-browser-automation)
11. [Real-World Use Cases](#11-real-world-use-cases)
12. [Learning Resources](#12-learning-resources)
13. [Community & Media](#13-community--media)
14. [Alternatives & Competitors](#14-alternatives--competitors)
15. [Related Repositories](#15-related-repositories)
16. [Performance Benchmarks](#16-performance-benchmarks)
17. [Enterprise Considerations](#17-enterprise-considerations)
18. [China & Global Adoption](#18-china--global-adoption)
19. [Release History](#19-release-history)
20. [Key Contributors](#20-key-contributors)
21. [Contributing](#21-contributing)

---

## 1. Product Overview

**OpenClaw** (formerly Clawdbot → Moltbot) is a free, open-source autonomous AI agent created by **Peter Steinberger** ([@steipete](https://github.com/steipete)). It runs on your own hardware, connects to 10+ messaging platforms (WhatsApp, Telegram, Slack, Discord, Signal, iMessage, Google Chat, Microsoft Teams, Matrix, Zalo), and orchestrates AI agent workflows with persistent memory and 24/7 operation.

### What OpenClaw Does

- Runs **locally on your own hardware** (Mac Mini, VPS, Raspberry Pi, ESP32-S3, or serverless)
- Connects to **10+ messaging platforms** simultaneously
- Has **persistent memory** across sessions (saves files, breadcrumbs, chat histories)
- Handles **tasks spanning hours or days** without losing context
- Operates **24/7 autonomously** focusing on automation and integration
- Supports **5,700+ community-built skills** via ClawHub
- Works with **multiple AI providers** (Anthropic, OpenAI, Google, OpenRouter, DeepSeek, local LLMs)
- Features **voice assistant**, **browser automation**, **home automation**, and **cron scheduling**

### Core Architecture (6 Layers)

| Layer | Purpose |
|-------|---------|
| **Gateway** | Central control plane — message routing, sessions, plugins, tool execution policy |
| **Channels** | Adapters normalizing Telegram/WhatsApp/Discord/iMessage into standard message shapes |
| **Routing + Sessions** | Determines which agent handles specific conversations |
| **Agent Runtime** | Processes context, calls model providers, streams responses, requests tools |
| **Tools** | Capabilities — web fetch, browser control, command execution, device pairing |
| **Surfaces** | Interaction points — chat apps, web dashboard, macOS menu bar, Live Canvas |

### Name History

| Date | Name | Reason |
|------|------|--------|
| Nov 2025 | **Clawdbot** | Original name at launch |
| Jan 27, 2026 | **Moltbot** | Anthropic trademark complaint (similarity to "Claude") |
| Jan 30, 2026 | **OpenClaw** | Final rebrand, community vote |

> When the team dropped the @clawdbot Twitter handle to transition to @moltbot, professional "handle snipers" immediately grabbed it. Scammers used the hijacked account to launch a fake CLAWD token on Solana.

### GitHub Growth Stats

| Project | Stars | Age | Time to 100K Stars | Stars/Day (avg) |
|---------|-------|-----|---------------------|-----------------|
| **OpenClaw** | **195K** | **~4 months** | **~2 days** | **~1,625** |
| React | 242K | 12 years | ~8 years | ~55 |
| Linux | 216K | 15 years | ~12 years | ~39 |
| Next.js | 137K | 9 years | ~8 years | ~41 |
| Kubernetes | 120K | 11 years | ~10 years | ~29 |

> OpenClaw reached 100K stars in ~2 days (Jan 29–30, 2026) — peak growth hit **710 stars/hour**. It is the fastest GitHub repo to reach 100K stars in history.

---

## 2. Quick Start & Setup Methods

### System Requirements

**Minimum:**
| Component | Requirement |
|-----------|-------------|
| OS | macOS 11+ / Ubuntu 22.04+ / Windows (WSL2) |
| Runtime | Node.js 22+ |
| RAM | 2 GB (may crash during onboarding) |
| CPU | 2 cores |
| Storage | 10 GB SSD |

**Recommended:**
| Component | Requirement |
|-----------|-------------|
| RAM | 4–8 GB (cloud models) / 16–24 GB (local LLMs) |
| CPU | 2–4 cores |
| Storage | 30–50 GB SSD |
| GPU | 12–24 GB VRAM (for local model inference) |

### Quick Start (1 Minute)

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
openclaw gateway --port 18789 --verbose
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
| **Railway** | [Template](https://railway.com/deploy/openclaw) | Web-based /setup wizard |
| **DigitalOcean** | [1-Click Deploy](https://marketplace.digitalocean.com/apps/openclaw) | Security-hardened, pre-configured |
| **Render** | [render.yaml](https://docs.openclaw.ai/render) | Infrastructure as Code |
| **SimpleClaw** | [simpleclaw.com](https://www.simpleclaw.com/) | Deploy in under 1 minute |
| **Zeabur** | [Template](https://zeabur.com/templates/VTZ4FX) | One-click Docker deploy |
| **Northflank** | [Stack](https://northflank.com/stacks/deploy-openclaw) | No server-side terminal needed |
| **Lightning.AI** | [Environment](https://lightning.ai/lightning-ai/environments/openclaw) | Browser-based, no local hardware |
| **Coolify** | [Template](https://github.com/essamamdani/openclaw-coolify) | Self-hosted PaaS template |
| **Elestio** | [Open Source](https://elest.io/open-source/openclaw) | Fully managed in < 3 min |

### Comparable AI Agent Products

| # | Product | Website | Type | Self-Host | Messaging Platforms |
|---|---------|---------|------|-----------|---------------------|
| 1 | **Hermes Agent** | [hermesagent.studio](https://hermesagent.studio/) | Autonomous agent + messaging hub | ✅ | WhatsApp, Telegram, Slack, Discord, and more |
| 2 | **Multica** | [multica.uk](https://multica.uk/) | Multi-channel AI automation | ✅ | Multi-platform |
| 3 | **AutoGPT** | [agpt.co](https://agpt.co/) | Autonomous task agent | ✅ | API / web UI |
| 4 | **LangChain** | [langchain.com](https://www.langchain.com/) | LLM orchestration framework | ✅ | Any (via custom integrations) |
| 5 | **n8n** | [n8n.io](https://n8n.io/) | Workflow automation + AI nodes | ✅ | Slack, Telegram, Discord, and 400+ apps |
| 6 | **AgentGPT** | [agentgpt.reworkd.ai](https://agentgpt.reworkd.ai/) | Browser-based autonomous agent | ✅ | Web UI |
| 7 | **CrewAI** | [crewai.com](https://www.crewai.com/) | Multi-agent role collaboration | ✅ | API / custom integrations |
| 8 | **SuperAGI** | [superagi.com](https://superagi.com/) | Autonomous agent infrastructure | ✅ | Slack, Email, API |

---

### All Setup Methods at a Glance

| Method | Time | Difficulty | Best For |
|--------|------|------------|----------|
| **[Agent37](https://www.agent37.com/openclaw)** | 30 sec | Easy | Cheapest managed ($0.99/mo) |
| **[SimpleClaw](https://www.simpleclaw.com/)** | 1 min | Easy | Non-technical users |
| **[npm install](https://docs.openclaw.ai/quickstart)** | 1 min | Easy | Developers with Node.js |
| **[DigitalOcean 1-Click](https://marketplace.digitalocean.com/apps/openclaw)** | 2 min | Easy | Quick cloud deploy |
| **[Railway Template](https://railway.com/deploy/openclaw)** | 2 min | Easy | PaaS users |
| **[Zeabur](https://zeabur.com/templates/VTZ4FX)** | 1 min | Easy | Docker auto-deploy |
| **[Docker](https://docs.openclaw.ai/docker)** | 5 min | Medium | Isolation & reproducibility |
| **[Cloudflare Workers](https://docs.openclaw.ai/cloudflare)** | 5 min | Medium | Serverless enthusiasts |
| **[xCloud Managed](https://xcloud.host/openclaw-hosting)** | 5 min | None | Full managed hosting |
| **[Kimi Claw](https://kimi.com/bot)** | Instant | None | Browser-native, 5K+ skills, 40 GB storage |
| **[Molty by Finna](https://molty.finna.ai)** | 30 sec | None | Multiple Molties, Mission Control, GitHub sync |
| **[Manual VPS](https://docs.openclaw.ai/vps)** | 10 min | Medium | Full control |
| **[Raspberry Pi](https://docs.openclaw.ai/raspberry-pi)** | 10 min | Medium | Low-power, always-on |
| **[ESP32-S3 (MimiClaw)](https://github.com/memovai/mimiclaw)** | 10 min | Medium | Cheapest hardware ($5), pure C, no OS |
| **[PicoClaw (RISC-V)](https://github.com/sipeed/picoclaw)** | 5 min | Easy | Single Go binary, 10 MB RAM, $10 board |
| **[ZeroClaw (Rust)](https://github.com/theonlyhennygod/zeroclaw)** | 2 min | Easy | 3.4 MB binary, <10ms startup, 22+ providers |
| **[TinyClaw (Shell)](https://github.com/jlia0/tinyclaw)** | 5 min | Easy | 400 LoC, Claude Code + tmux, self-healing |
| **[Autobot (Crystal)](https://github.com/crystal-autobot/autobot)** | 2 min | Easy | 2MB binary, ~5MB RAM, <10ms startup |

---

## 3. Hosting & Deployment

### 3.1 Free Tier ($0/month)

| Provider | Free Resources | Limits | Permanent? | Setup Time | Best For |
|----------|---------------|--------|------------|------------|----------|
| **[Oracle Cloud](https://www.oracle.com/cloud/free/)** | 4 ARM CPUs, 24 GB RAM, 200 GB storage, 10 TB/mo | ARM architecture only | Yes (forever) | ~3 hours | Power users wanting $0 hosting |
| **[AMD Developer Cloud](https://www.amd.com/en/developer/resources/cloud-access.html)** | MI300X GPU (192 GB memory), $100 credits | ~50 hours compute | No (credits) | 30 min | GPU-accelerated local LLMs |
| **[Google Cloud Run](https://cloud.google.com/run)** | 180K vCPU-sec, 360K GiB-sec, 2M requests/mo | Cold starts, stateless | Yes | 30 min | Serverless testing |
| **[Azure Container Apps](https://azure.microsoft.com/en-us/products/container-apps)** | 180K vCPU-sec, 360K GiB-sec, 2M requests/mo | Cold starts | Yes | 30 min | Enterprise users |
| **[Render](https://render.com/)** | Web service (spins down after 15 min) | Slow wake-up (~60s) | Yes | 5 min | Testing only |
| **[AWS Free Tier](https://aws.amazon.com/free/)** | t2.micro (1 vCPU, 1 GB RAM) | 12 months only | No (12 mo) | 15 min | AWS-familiar users |
| **[Railway](https://railway.com/deploy/openclaw)** | $5 one-time credit | 30 days trial | No | 2 min | Quick testing |

### 3.2 Budget VPS ($2–8/month)

| Provider | Plan | Price/mo | vCPU | RAM | Storage | Bandwidth | Region |
|----------|------|----------|------|-----|---------|-----------|--------|
| **[LumaDock](https://lumadock.com/)** | Basic | $1.99 | 1 | 1 GB | 20 GB SSD | 1 TB | US/EU |
| **[Vultr](https://www.vultr.com/)** | Regular Cloud | $2.50 | 1 | 512 MB | 10 GB | 0.5 TB | 32 locations |
| **[Vultr](https://www.vultr.com/)** | Standard | $3.50 | 1 | 1 GB | 25 GB NVMe | 1 TB | 32 locations |
| **[Hetzner](https://www.hetzner.com/cloud/)** | CX22 | €3.79 (~$4.15) | 2 | 4 GB | 40 GB SSD | 20 TB | EU (DE/FI) |
| **[Alibaba Cloud](https://www.alibabacloud.com/en/campaign/ai-openclaw)** | Simple App Server | $4 | 1 | 1 GB | Varies | Varies | 19 regions |
| **[Contabo](https://contabo.com/en/openclaw-hosting/)** | Cloud VPS S | $4.95 | 4 | 8 GB | 50 GB SSD | Unlimited | US/EU/Asia |
| **[Hostinger](https://www.hostinger.com/uk/vps/docker/openclaw)** | KVM 1 | $4.99 | 1 | 4 GB | 50 GB NVMe | 4 TB | Global |
| **[Linode](https://www.linode.com/)** | Shared 1GB | $5 | 1 | 1 GB | 25 GB | 1 TB | Global |
| **[Vultr](https://www.vultr.com/)** | High-Performance | $6 | 1 | 1 GB | 25 GB NVMe | 2 TB | 32 locations |
| **[DigitalOcean](https://marketplace.digitalocean.com/apps/openclaw)** | Basic Droplet | $6 | 1 | 1 GB | 25 GB | 1 TB | Global |
| **[Hetzner](https://www.hetzner.com/cloud/)** | CX32 | €6.80 (~$7.45) | 4 | 8 GB | 80 GB SSD | 20 TB | EU (DE/FI) |
| **[Contabo](https://contabo.com/en/openclaw-hosting/)** | Cloud VPS M | $7.95 | 4 | 8 GB | 200 GB SSD | Unlimited | US/EU/Asia |

### 3.3 Mid-Range ($5–25/month)

| Provider | Plan | Price/mo | vCPU | RAM | Storage | Notes |
|----------|------|----------|------|-----|---------|-------|
| **[DigitalOcean](https://marketplace.digitalocean.com/apps/openclaw)** | Premium Droplet | $7 | 1 | 1 GB | 25 GB NVMe | 1-Click Deploy available |
| **[DigitalOcean](https://marketplace.digitalocean.com/apps/openclaw)** | Standard 2GB | $12 | 1 | 2 GB | 50 GB | Recommended for OpenClaw |
| **[Hostinger](https://www.hostinger.com/uk/vps/docker/openclaw)** | KVM 2 | $6.99 | 2 | 8 GB | 100 GB NVMe | Best Hostinger value |
| **[GCP](https://cloud.google.com/compute)** | e2-medium | ~$12 | 2 | 4 GB | 30 GB SSD | $300 free credit (90 days) |
| **[Azure](https://azure.microsoft.com/en-us/products/virtual-machines)** | B1ms VM | ~$15 | 1 | 2 GB | 32 GB | Enterprise compliance |
| **[Linode](https://www.linode.com/)** | Dedicated 4GB | $36 | 2 (dedicated) | 4 GB | 40 GB | Consistent performance |

### 3.4 Serverless & PaaS

| Platform | Starting Price | Free Tier? | Persistent Storage | Auto-Scale | Notes |
|----------|---------------|------------|-------------------|------------|-------|
| **[Cloudflare Workers](https://workers.cloudflare.com/)** | $5/mo (paid plan) | 100K req/day (free) | R2 ($0.015/GB/mo) | Yes | Moltworker PoC |
| **[Railway](https://railway.com/deploy/openclaw)** | $5/mo (Hobby) | $5 credit trial | Yes (volumes) | Yes | Best PaaS UX |
| **[Render](https://render.com/)** | $7/mo (web service) | Free w/ limits | Yes (disks) | Yes | YAML IaC |
| **[Fly.io](https://fly.io/)** | Pay-as-you-go | None | Yes (volumes) | Yes | Global edge |
| **[AWS Lightsail](https://aws.amazon.com/lightsail/)** | $3.50/mo | None | Yes | No | Simple AWS VPS |
| **[Northflank](https://northflank.com/stacks/deploy-openclaw)** | Varies | Limited | Yes | Yes | Stack templates |
| **[Zeabur](https://zeabur.com/templates/VTZ4FX)** | Varies | Limited | Yes | Yes | One-click Docker |
| **[Elestio](https://elest.io/open-source/openclaw)** | Varies | None | Yes | Yes | Fully managed open source |
| **[Coolify](https://github.com/essamamdani/openclaw-coolify)** | Self-hosted | Free (self-host) | Yes | No | Open-source PaaS |

### 3.5 Managed Hosting Services

These providers handle ALL the setup for you — no Docker, no terminal, no DevOps required.

| Provider | Price/mo | Setup Time | Specs | What's Included | Promo |
|----------|----------|------------|-------|-----------------|-------|
| **[Agent37](https://www.agent37.com/openclaw)** | $0.99–3.99 | 30 sec | 2 vCPU, 4–6 GB RAM | Isolated instance, full UI, terminal, SSL | — |
| **[MyClaw.ai](https://myclaw.ai/pricing)** | $9 (was $29) | Instant | 2 vCPU, 4 GB RAM, 40 GB SSD | Auto-updates, backups, web terminal | 69–76% off early bird |
| **[get-open-claw.com](https://www.get-open-claw.com/)** | $9–49 | < 1 min | Varies by plan | OpenClaw Secure, daily backups, health monitoring | Pro includes $10 AI credits |
| **[EasyClaw](https://www.easyclaw.pro/en)** | $10+ | 60 sec | Varies | Multi-model, 3+ platforms, zero maintenance | 29 min saved per deploy |
| **[ClawSimple](https://clawsimple.com/en)** | $8.25–29.08 | 2–3 min | Varies | Secure cloud, one-click updates (coming) | 20% off with LAUNCH20 |
| **[xCloud](https://xcloud.host/openclaw-hosting)** | $24 | 5 min | Managed | Telegram/WhatsApp pre-configured, encrypted backups | 7-day guarantee |
| **[ClawCloud](https://www.clawcloud.sh/)** | $29–129 | < 1 min | 1–2 vCPU, 1–4 GB RAM | All AI models (BYOK), auto-updates, daily backups | 70% off with EARLYBIRD70 |
| **[SimpleClaw](https://www.simpleclaw.com/)** | TBD | < 1 min | Managed | 1-click deploy, model selection | — |
| **[OpenClaw Cloud](https://openclawcloud.work/)** | Beta pricing | 5 min | Managed | All AI tokens included, 99.9% uptime, $0 hidden fees | Waitlist open |
| **[OpenClawd.ai](https://openclawd.ai)** | Free + Premium | Minutes | Managed | Fully managed, one-click deploy, security built-in, free tier available | — |
| **[Kimi Claw](https://kimi.com/bot)** | Allegretto+ | Instant | Browser-native | 5,000+ ClawHub skills, 40 GB cloud storage, BYOC | Beta open |
| **[Kilo Claw](https://kilo.ai/kiloclaw)** | Pay-as-you-go | < 60 sec | Managed | 500+ models, 50+ platforms, SSO, audit logs | 7 days free compute |
| **[OpenClaw Hosting](https://openclawhosting.io/pricing)** | $29+ | 5 min | Managed | Solo/Team/Business tiers, annual billing saves 20% | — |
| **[Myclawhost](https://www.myclawhost.com/)** | $9–39 | Instant | Managed | Lite ($9), Pro ($19), Max ($39), full lifecycle | One-click deploy |
| **[Contabo OpenClaw](https://contabo.com/en/openclaw-hosting/)** | $4.95+ | Minutes | VPS | Unlimited workflows, full data ownership | — |
| **[Molty by Finna](https://molty.finna.ai)** | $19–99 | 30 sec | VM-isolated (Fly.io) | Multiple Molties, Mission Control, GitHub sync, browser automation | 3-day free trial |
| **[ClawLaunch](https://clawlaunch.ai)** | Free (30d) / $9.49 | 60 sec | Varies | AI Credits, gVisor sandbox, free Whisper TTS | 30-day free trial, 50% revshare affiliate |
| **[OpenClaw Setup](https://openclaw-setup.me)** | $3.9 (Solo) / $6.9 (Trio) | ~2 min | 1 CPU, 3–12 GB RAM | Full UI, LLM providers config, Telegram + Slack, encrypted credentials, per-model analytics | AWESOMEOPENCLAWSETUP (50% off) |

### 3.6 Setup-as-a-Service (Freelancers)

Hire someone to set it up for you.

| Provider | Price | Type | What's Included |
|----------|-------|------|-----------------|
| **[GetClawHelp](https://getclawhelp.com/)** | $119–229 (one-time) | 1-on-1 video call | VPS setup, LLM config, 10–25 skills, 24/7 uptime |
| **[GetClawHelp Maintenance](https://getclawhelp.com/)** | $97/mo | Monthly | Updates, troubleshooting, new skills |
| **Fiverr - [almaasparvez](https://www.fiverr.com/almaasparvez)** | $90 | One-time | OpenClaw on AWS VPS, Telegram setup |
| **Fiverr - marcos_mark683** | $40 | One-time | OpenClaw installation |
| **[Upwork - Custom Skills](https://www.upwork.com/services/product/development-it-openclaw-ai-agent-setup-with-custom-skills-2018301653307508886)** | Varies | One-time | Up to 23 custom skills, testing, step-by-step guide |
| **[Upwork - Secure Deploy](https://www.upwork.com/services/product/development-it-secure-openclaw-clawdbot-deployment-mac-mini-or-vps-approval-gates-2019127245731633908)** | Varies | One-time | Mac Mini/VPS, sandboxing, human-in-the-loop approval gates |
| **[Freelancer.com](https://www.freelancer.com/projects/automation/OpenClaw-Linux-Setup.html)** | Varies | One-time | Linux setup, tuning, README |
| **[OpenClaw Money Playbook](https://openclawmoney.com/)** | $9.95 | E-book | Guide on monetizing OpenClaw setup services |

> **Business Model Insight**: *"The move right now is doing free OpenClaw installs, upselling security/skill packages/custom builds. We still make money on a 'free' install because we get an affiliate commission from the hosting company."* — [@GanimCorey on X](https://x.com/GanimCorey)

### 3.7 Master Cost Comparison Table

| Provider | Monthly Cost | Setup Time | Difficulty | 1-Click? | Best For |
|----------|-------------|------------|------------|----------|----------|
| [Oracle Cloud](https://www.oracle.com/cloud/free/) | **$0** | 3 hours | Hard | No | Free-forever hosting |
| [AMD Dev Cloud](https://www.amd.com/en/developer/resources/cloud-access.html) | **$0** (credits) | 30 min | Medium | No | Free GPU inference |
| [Agent37](https://www.agent37.com/openclaw) | **$0.99** | 30 sec | **None** | **Yes** | Cheapest managed |
| [LumaDock](https://lumadock.com/) | **$1.99** | 15 min | Medium | No | Cheapest VPS |
| [Vultr](https://www.vultr.com/) | **$2.50** | 10 min | Medium | Yes | Global presence |
| [Hetzner CX22](https://www.hetzner.com/cloud/) | **$4.15** | 10 min | Medium | No | Best price/performance |
| [Contabo VPS S](https://contabo.com/en/openclaw-hosting/) | **$4.95** | 15 min | Medium | No | Unlimited bandwidth |
| [Hostinger KVM 1](https://www.hostinger.com/uk/vps/docker/openclaw) | **$4.99** | 10 min | Easy | Yes | Docker templates |
| [Cloudflare Workers](https://workers.cloudflare.com/) | **$5** | 5 min | Medium | No | Serverless |
| [Railway Hobby](https://railway.com/deploy/openclaw) | **$5** | 2 min | Easy | Yes | Best PaaS experience |
| [Linode 1GB](https://www.linode.com/) | **$5** | 10 min | Medium | No | Consistent performance |
| [DigitalOcean](https://marketplace.digitalocean.com/apps/openclaw) | **$6** | 2 min | Easy | **Yes** | Best docs + 1-Click |
| [Render](https://render.com/) | **$7** | 5 min | Easy | Yes | YAML Infrastructure |
| [MyClaw.ai Lite](https://myclaw.ai/pricing) | **$9** | Instant | **None** | **Yes** | Budget managed |
| [DigitalOcean 2GB](https://marketplace.digitalocean.com/apps/openclaw) | **$12** | 2 min | Easy | **Yes** | Recommended production |
| [Molty by Finna](https://molty.finna.ai) | **$19** | 30 sec | **None** | **Yes** | Multi-Molty, Mission Control |
| [xCloud Managed](https://xcloud.host/openclaw-hosting) | **$24** | 5 min | **None** | **Yes** | Full managed hosting |
| [ClawCloud Starter](https://www.clawcloud.sh/) | **$29** | < 1 min | **None** | **Yes** | Premium managed |
| [Raspberry Pi 5](https://docs.openclaw.ai/raspberry-pi) | **$0**/mo | 30 min | Medium | No | After $80 hardware purchase |
| [ESP32-S3 (MimiClaw)](https://github.com/memovai/mimiclaw) | **$0**/mo | 10 min | Medium | No | After $5 hardware purchase |
| [PicoClaw (RISC-V)](https://github.com/sipeed/picoclaw) | **$0**/mo | 5 min | Easy | No | After $10 hardware purchase |
| [ZeroClaw (Rust)](https://github.com/theonlyhennygod/zeroclaw) | **$0**/mo | 2 min | Easy | No | 3.4 MB binary, <10ms startup |
| [TinyClaw (Shell)](https://github.com/jlia0/tinyclaw) | **$0**/mo | 5 min | Easy | No | 400 LoC, Claude Code + tmux |
| [Autobot (Crystal)](https://github.com/crystal-autobot/autobot) | **$0**/mo | 2 min | Easy | No | Crystal, <10ms startup |
| Mac Mini | **$0**/mo | 10 min | Easy | No | Privacy-first, local |

---

## 4. Platform-Specific Deployment Guides

### DigitalOcean 1-Click Deploy

The fastest path to a production OpenClaw instance.

1. Go to [DigitalOcean Marketplace](https://marketplace.digitalocean.com/apps/openclaw)
2. Click "Create OpenClaw Droplet"
3. Choose $12/mo plan (2 GB RAM recommended)
4. Select region, SSH key
5. Deploy (ready in ~90 seconds)

**Pre-configured**: OpenClaw 2026.1.24-1, Docker isolation, unique gateway token, security-hardened, Caddy HTTPS.

- [DigitalOcean Blog - Introducing OpenClaw](https://www.digitalocean.com/blog/moltbot-on-digitalocean)
- [Technical Deep Dive - Security Hardening](https://www.digitalocean.com/blog/technical-dive-openclaw-hardened-1-click-app)
- [Tutorial - How to Run OpenClaw](https://www.digitalocean.com/community/tutorials/how-to-run-openclaw)

### Hetzner Setup Guide

Best price-to-performance ratio for OpenClaw hosting.

| Plan | Price/mo | vCPU | RAM | Storage | Bandwidth |
|------|----------|------|-----|---------|-----------|
| **CX22** | €3.79 | 2 | 4 GB | 40 GB SSD | 20 TB |
| **CX32** | €6.80 | 4 | 8 GB | 80 GB SSD | 20 TB |
| **CAX11 (ARM)** | €3.79 | 2 | 4 GB | 40 GB | 20 TB |

```bash
ssh root@your-server-ip
curl -fsSL https://deb.nodesource.com/setup_22.x | bash -
apt-get install -y nodejs
npm install -g openclaw@latest
openclaw onboard --install-daemon
ufw allow ssh && ufw allow 443/tcp && ufw enable
```

- [Hetzner - OpenClaw Docs](https://docs.openclaw.ai/platforms/hetzner)
- [Deploy with Pulumi + Tailscale](https://www.pulumi.com/blog/deploy-openclaw-aws-hetzner/)

### Hostinger VPS Setup

| Plan | Price/mo | vCPU | RAM | Storage | Bandwidth |
|------|----------|------|-----|---------|-----------|
| **KVM 1** | $4.99 | 1 | 4 GB | 50 GB NVMe | 4 TB |
| **KVM 2** | $6.99 | 2 | 8 GB | 100 GB NVMe | 8 TB |
| **KVM 4** | $10.99 | 4 | 16 GB | 200 GB NVMe | 16 TB |

> Renewal prices are ~2x. Lock in annual pricing.

- [How to Install OpenClaw on Hostinger VPS](https://www.hostinger.com/support/how-to-install-openclaw-on-hostinger-vps/)
- [How to Secure OpenClaw on Hostinger](https://www.hostinger.com/support/how-to-secure-and-harden-openclaw-security/)
- [25 OpenClaw Use Cases](https://www.hostinger.com/tutorials/openclaw-use-cases)

### Oracle Cloud Free Tier Setup

**Truly free forever** — 4 ARM cores, 24 GB RAM, 200 GB storage, 10 TB/month.

```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | bash -
apt-get install -y nodejs git
npm install -g openclaw@latest
openclaw onboard --install-daemon
```

**Caveats**: ARM architecture, high demand (keep retrying), add credit card to prevent account termination.

- [Oracle Cloud - OpenClaw Docs](https://docs.openclaw.ai/platforms/oracle)
- [Always-On AI for $0/month](https://ryanshook.org/blog/posts/openclaw-on-oracle-free-tier-always-on-ai-for-free/)
- [Self-Host on a Free VPS](https://cognio.so/clawdbot/self-hosting)

### Raspberry Pi Setup

| Device | Price | RAM | Performance |
|--------|-------|-----|-------------|
| **Pi 5 (8 GB)** | $80 | 8 GB | Best choice |
| **Pi 5 (4 GB)** | $60 | 4 GB | Good budget option |
| **Pi 4 (8 GB)** | $55 | 8 GB | 2–2.5x slower than Pi 5 |

```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo bash -
sudo apt-get install -y nodejs
npm install -g openclaw@latest
openclaw onboard --install-daemon
```

- [OpenClaw on Raspberry Pi - ajfisher](https://ajfisher.me/2026/02/03/openclaw-raspberrypi-howto/)
- [OpenClaw on Raspberry Pi - Adafruit](https://learn.adafruit.com/openclaw-on-raspberry-pi)

### ESP32 Embedded (MimiClaw)

[MimiClaw](https://github.com/memovai/mimiclaw) implements OpenClaw's core principles on a **$5 ESP32-S3** microcontroller. Written entirely in pure C — no Linux, no Node.js, no server infrastructure needed.

| Spec | Detail |
|------|--------|
| **Hardware** | ESP32-S3 (16 MB flash, 8 MB PSRAM) |
| **Cost** | ~$5 (chip only) |
| **Language** | Pure C (ESP-IDF v5.5+) |
| **AI Backend** | Anthropic Claude API with ReAct agent loop |
| **Messaging** | Telegram |
| **Features** | Tool use, dual-core processing, WebSocket gateway, runtime CLI config |

### Cloudflare Workers (Moltworker) Deep Dive

[Moltworker](https://github.com/cloudflare/moltworker) is Cloudflare's official adaptation of OpenClaw for Workers.

**Architecture:**
- **Container**: Sandbox (standard-1: 1/2 vCPU, 4 GiB RAM, 8 GB disk)
- **Storage**: R2 for persistence (auto-sync every 5 minutes)
- **Auth**: Cloudflare Access (Zero Trust) + gateway token + device pairing
- **Status**: Proof-of-concept (not an official Cloudflare product)

**Setup:**
```bash
git clone https://github.com/cloudflare/moltworker.git
cd moltworker && npm install
npx wrangler secret put ANTHROPIC_API_KEY
export MOLTBOT_GATEWAY_TOKEN=$(openssl rand -hex 32)
npx wrangler secret put MOLTBOT_GATEWAY_TOKEN
npm run deploy
```

**Cost Breakdown (24/7 Operation):**

| Component | Monthly Cost |
|-----------|-------------|
| Workers Paid Plan | $5.00 |
| Memory (~4 GiB) | ~$26.00 |
| CPU | ~$2.00 |
| Disk (8 GB) | ~$1.50 |
| **Total** | **~$34.50** |

> Set `SANDBOX_SLEEP_AFTER=10m` for infrequent use to reduce costs significantly.

> **Limitation**: Cannot support Telegram bots (requires persistent connection for long-polling). Use VPS deployment for Telegram integration.

- [GitHub - cloudflare/moltworker](https://github.com/cloudflare/moltworker)
- [Blog - Introducing Moltworker](https://blog.cloudflare.com/moltworker-self-hosted-ai-agent/)

### Docker Deployment

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw && ./docker-setup.sh
```

**Useful Commands:**
```bash
docker compose run --rm openclaw-cli pairing approve telegram <CODE>
docker compose run --rm openclaw-cli dashboard --no-open
docker compose run --rm openclaw-cli security audit --deep
```

- [Docker - OpenClaw Docs](https://docs.openclaw.ai/install/docker)
- [Running OpenClaw in Docker - Simon Willison](https://til.simonwillison.net/llms/openclaw-docker)
- [Docker Guide for Beginners - Medium](https://medium.com/@ozbillwang/run-openclaw-moltbot-clawdbot-safely-with-docker-a-practical-guide-for-beginners-94112a9b57be)

### PicoClaw (RISC-V / Ultra-Lightweight)

[PicoClaw](https://github.com/sipeed/picoclaw) is an ultra-lightweight AI assistant in Go that runs on less than **10 MB RAM**. Boots in **1 second** on a **$10 RISC-V board** (Sipeed LicheeRV Nano).

| Spec | Detail |
|------|--------|
| **Language** | Go |
| **RAM** | < 10 MB |
| **Hardware** | Sipeed LicheeRV Nano ($10); also ARM64 and x86-64 |
| **Boot Time** | ~1 second |
| **Stars** | 5,000+ |
| **Messaging** | Telegram, Discord, QQ, DingTalk |
| **AI Providers** | Gemini, Anthropic, OpenRouter, local LLMs |
| **Features** | Persistent memory, scheduled tasks, web search, multi-provider routing |

> Sipeed claims PicoClaw matches OpenClaw's core features with 1% of the code and 1% of the memory.

- [GitHub - sipeed/picoclaw](https://github.com/sipeed/picoclaw)
- [CNX Software - PicoClaw runs on just 10MB of RAM](https://www.cnx-software.com/2026/02/10/picoclaw-ultra-lightweight-personal-ai-assistant-run-on-just-10mb-of-ram/)

---

## 5. Cost Analysis

### AI Model API Pricing (per 1M tokens)

The **real cost** of running OpenClaw is the AI model API, not infrastructure.

| Provider | Model | Input Cost | Output Cost | Notes |
|----------|-------|-----------|-------------|-------|
| **[Anthropic](https://console.anthropic.com/)** | Claude 3.5 Haiku | $0.80 | $4.00 | Best budget option |
| **[Anthropic](https://console.anthropic.com/)** | Claude 3.5 Sonnet | $3.00 | $15.00 | Best balance |
| **[Anthropic](https://console.anthropic.com/)** | Claude Opus 4.5 | $15.00 | $75.00 | Most capable, expensive |
| **[OpenAI](https://platform.openai.com/)** | GPT-4o | $2.50 | $10.00 | Good alternative |
| **[OpenAI](https://platform.openai.com/)** | GPT-4o-mini | $0.15 | $0.60 | Very cheap |
| **[Google](https://aistudio.google.dev/)** | Gemini 2.0 Flash | $0.10 | $0.40 | Cheapest hosted |
| **[Google](https://aistudio.google.dev/)** | Gemini Flash-Lite | **Free tier** | **Free tier** | Zero cost option |
| **[DeepSeek](https://platform.deepseek.com/)** | DeepSeek V3 | $0.27 | $1.10 | Best value reasoning |
| **[Moonshot](https://platform.moonshot.cn/)** | Kimi K2.5 | $3.00 | $3.00 | Free built-in since v2026.2.6 |
| **[Grok](https://console.x.ai/)** | Grok 4.1 mini | $0.20 | $0.50 | Budget alternative |
| **[OpenRouter](https://openrouter.ai/)** | Various | Varies | Varies | Unified API for 200+ models |
| **[Ollama](https://ollama.com/)** | Any | **$0** | **$0** | Requires hardware (16 GB+ RAM) |

> **75x price difference** between the most expensive (Claude Opus) and cheapest (Gemini Flash) options.

### Monthly API Cost Estimates

| Usage Level | Description | Monthly Cost |
|-------------|-------------|-------------|
| **Minimal** | Few messages/day, Gemini free tier | $0–5 |
| **Light** | ~50 messages/day, Claude Haiku | $5–15 |
| **Moderate** | ~200 messages/day, mixed models | $15–50 |
| **Heavy** | 500+ messages/day, Claude Sonnet | $50–150 |
| **Power User** | All-day usage, Claude Opus | $150–500+ |

### Total Real-World Cost Examples

| Setup | Infrastructure | API | Total/month | Notes |
|-------|---------------|-----|-------------|-------|
| **Free Tier Max** | Oracle Cloud ($0) | Gemini free ($0) | **$0** | Limited but functional |
| **Cheapest Managed** | Agent37 ($1) | Haiku ($5) | **$6** | 30-second setup |
| **Ultra Budget** | LumaDock ($2) | Haiku ($5) | **$7** | Basic personal assistant |
| **Budget Managed** | MyClaw.ai Lite ($9) | BYOK ($10) | **$19** | Zero setup, instant access |
| **Sweet Spot** | Hetzner CX22 ($4) | Mixed models ($15) | **$19** | Best value-to-capability |
| **Standard** | DigitalOcean ($12) | Sonnet ($40) | **$52** | Production-ready |
| **Managed Easy** | xCloud ($24) | Mixed ($30) | **$54** | Zero technical setup |
| **Cloudflare** | Workers ($5+$30) | Mixed ($20) | **$55** | Serverless architecture |
| **Local LLM** | Raspberry Pi 5 ($0/mo) | Ollama ($0) | **$0** | After $80 hardware purchase |
| **Embedded** | ESP32-S3 ($0/mo) | Claude API ($5) | **$5** | After $5 hardware purchase |
| **PicoClaw** | RISC-V board ($0/mo) | Gemini/Claude ($5) | **$5** | After $10 hardware purchase |
| **Power User** | DigitalOcean ($24) | Opus ($200) | **$224** | Heavy professional use |
| **Extreme** | Dedicated ($50) | All models ($573) | **$623** | One developer's real report |

### Cost Optimization Tips

1. Use **smart model routing** — cheap models (Haiku/Flash) for simple tasks, expensive (Sonnet/Opus) for complex
2. Enable **prompt caching** — Anthropic auto-applies 5-min cache, reducing repeat costs
3. Use **local LLMs** via Ollama for zero API cost (requires 16 GB+ RAM)
4. Set **budget alerts** in your AI provider dashboard
5. Use [OpenClaw Cost Calculator](https://calculator.vlvt.sh/) to estimate your spend

### Monthly Budget Targets

| Budget | Strategy |
|--------|----------|
| **$0** | Oracle Cloud + Gemini free tier + Ollama |
| **$6** | Agent37 ($1) + Claude Haiku ($5) |
| **$19** | Hetzner ($4) + mixed models ($15) |
| **$50** | DigitalOcean ($12) + Claude Sonnet ($38) |
| **$100** | Managed hosting ($24) + heavy API ($76) |

---

## 6. Configuration

### Model Providers

| Provider | Config Key | Free Tier? | Notes |
|----------|-----------|------------|-------|
| **Anthropic** | `ANTHROPIC_API_KEY` | No | Primary, best quality |
| **OpenAI** | `OPENAI_API_KEY` | No | GPT-4, GPT-4o |
| **Google** | `GOOGLE_API_KEY` | Yes (Gemini Flash-Lite) | Cheapest hosted |
| **OpenRouter** | `OPENROUTER_API_KEY` | No | 200+ models unified API |
| **DeepSeek** | `DEEPSEEK_API_KEY` | No | Excellent value |
| **Moonshot** | `MOONSHOT_API_KEY` | No | Kimi K2.5 (great agentic) |
| **MiniMax** | `MINIMAX_API_KEY` | No | M2.1 native support |
| **Ollama** | Local | **Free** | Requires local hardware |
| **LM Studio** | Local | **Free** | Requires local hardware |
| **vLLM** | Local | **Free** | High-performance inference |

### Messaging Channels

| Channel | Setup | Auth Method | Notes |
|---------|-------|-------------|-------|
| **Telegram** | 2 min | BotFather token | Fastest setup, supports Topics for parallel threads |
| **WhatsApp** | 2 min | QR code scan | Separate phone number recommended |
| **Discord** | 5 min | Bot application | Developer portal required |
| **Slack** | 5 min | Bot token (Socket or HTTP mode) | api.slack.com/apps |
| **Signal** | 5 min | Direct integration | Privacy-focused |
| **iMessage** | 10 min | BlueBubbles bridge | macOS only |
| **Microsoft Teams** | 5 min | Enterprise integration | Business users |
| **Google Chat** | 5 min | Workspace integration | Google Workspace |
| **Matrix** | 5 min | E2E encryption | Best for privacy |
| **Zalo** | 5 min | Direct integration | Popular in Vietnam |
| **WebChat** | Built-in | Gateway token | Browser-based interface |

### Local LLM Integration

**Ollama:**
```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama pull llama3.1
```
```json
{ "provider": "openai", "baseUrl": "http://localhost:11434/v1", "model": "llama3.1" }
```

**LM Studio:**
```json
{ "provider": "openai", "baseUrl": "http://localhost:1234/v1", "model": "your-model-name" }
```

**vLLM (GPU-Accelerated):**
```json
{ "provider": "openai", "baseUrl": "http://localhost:8000/v1", "model": "your-model-name" }
```

- [OpenClaw + Ollama Guide](https://codersera.com/blog/openclaw-ollama-setup-guide-2026/)
- [OpenClaw + LM Studio Guide](https://codersera.com/blog/openclaw-lm-studio-setup-guide-2026/)
- [OpenClaw + vLLM on AMD](https://www.amd.com/en/developer/resources/technical-articles/2026/openclaw-with-vllm-running-for-free-on-amd-developer-cloud-.html)

### MCP Server Integration

| Plugin | Source | Features |
|--------|--------|----------|
| **openclaw-mcp-plugin** | [GitHub](https://github.com/lunarpulse/openclaw-mcp-plugin) | HTTP/SSE transport, multi-server, unified interface |
| **openclaw-mcp-adapter** | [npm](https://www.npmjs.com/package/openclaw-mcp-adapter) | Registers MCP tools as native agent tools |
| **openclaw-mcp** | [GitHub](https://github.com/freema/openclaw-mcp) | Secure Claude.ai ↔ OpenClaw bridge with OAuth 2.1 |
| **openclaw-mcp-server** | [GitHub](https://github.com/Helms-AI/openclaw-mcp-server) | Exposes OpenClaw Gateway tools to Claude Code and MCP clients |

---

## 7. Features & Integrations

### Voice Assistant

| Feature | Description |
|---------|-------------|
| **OpenClaw Voice** | Self-hosted browser-based voice chat (Whisper STT + ElevenLabs TTS) |
| **Android App** | Customizable wake words, long-press home button activation |
| **Voice Call Plugin** | Telephony via Twilio, Telnyx, Plivo |
| **ClawdTalk** | Phone calling and SMS for OpenClaw, with calendar/Jira/web search integration |
| **Always-On Speech** | macOS/iOS/Android with ElevenLabs |

- [OpenClaw Voice](https://openclawvoice.com/)
- [Voice Call Plugin Docs](https://docs.openclaw.ai/plugins/voice-call)
- [ClawdTalk](https://clawdtalk.com/) — Phone calls and SMS for OpenClaw agents ([GitHub](https://github.com/team-telnyx/clawdtalk-client))

### Home Automation

- **Home Assistant** custom add-on with ha-mcp integration
- Control lights, thermostats, IoT devices via messaging
- Adjust boilers based on weather forecasts
- Voice commands through WhatsApp/Telegram

- [OpenClaw on Home Assistant](https://community.home-assistant.io/t/openclaw-clawdbot-on-home-assistant/981467)
- [OpenClaw Gave My Home Assistant an AI Agent](https://www.dan-malone.com/blog/openclaw-home-assistant)

### Email & Calendar

- **Gmail**: Real-time processing via Pub/Sub, smart filtering, auto-responses
- **Google Calendar**: Event creation, viewing, sync, daily briefings
- **Apple Calendar**: Via khal/vdirsyncer integration
- **Outlook**: Calendar sync and management
- **[BotEmail.ai](https://botemail.ai)** — Instant @botemail.ai email inboxes for AI agents ([ClawHub](https://clawhub.ai/skills/bot-email))

- [Gmail Automation Guide](https://zenvanriel.nl/ai-engineer-blog/openclaw-gmail-pubsub-automation-guide/)
- [Google Calendar Sync](https://martin.hjartmyr.se/articles/openclaw-google-calendar-sync/)
- [Google Workspace Integration Guide](https://www.getopenclaw.ai/integrations/google-workspace)

### Webhooks & Cron Jobs

**Webhooks**: POST to `/hooks/wake` or `/hooks/agent` with Bearer token authentication. [Hookdeck](https://hookdeck.com/webhooks/platforms/using-hookdeck-with-openclaw-reliable-webhooks-for-your-ai-agent) for secure tunnels with retries.

**Cron Jobs**: Interval-based (`every 30 minutes`) or Unix cron expressions (`0 9 * * 1`). Stored at `~/.openclaw/cron/jobs.json`. Exponential retry backoff.

**Heartbeat**: Agent wakes every 30 min (configurable), reads `HEARTBEAT.md`, decides if action needed.

- [Webhooks Docs](https://docs.openclaw.ai/automation/webhook)
- [Cron Jobs Docs](https://docs.openclaw.ai/automation/cron-jobs)
- [Heartbeat Docs](https://docs.openclaw.ai/gateway/heartbeat)
- **[ClawTick](https://clawtick.com/)** — Cloud scheduler for OpenClaw agents with performance monitoring and uptime checks.

### Live Canvas

A2UI (Agent-to-UI) visual workspace — agent can render real-time UI, charts, and diagrams. Embedded in macOS menu bar app using WKWebView. Borderless, resizable, auto-reloads on file changes.

- [Canvas Docs](https://docs.openclaw.ai/platforms/mac/canvas)

### Multi-Agent Setup

Configure multiple agents with separate workspaces, personas, auth profiles, and sessions (no cross-talk). Route by channel, phone number, or personality.

- [Multi-Agent Docs](https://docs.openclaw.ai/concepts/multi-agent)
- [Build Your Own AI Agent Team in 15 Minutes](https://ai2sql.io/how-to-build-your-own-ai-agent-team-with-openclaw-in-15-minutes)

### Companion Apps

| App | Platform | Features |
|-----|----------|----------|
| **Menu Bar App** | macOS | Pixel lobster icon, voice wake, Canvas panel, TCC permissions |
| **Crabwalk** | Cross-platform | Open-source companion app ([crabwalk.app](https://crabwalk.app/)) |
| **iOS/Android** | Mobile | Camera, screen recording, notifications |
| **[Expo OpenClaw Chat](https://github.com/brunobar79/expo-openclaw-chat)** | iOS/Android (Expo) | React Native chat SDK for native mobile clients |
| **[OpenClawgotchi](https://github.com/turmyshevd/openclawgotchi)** | Raspberry Pi | AI Tamagotchi with E-Ink face |
| **[VisionClaw](https://github.com/sseanliu/VisionClaw)** | Meta Ray-Ban (iOS) | Voice + vision + agentic actions via Gemini Live (796 stars) |
| **[PinchChat](https://github.com/MarlBurroW/pinchchat)** | Web (PWA) | ChatGPT-like interface, live tool calls, multi-session, 8 languages |
| **[VibeClaw](https://vibeclaw.dev)** | Web | Full OpenClaw in the browser, no install required |

### Monitoring & Dashboards

| Tool | Type | Features |
|------|------|----------|
| **openclaw dashboard** | Built-in | Gateway info, stats, web UI |
| **[ClawController](https://www.clawcontroller.com/)** | Third-party | Real-time monitoring, task orchestration, agent chat |
| **claw-dash** | Community | Sessions, tokens, costs, CPU/RAM/disk metrics |
| **[OpenClaw Studio](https://github.com/grp06/openclaw-studio)** | Community | Visual agent management with cron jobs, tool extraction, mentions (410 stars) |
| **[Hawk Eye](https://github.com/benfoxsb/hawk-eye)** | Community | Workspace sentinel & operational dashboard |
| **[ClawTick](https://clawtick.com/)** | Third-party | Performance monitoring, uptime checks, real-time analytics |

### Backup & Restore

```bash
openclaw config backup
openclaw config restore config-2026-02-01-1600.yaml

# Manual backup
tar -czvf ~/openclaw_backup_$(date +%Y%m%d).tar.gz -C "$HOME" .openclaw
```

> Never commit `~/.openclaw/` to Git (contains secrets).

### OpenClaw vs Claude Code

**Complementary tools**, not competitors. Many engineers run both simultaneously.

| Feature | Claude Code | OpenClaw |
|---------|------------|----------|
| **Lives in** | Terminal / IDE | Messaging apps |
| **Focus** | Coding, development | Automation, integration |
| **Memory** | Session-based | Persistent (24/7) |
| **Operation** | Interactive | Autonomous |
| **Runtime** | Per-session | Always-on daemon |
| **Best for** | Multi-file refactoring, tests | Inbox monitoring, reminders, web scraping |

---

## 8. Security

### Known CVEs (All Patched)

| CVE | Severity | Description | Fixed In |
|-----|----------|-------------|----------|
| **CVE-2026-24763** | High | Docker PATH Command Injection | v2026.1.29 |
| **GHSA-g8p2-7wf7-98mq** | Critical (8.8) | gatewayUrl Token Exfiltration (1-click RCE) | v2026.1.29 |
| **GHSA-q284-4pvr-m585** | High | sshNodeCommand Injection | v2026.1.29 |
| **CVE-2026-25593** | Critical | Unauthenticated Local RCE via WebSocket | v2026.1.30 |
| **CVE-2026-25475** | High | Local File Inclusion via MEDIA: Path | v2026.1.30 |
| **CVE-2026-25253** | Critical (8.8) | 1-Click RCE via Cross-Site WebSocket Hijacking | v2026.1.29 |

> **Update immediately to v2026.2.12+** to patch all known vulnerabilities (40+ security fixes).

### Security Best Practices

1. **Bind to `127.0.0.1` only** (never `0.0.0.0`) — over 135,000 exposed instances found online
2. Use **SSH tunnels** or [Tailscale Serve](https://tailscale.com/kb/1242/tailscale-serve) for remote access
3. Use **auth profiles** (system keychain): `openclaw auth set ANTHROPIC_API_KEY`
4. Configure **firewall**: `ufw default deny incoming && ufw allow ssh && ufw allow 443/tcp && ufw enable`
5. Use **Docker** for container isolation
6. Run regular audits: `openclaw security audit --deep` and `openclaw doctor`
7. Use **Composio** for managed OAuth ([security guide](https://composio.dev/blog/secure-openclaw-moltbot-clawdbot-setup))

### Skills Marketplace Risks

> **~15% of community skills contain malicious instructions**

- **341 malicious skills** discovered in "ClawHavoc" campaign (Atomic Stealer malware)
- **280+ skills leak API keys and PII** ([Snyk](https://snyk.io/blog/openclaw-skills-credential-leaks-research/))
- VirusTotal scanning now integrated
- Always audit skills before installation

### Security Tools

| Tool | Description | Source |
|------|-------------|--------|
| **ClawSec** | Complete security skill suite by Prompt Security | [GitHub](https://github.com/prompt-security/clawsec) |
| **ClawBands** | Security middleware — human-in-the-loop approval for dangerous actions | [GitHub](https://github.com/SeyZ/clawbands) |
| **ClawGuard** | Permission manifests, runtime enforcement, sandboxing, audit logging | [GitHub](https://github.com/newtro/ClawGuard) |
| **Claw-Hunter** | MDM-ready scripts to detect shadow OpenClaw agents across endpoints | [GitHub](https://github.com/backslash-security/Claw-Hunter) |
| **Aquaman** | Credential isolation proxy — API keys never enter the agent process | [GitHub](https://github.com/tech4242/aquaman) |
| **Clawhatch** | Pre-install security scanner — 128 automated checks, scores skills 0–100 | [GitHub](https://github.com/AISafetyLab/clawhatch) |
| **OpenClaw Scanner** | Enterprise endpoint scanner — detects exposed instances and misconfigurations | [Help Net Security](https://www.helpnetsecurity.com/2026/02/13/openclaw-scanner-enterprise/) |

### Security Resources

- [centminmod/explain-openclaw](https://github.com/centminmod/explain-openclaw) - Deep security analysis (73 files, multi-AI)
- [Cisco - AI Agents Are a Security Nightmare](https://blogs.cisco.com/ai/personal-ai-agents-like-openclaw-are-a-security-nightmare)
- [Bitdefender - Malicious Skill Trap](https://www.bitdefender.com/en-us/blog/labs/helpful-skills-or-hidden-payloads-bitdefender-labs-dives-deep-into-the-openclaw-malicious-skill-trap)
- [Snyk - 280+ Leaky Skills](https://snyk.io/blog/openclaw-skills-credential-leaks-research/)
- [The Register - Security Issues](https://www.theregister.com/2026/02/02/openclaw_security_issues/)
- [SecurityWeek - Hijack OpenClaw AI Assistant](https://www.securityweek.com/vulnerability-allows-hackers-to-hijack-openclaw-ai-assistant/)
- [Censys - 135,000+ AI Instances Exposed](https://censys.com/blog/openclaw-in-the-wild-mapping-the-public-exposure-of-a-viral-ai-assistant)
- [VirusTotal - From Automation to Infection](https://blog.virustotal.com/2026/02/from-automation-to-infection-how.html)
- [Semgrep - OpenClaw Security Engineer's Cheat Sheet](https://semgrep.dev/blog/openclaw-security-cheat-sheet)
- [Cyera - The OpenClaw Security Saga](https://www.cyera.com/research-labs/the-openclaw-security-saga-how-ai-adoption-outpaced-security-boundaries)
- [Belgium CCB Advisory](https://ccb.belgium.be/advisories/warning-critical-vulnerability-openclaw-allows-1-click-remote-code-execution-when)

### Diagnostic Commands

```bash
openclaw doctor                    # Common issues
openclaw security audit --deep     # Deep security scan
openclaw security audit --fix      # Auto-fix safe issues
node --version                     # Must be 22+
```

---

## 9. Skills & Ecosystem

### Registries

| Registry | URL | Count |
|----------|-----|-------|
| **ClawHub (Official)** | [clawhub.ai](https://clawhub.ai/) | 5,705+ skills |
| **Awesome OpenClaw Skills** | [VoltAgent/awesome-openclaw-skills](https://github.com/VoltAgent/awesome-openclaw-skills) | 3,009 curated |

### Lobster Workflow Runtime

[Lobster](https://github.com/openclaw/lobster) — typed workflow runtime with resumable approvals. Turns skills/tools into composable pipelines.

### Notable Skills & Plugins

| Skill | Description | Source |
|-------|-------------|--------|
| **Mixpost** | Social media management integration | [ClawHub](https://mixpost.app/blog/openclaw-skill) |
| **Luma Events** | Search events, RSVP, sync to Google Calendar | [X/@bilbeny](https://x.com/bilbeny/status/2017046033759686929) |
| **QMD Skill** | Cuts token usage by 95% | [X](https://x.com/milesdeutscher/status/2018768974872449100) |
| **Supermemory** | Unlimited memory for OpenClaw | [GitHub](https://github.com/supermemoryai/openclaw-supermemory) |
| **Cognee** | Graph-based memory with auto-recall, semantic search | [GitHub](https://github.com/topoteretes/cognee-integrations/tree/main/integrations/openclaw) |
| **ClawRouter** | Smart LLM router — save 78% on inference costs, 30+ models | [GitHub](https://github.com/BlockRunAI/ClawRouter) |
| **Honcho** | Persistent cross-session memory with user modeling | [ClawHub](https://clawhub.ai/ajspig/honcho-setup) |
| **memory-mem0** | Self-hosted memory using Mem0, Ollama embeddings, Qdrant vector storage | [GitHub](https://github.com/serenichron/openclaw-memory-mem0) |
| **Announcer** | House-wide TTS announcements via AirPlay speakers | [GitHub](https://github.com/odrobnik/announcer-skill) |
| **Unbrowse** | Self-learning API skill generator — auto-discovers APIs from browser traffic | [GitHub](https://github.com/lekt9/unbrowse-openclaw) |
| **Foundry** | Self-writing meta-extension — learns how you work, writes new capabilities | [GitHub](https://github.com/lekt9/openclaw-foundry) |
| **AfrexAI Skills** | 13 free business skills: prospect research, cold email, competitor analysis, CRM, SEO, etc. | [Setup Wizard](https://afrexai-cto.github.io/agent-setup/) |

### Third-Party Platforms

| Platform | Integration | Description |
|----------|------------|-------------|
| **[LangBot](https://github.com/langbot-app/LangBot)** | Multi-platform | Agentic IM bots with OpenClaw, Dify, n8n, Langflow, Coze |
| **[OpenRouter](https://openrouter.ai/docs/guides/guides/openclaw-integration)** | LLM routing | Access 30+ models with smart routing |
| **[You.com](https://you.com/resources/openclaw-integration)** | Search/AI | OpenClaw skill for You.com search and AI integration |
| **[unRAID Community App](https://www.reddit.com/r/unRAID/comments/1qv4tky/openclaw_ai_assistant_gateway_now_available_on/)** | NAS/Server | Official Community Apps template for unRAID |
| **[Airstore](https://github.com/beam-cloud/airstore)** | Agent Storage | The filesystem for AI agents — persistent storage layer |

### Install a Skill

```bash
openclaw skill install <skill-name>
```

> Always audit skills before installation. ~15% contain malicious instructions. Use VirusTotal-scanned ClawHub skills only.

---

## 10. Browser Automation

| Mode | Description | Use Case |
|------|-------------|----------|
| **Extension Relay** | Control existing Chrome tabs with logged-in sessions | Personal browsing |
| **OpenClaw-managed** | Isolated automation in dedicated browser | Web scraping, testing |
| **Remote CDP** | Distributed cloud deployments | Scale at cloud level |

Capabilities: CDP, ARIA snapshots, screenshots, tab management, click/type/drag, PDF export, video recording.

- [Browser Docs](https://docs.openclaw.ai/tools/browser)
- [Browser Automation Guide](https://help.apiyi.com/en/openclaw-browser-automation-guide-en.html)

---

## 11. Real-World Use Cases

### Productivity
- **Morning brief**: Weather, calendar, headlines before checking your phone
- **Inbox management**: Process thousands of emails autonomously, unsubscribe from spam
- **Grocery list**: Auto-add items from household texts to shared documents

### Development
- Review PRs from your phone, run tests remotely, merge code
- Multi-instance Claude Code supervised by OpenClaw via Telegram + Tailscale
- Run coding agents while sleeping

### Smart Home
- Control Philips Hue, Elgato, Home Assistant via messaging
- Adjust heating based on weather forecasts
- Security camera monitoring with alerts

### Financial
- Calculate position sizes, manage stop-loss rules
- Trade alert logging and automation
- Integrate with on-chain token deployment on Base (e.g., [PumpClaw](https://pumpclaw.com))

### Creative
- Voice notes to clean journal entries
- Platform-specific content: X threads, LinkedIn posts, blog articles
- Weekly meal planning in Notion (saves 1 hour/week)

### Family
- Monitor school WhatsApp groups, filter noise
- Run face recognition on photos, send daily digest to parents

- [25 OpenClaw Use Cases - Hostinger](https://www.hostinger.com/tutorials/openclaw-use-cases)
- [20 Genius Use Cases](https://ucstrategies.com/news/20-genius-openclaw-use-cases-people-are-using-right-now/)
- [33 Automations in 30 Minutes](https://medium.com/@rentierdigital/33-openclaw-automations-you-can-set-up-in-30-minutes-that-start-making-you-money-tonight-f8c3b8a402f1)

### Common Issues & Troubleshooting

| Issue | Cause | Fix |
|-------|-------|-----|
| Crash during onboarding | < 2 GB RAM | Upgrade to 4 GB+ RAM |
| API key not working | Incorrect format or expired | Re-enter via `openclaw auth set` |
| Telegram not connecting | Using Cloudflare Workers | Switch to VPS (needs persistent connection) |
| Slow inference (3.5s/token) | CPU-only with large model | Use smaller model or add GPU |
| Port conflict on 18789 | Another service using port | `openclaw gateway --port 18790` |
| Docker sandbox issues | Permissions or config | Run `openclaw doctor` |
| High token consumption | ~35,600 tokens per message overhead | Reduce workspace files |
| Rate limiting | Aggressive retry loops | Update (exponential backoff fix) |

---

## 12. Learning Resources

### Getting Started Guides

- [Official Getting Started](https://docs.openclaw.ai/start/getting-started)
- [Codecademy Tutorial (20 min)](https://www.codecademy.com/article/open-claw-tutorial-installation-to-first-chat-setup)
- [freeCodeCamp Full Tutorial](https://www.freecodecamp.org/news/openclaw-full-tutorial-for-beginners/)
- [Master OpenClaw in 30 Minutes](https://creatoreconomy.so/p/master-openclaw-in-30-minutes-full-tutorial)
- [Beginner's Guide (5 min)](https://help.apiyi.com/en/openclaw-beginner-guide-en.html)
- [40 Tips & Tricks](https://mlearning.substack.com/p/40-tips-and-tricks-from-first-install-to-production-nanoclaw-nano-claw-openclaw-open-2026-2-1-self-learning-skill-that-actually-work-vps-docker-security-ai-agent-swarm-readme-md-memory-architecture-cron-hearbeat-sessions-slack-telegram-whatsapp)
- [BitLaunch - Install on macOS, Linux, Windows](https://bitlaunch.io/blog/install-configure-openclaw/)

### Cloud Provider Guides

- [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-run-openclaw) | [AWS](https://dev.to/brayanarrieta/how-to-set-up-openclaw-ai-on-aws-3a0j) | [AWS Bedrock (Official Sample)](https://github.com/aws-samples/sample-OpenClaw-on-AWS-with-Bedrock)
- [GCP](https://rizwantheanalyst.com/2026/02/04/openclaw-on-google/) | [Azure](https://techcommunity.microsoft.com/blog/azuredevcommunityblog/complete-guide-to-deploying-openclaw-on-azure-windows-11-virtual-machine/4492001)
- [Hostinger](https://www.hostinger.com/tutorials/how-to-set-up-openclaw) | [Alibaba Cloud](https://www.alibabacloud.com/en/campaign/ai-openclaw)

### Integration Guides

- [Slack Integration](https://lumadock.com/tutorials/openclaw-slack-integration) | [Notion Integration](https://www.openclawexperts.io/guides/integrations/how-to-connect-openclaw-to-notion)
- [GitHub PR Automation](https://zenvanriel.nl/ai-engineer-blog/openclaw-github-pr-review-automation-guide/)
- [Tailscale VPN Setup](https://dev.to/nunc/self-hosting-openclaw-ai-assistant-on-a-vps-with-tailscale-vpn-zero-public-ports-35fn)
- [OpenRouter Integration](https://openrouter.ai/docs/guides/guides/openclaw-integration) | [DeepSeek via OpenRouter](https://medium.com/@oo.kaymolly/connect-deepseek-to-openclaw-via-openrouter-7eb19ef61a84)
- [Kimi K2.5 + OpenClaw Guide](https://medium.com/coding-nexus/how-to-connect-kimi-k2-5-to-openclaw-clawdbot-bf7ed5a31743) | [Moonshot Official Docs](https://platform.moonshot.ai/docs/guide/use-kimi-in-openclaw)
- [Cron Jobs Automation Guide](https://zenvanriel.nl/ai-engineer-blog/openclaw-cron-jobs-proactive-ai-guide/)

### Security Guides

- [Secure on Cloudflare](https://medium.com/@williamogou/deploy-openclaw-securely-on-cloudflare) | [7 Security Best Practices](https://xcloud.host/openclaw-security-best-practices)
- [Security & Cost Control](https://www.moltbook-ai.com/blog/openclaw-guide-2026) | [Composio Controls](https://composio.dev/blog/secure-openclaw-moltbot-clawdbot-setup)

### Video Tutorials

| Title | Platform | Topics |
|-------|----------|--------|
| **Master OpenClaw in 30 Minutes** | Creator Economy (YouTube) | Safe setup, 5 real use cases, memory |
| **How OpenClaw's Creator Uses AI** | Creator Economy | Full demo with Peter Steinberger |
| **OpenClaw Full Tutorial for Beginners** | [freeCodeCamp (YouTube)](https://www.youtube.com/watch?v=n1sfrc-RjyM) | Installation, models, memory, Docker, skills |
| **The Wild Rise of OpenClaw** | [Fireship (YouTube)](https://www.youtube.com/watch?v=ssYt09bCgUY) | History, architecture, why it matters |
| **How to Setup OpenClaw in 5 Minutes** | [Julian Goldie (YouTube)](https://www.youtube.com/watch?v=1luvvYcpSJ8) | Quick start, beginner-friendly |
| **This Open-Source AI Agent Is INSANE** | [YouTube](https://m.youtube.com/watch?v=KqTs7QvknDo) | Review, Live Canvas, A2UI demo |
| **ClawCon SF: Live Interviews** | [YouTube](https://www.youtube.com/watch?v=jMnLqGU-Ds4) | Builder interviews, demos from ClawCon |
| **ClawCon 2026 Raw Footage** | [YouTube](https://www.youtube.com/watch?v=gT98KNkoLGM) | Community event, builder demos |

### Courses & Learning Platforms

| Platform | URL | Cost | Description |
|----------|-----|------|-------------|
| **OpenClaw Academy** | [openclaw.academy](https://openclaw.academy/) | **Free** | All courses free, no signup, interactive quizzes |
| **freeCodeCamp** | [YouTube](https://www.freecodecamp.org/news/openclaw-full-tutorial-for-beginners/) | **Free** | Comprehensive 1-hour course |
| **Codecademy** | [Tutorial](https://www.codecademy.com/article/open-claw-tutorial-installation-to-first-chat-setup) | **Free** | 20-minute install guide |
| **GitHub Course** | [kiankyars/openclawcourse](https://github.com/kiankyars/openclawcourse) | **Free** | 1-hour crash course |
| **Udemy** | [Azure VM Course](https://www.udemy.com/course/openclaw/) | Paid | Azure Linux VM deployment |
| **Gripsy Learn** | [OpenClaw Mastery](https://gripsy.com.au/learn/openclaw/) | Free/Paid | 11-module course: setup, skills, security, automation |

### Events & Hackathons

| Event | Date | Location | Details |
|-------|------|----------|---------|
| **[ClawCon: 1st OpenClaw SF Show & Tell](https://trymimetic.com/events/sf/clawcon-1st-openclaw-sf-show-tell-open-registration-feb-2026)** | Feb 5, 2026 | San Francisco | Builder demos, live interviews |
| **[OpenClaw Unhackathon](https://sf.aitinkerers.org/p/openclaw-unhackathon)** | Feb 7, 2026 | San Francisco (AI Tinkerers) | Build & compete |
| **[OpenClaw Micro Hackathon](https://www.eventbrite.co.uk/e/openclaw-micro-hackathon-tickets-1982409167184)** | Feb 7, 2026 | Hong Kong (Dim Sum Labs) | Community hackathon |
| **[OpenClaw/Moltbook Hackathon at MIT](https://x.com/SantanuB01/status/2018608892591395079)** | Feb 3, 2026 | MIT, Cambridge | Serious coders, agent building |
| **[Circle/USDC Hackathon on Moltbook](https://www.circle.com/blog/openclaw-usdc-hackathon-on-moltbook)** | 2026 | Online (Moltbook) | USDC, onchain payments |

---

## 13. Community & Media

### Community Platforms

| Platform | URL | Members | Best For |
|----------|-----|---------|----------|
| **Discord** | [OpenClaw Discord](https://docs.openclaw.ai/channels/discord) | 8,000+ | Quick questions, troubleshooting |
| **Discourse (CoClaw)** | [coclaw.com](https://coclaw.com/) | 15,000+ | Long-form discussion, bug reports |
| **X/Twitter Community** | [OpenClaw Community](https://x.com/i/communities/2013441068562325602) | 12,200+ | News, updates, demos |
| **GitHub Issues** | [openclaw/openclaw/issues](https://github.com/openclaw/openclaw/issues) | N/A | Bug reports, feature requests |
| **GitHub Discussions** | [openclaw/openclaw/discussions](https://github.com/openclaw/openclaw/discussions) | N/A | Q&A, show-and-tell |
| **Hacker News** | [Search](https://hn.algolia.com/?q=openclaw) | N/A | Technical discussion |

### Mainstream Media Coverage

- [CNBC - From Clawdbot to Moltbot to OpenClaw](https://www.cnbc.com/2026/02/02/openclaw-open-source-ai-agent-rise-controversy-clawdbot-moltbot-moltbook.html)
- [TechCrunch - AI assistants building their own social network](https://techcrunch.com/2026/01/30/openclaws-ai-assistants-are-now-building-their-own-social-network/)
- [Fortune - 'Most interesting place on the internet'](https://fortune.com/2026/01/31/ai-agent-moltbot-clawdbot-openclaw-data-privacy-security-nightmare-moltbook-social-network/)
- [VentureBeat - What the OpenClaw moment means for enterprises](https://venturebeat.com/technology/what-the-openclaw-moment-means-for-enterprises-5-big-takeaways)
- [Forbes - OpenClaw, Moltbook & The Birth of a Machine Society](https://www.forbes.com/sites/jonmarkman/2026/02/06/openclaw-moltbook--the-birth-of-a-machine-society/)
- [Bloomberg - AI Sensation, Security a Work in Progress](https://www.bloomberg.com/news/articles/2026-02-04/openclaw-s-an-ai-sensation-but-its-security-a-work-in-progress)
- [BBC Science Focus](https://www.sciencefocus.com/future-technology/openclaw-first-agentic-ai) | [PCMag](https://www.pcmag.com/news/openclaw-is-the-hot-new-ai-agent-but-is-it-safe-to-use) | [CNET](https://www.cnet.com/tech/services-and-software/from-clawdbot-to-moltbot-to-openclaw/)
- [Nature - OpenClaw AI chatbots are running amok](https://www.nature.com/articles/d41586-026-00439-0)
- [Wikipedia - OpenClaw](https://en.wikipedia.org/wiki/OpenClaw) | [Wikipedia - Moltbook](https://en.wikipedia.org/wiki/Moltbook)

### Security Coverage

- [Cisco - Security Nightmare](https://blogs.cisco.com/ai/personal-ai-agents-like-openclaw-are-a-security-nightmare)
- [Hacker News - One-Click RCE](https://thehackernews.com/2026/02/openclaw-bug-enables-one-click-remote.html)
- [CrowdStrike - What Security Teams Need to Know](https://www.crowdstrike.com/en-us/resources/crowdcasts/what-security-teams-need-to-know-about-openclaw/)
- [Censys - 135,000+ AI Instances Exposed](https://censys.com/blog/openclaw-in-the-wild-mapping-the-public-exposure-of-a-viral-ai-assistant)

### Moltbook (AI Social Network)

Created by OpenClaw agent "Clawd Clawderberg" (built by Matt Schlicht, Cofounder of Octane AI).

| Stat | Value |
|------|-------|
| **Launched** | January 28, 2026 |
| **Registered AI agents** | 1.6M+ |
| **Posts & responses** | 7.5M+ AI-generated |
| **Format** | Reddit-style forum for AI agents |
| **Human access** | Read-only observation |

> *"Most interesting place on the internet right now"* — Fortune

- [TechCrunch](https://techcrunch.com/2026/01/30/openclaws-ai-assistants-are-now-building-their-own-social-network/)
- [Proof of Lobster](https://proofoflobster.ai) — Verify if Moltbook profiles are AI-generated ([GitHub](https://github.com/Theseuschain/proof-of-lobster))

---

## 14. Alternatives & Competitors

| Alternative | Type | Best For | Key Advantage |
|-------------|------|----------|---------------|
| **[Nanobot](https://github.com/HKUDS/nanobot)** | Lightweight (4K lines) | Minimalists | 99% smaller codebase, 45 MB RAM, MCP-native |
| **[PicoClaw](https://github.com/sipeed/picoclaw)** | Ultra-lightweight (Go) | Embedded/hardware | 10 MB RAM, $10 RISC-V, single binary, 1s boot |
| **[Archestra](https://github.com/archestra-ai/archestra)** | Enterprise | Security/compliance | MCP registry, A2A, agentic security (3.5K stars) |
| **[NanoClaw](https://github.com/qwibitai/nanoclaw)** | Security-first | Apple container | 500 lines TypeScript, WhatsApp, Anthropic Agent SDK (7K+ stars) |
| **[IronClaw](https://github.com/nearai/ironclaw)** | Rust rewrite | Privacy & security | OpenClaw-inspired, built by NEAR AI (1.3K stars) |
| **[ZeroClaw](https://github.com/theonlyhennygod/zeroclaw)** | Rust ultra-fast | Speed-first users | 3.4 MB binary, <10ms startup, 22+ providers |
| **[TinyClaw](https://github.com/jlia0/tinyclaw)** | Shell script (400 LoC) | Stability-first | Claude Code + tmux, WhatsApp, self-healing (1.3K stars) |
| **[MimiClaw](https://github.com/memovai/mimiclaw)** | ESP32, Pure C | Cheapest hardware | $5 chip, no OS, no Node.js required |
| **[Mini-Claw](https://github.com/htlin222/mini-claw)** | Minimalist | Subscription users | Uses Claude Pro/Max directly in Telegram, zero API cost |
| **[Autobot](https://github.com/crystal-autobot/autobot)** | Crystal | Speed and security | 2MB binary, ~5MB RAM, <10ms startup |
| **[GitClaw](https://github.com/SawyerHood/gitclaw)** | GitHub Actions | Serverless | Zero-infra via GitHub Issues & Actions |
| **[ClosedClaw](https://github.com/asafelobotomy/ClosedClaw)** | Desktop GUI fork | GTK users | GTK GUI + Ollama integration |
| **[VisionClaw](https://github.com/sseanliu/VisionClaw)** | Smart glasses | Wearable AR | Meta Ray-Ban + Gemini Live + OpenClaw (796 stars) |
| **[BankrBot Skills](https://github.com/BankrBot/openclaw-skills)** | DeFi/crypto agent | Web3 traders | Polymarket, token trading, NFTs, on-chain messaging |
| **[Ralv](https://ralv.ai/)** | 3D agent orchestration | Multi-agent management | StarCraft-like spatial UI for 100+ agents |
| **Jan.ai** | Offline chat | Privacy absolutists | 100% offline |
| **Dify** | LLM app platform | Agents, RAG, MLOps | Best debugging, workflow visualization |
| **n8n** | Workflow automation | Business processes | Visual workflow builder |
| **Claude Code** | Coding agent | Developers | Best coding assistant |
| **Knolli.ai** | Safe agentic AI | Security-first | [Best OpenClaw alternative](https://www.knolli.ai/post/clawdbot-alterantive) |

---

## 15. Related Repositories

| Repository | Description |
|------------|-------------|
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | Main repository (195K+ stars) |
| [openclaw/clawhub](https://github.com/openclaw/clawhub) | Official skill directory |
| [openclaw/lobster](https://github.com/openclaw/lobster) | Typed workflow runtime |
| [openclaw/barnacle](https://github.com/openclaw/barnacle) | Official OpenClaw companion bot |
| [openclaw/trust](https://github.com/openclaw/trust) | Official open threat model |
| [cloudflare/moltworker](https://github.com/cloudflare/moltworker) | Cloudflare Workers adaptation |
| [VoltAgent/awesome-openclaw-skills](https://github.com/VoltAgent/awesome-openclaw-skills) | 3,009 curated skills |
| [aws-samples/sample-OpenClaw-on-AWS-with-Bedrock](https://github.com/aws-samples/sample-OpenClaw-on-AWS-with-Bedrock) | AWS-native deployment using Amazon Bedrock |
| [centminmod/explain-openclaw](https://github.com/centminmod/explain-openclaw) | Deep security analysis (73 files) |
| [lunarpulse/openclaw-mcp-plugin](https://github.com/lunarpulse/openclaw-mcp-plugin) | MCP server integration |
| [essamamdani/openclaw-coolify](https://github.com/essamamdani/openclaw-coolify) | Coolify PaaS template |
| [prompt-security/clawsec](https://github.com/prompt-security/clawsec) | Complete security skill suite |
| [SeyZ/clawbands](https://github.com/SeyZ/clawbands) | Security middleware (human-in-the-loop) |
| [newtro/ClawGuard](https://github.com/newtro/ClawGuard) | Permission manifests and sandboxing |
| [backslash-security/Claw-Hunter](https://github.com/backslash-security/Claw-Hunter) | MDM-ready shadow agent detection |
| [tech4242/aquaman](https://github.com/tech4242/aquaman) | Credential isolation proxy |
| [AISafetyLab/clawhatch](https://github.com/AISafetyLab/clawhatch) | Pre-install skill security scanner |
| [BlockRunAI/ClawRouter](https://github.com/BlockRunAI/ClawRouter) | Smart LLM router (save 78% on costs) |
| [langbot-app/LangBot](https://github.com/langbot-app/LangBot) | Multi-platform IM bot with OpenClaw |
| [kiankyars/openclawcourse](https://github.com/kiankyars/openclawcourse) | 1-hour crash course |
| [memovai/mimiclaw](https://github.com/memovai/mimiclaw) | OpenClaw core in pure C on ESP32-S3 |
| [sipeed/picoclaw](https://github.com/sipeed/picoclaw) | Ultra-lightweight AI agent in Go (5K stars) |
| [HKUDS/nanobot](https://github.com/HKUDS/nanobot) | Ultra-lightweight OpenClaw alternative (15K+ stars) |
| [nearai/ironclaw](https://github.com/nearai/ironclaw) | OpenClaw-inspired Rust implementation by NEAR AI |
| [theonlyhennygod/zeroclaw](https://github.com/theonlyhennygod/zeroclaw) | Pure Rust, 3.4 MB binary, <10ms startup |
| [jlia0/tinyclaw](https://github.com/jlia0/tinyclaw) | OpenClaw in ~400 lines of shell script (1.3K stars) |
| [crystal-autobot/autobot](https://github.com/crystal-autobot/autobot) | Crystal, 2 MB binary, ~5 MB RAM, <10ms startup |
| [qwibitai/nanoclaw](https://github.com/qwibitai/nanoclaw) | Original NanoClaw — Apple containers, 500 lines TypeScript (7K+ stars) |
| [SawyerHood/gitclaw](https://github.com/SawyerHood/gitclaw) | OpenClaw on GitHub Actions — issues become AI chat threads |
| [BankrBot/openclaw-skills](https://github.com/BankrBot/openclaw-skills) | DeFi/crypto skill library |
| [clawd800/pumpclaw](https://github.com/clawd800/pumpclaw) | Token launcher for AI agents on Base (Uniswap V4) |
| [brunobar79/expo-openclaw-chat](https://github.com/brunobar79/expo-openclaw-chat) | Expo / React Native chat SDK |
| [archestra-ai/archestra](https://github.com/archestra-ai/archestra) | OpenClaw for Enterprise — agentic security, MCP registry (3.5K stars) |
| [grp06/openclaw-studio](https://github.com/grp06/openclaw-studio) | Visual agent management UI (410 stars) |
| [abhi1693/openclaw-mission-control](https://github.com/abhi1693/openclaw-mission-control) | Mission control with RBAC, Kanban, War Room |
| [turmyshevd/openclawgotchi](https://github.com/turmyshevd/openclawgotchi) | AI Tamagotchi on Raspberry Pi with E-Ink face |
| [sseanliu/VisionClaw](https://github.com/sseanliu/VisionClaw) | Meta Ray-Ban + Gemini Live + OpenClaw (796 stars) |
| [MarlBurroW/pinchchat](https://github.com/MarlBurroW/pinchchat) | Open-source webchat UI — ChatGPT-like, multi-session, 8 languages |
| [lekt9/unbrowse-openclaw](https://github.com/lekt9/unbrowse-openclaw) | Self-learning API skill generator |
| [lekt9/openclaw-foundry](https://github.com/lekt9/openclaw-foundry) | Self-writing meta-extension (97 stars) |
| [supermemoryai/openclaw-supermemory](https://github.com/supermemoryai/openclaw-supermemory) | Official Supermemory integration |
| [freema/openclaw-mcp](https://github.com/freema/openclaw-mcp) | MCP server bridging Claude.ai to OpenClaw |
| [beam-cloud/airstore](https://github.com/beam-cloud/airstore) | The filesystem for AI agents (89 stars) |
| [BotMesh/debot](https://github.com/BotMesh/debot) | Rust+Python lightweight alternative |
| [deeqyaqub1-cmd/zero-rules-openclaw](https://github.com/deeqyaqub1-cmd/zero-rules-openclaw) | Deterministic engine for OpenClaw, saves 50–70% on tokens |
| [RyanLisse/engram](https://github.com/RyanLisse/engram) | Unified multi-agent memory for OpenClaw |
| [Ramsbaby/openclaw-self-healing](https://github.com/Ramsbaby/openclaw-self-healing) | 4-tier autonomous self-healing system |
| [coollabsio/openclaw](https://github.com/coollabsio/openclaw) | Auto-built Docker images by CoolLabs |
| [hesamsheikh/awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases) | Real-life OpenClaw use cases |
| [htlin222/mini-claw](https://github.com/htlin222/mini-claw) | Minimalist OpenClaw using Claude Pro/Max directly |
| [asafelobotomy/ClosedClaw](https://github.com/asafelobotomy/ClosedClaw) | OpenClaw fork with GTK GUI and Ollama integration |
| [clawdeckio/clawdeck](https://github.com/clawdeckio/clawdeck) | Open-source mission control dashboard |
| [Theseuschain/proof-of-lobster](https://github.com/Theseuschain/proof-of-lobster) | Verify Moltbook profiles as AI/human |
| [eltociear/awesome-molt-ecosystem](https://github.com/eltociear/awesome-molt-ecosystem) | Curated list of Molt ecosystem services |
| [kelkalot/moltbook-observatory](https://github.com/kelkalot/moltbook-observatory) | Data collection from Moltbook |

### Kubernetes & Helm Charts

| Chart | Source | Features |
|-------|--------|----------|
| **serhanekicii/openclaw-helm** | [GitHub](https://github.com/serhanekicii/openclaw-helm) | Built on bjw-s app-template |
| **waTeim/openclaw-helm** | [GitHub](https://github.com/waTeim/openclaw-helm) | Multi-channel support |
| **khal3d/openclaw** | [GitHub](https://github.com/khal3d/openclaw) | Docker & HELM deployment |

- [Running OpenClaw on Kubernetes - Metoro Blog](https://metoro.io/blog/openclaw-kubernetes)

---

## 16. Performance Benchmarks

### Inference Speed (Local Models)

| Hardware | Tokens/sec | Notes |
|----------|-----------|-------|
| **RTX 4090** | ~80 t/s | Best GPU performance |
| **AMD MI300X** | High | 192 GB memory, free credits available |
| **Apple M2 Pro 64GB** | Good | Large memory pool for bigger models |
| **MacBook Air M2** | ~3.2 t/s | CPU-only, usable |
| **Typical CPU** | ~13.5 t/s | Non-time-critical tasks |
| **Oracle ARM (7B)** | 5–10 t/s | Free tier, acceptable |
| **Raspberry Pi 5** | 2–5 t/s | Slow but works |
| **ESP32-S3 (MimiClaw)** | Cloud API | No local inference, calls Claude API via Wi-Fi |
| **RISC-V (PicoClaw)** | Cloud API | 10 MB RAM, single Go binary, 1s boot, $10 board |

### Memory Requirements for Local Models

| Model Size | RAM Required | GPU VRAM |
|------------|-------------|----------|
| 3B (quantized) | 4 GB | 4 GB |
| 7B (quantized) | 8 GB | 8 GB |
| 13B (quantized) | 16 GB | 12–16 GB |
| 70B (quantized) | 64 GB | 48 GB+ |

**Bottleneck**: Memory bandwidth and VRAM capacity, not CPU speed. Sweet spot: 7B models.

---

## 17. Enterprise Considerations

> *"It is not enterprise software. There is no promise of quality, no vendor support, no SLA… it ships without authentication enforced by default."* — **Gartner**

### Risk Assessments

- **Palo Alto Networks**: OpenClaw presents a "lethal trifecta": access to private data + exposure to untrusted content + ability to communicate externally while retaining memory
- [Vectra - When Automation Becomes a Digital Backdoor](https://www.vectra.ai/blog/clawdbot-to-moltbot-to-openclaw-when-automation-becomes-a-digital-backdoor)
- [Cyera - How AI Adoption Outpaced Security Boundaries](https://www.cyera.com/research-labs/the-openclaw-security-saga-how-ai-adoption-outpaced-security-boundaries)
- [VentureBeat - OpenClaw proves agentic AI works, security model doesn't](https://venturebeat.com/security/openclaw-agentic-ai-security-risk-ciso-guide)

### Enterprise Alternatives

For organizations needing compliance, SLAs, and vendor support, consider:
- **Kilo Claw** — SSO, audit logs, pay-as-you-go
- **ClawCloud Business** — $129/mo, dedicated resources
- **OpenClaw Hosting Business** — Team/Business tiers
- Self-hosted with **NanoClaw** (security-first fork) in isolated containers

---

## 18. China & Global Adoption

OpenClaw has seen explosive adoption in China with support from major tech companies.

| Company | Integration | Details |
|---------|------------|---------|
| **Alibaba Cloud** | [Simple Application Server](https://www.alibabacloud.com/en/campaign/ai-openclaw) | 19 regions, from $4/mo |
| **Tencent Cloud** | Lighthouse Service | One-click install |
| **ByteDance** | Volcano Engine | Cloud hosting support |

### v2026.2.2 — China Support

- Native **Feishu** (飞书) and **Lark** support — first official Chinese chat client integration
- [EvolutionAI Hub - OpenClaw v2026.2.2](https://evolutionaihub.com/openclaw-2026-2-2-ai-agent-framework-onchain/)

### Coverage

- [Rest of World - Moltbot Finds Fans in China and Silicon Valley](https://restofworld.org/2026/moltbot-china-ai-agent/)
- [China's Tech Giants Opening Doors to OpenClaw](https://dnyuz.com/2026/02/05/chinas-tech-giants-are-opening-their-doors-to-openclaw-the-chinese-internet-is-lapping-it-up/)

---

## 19. Release History

| Version | Date | Key Changes |
|---------|------|-------------|
| **v2026.2.12** | Feb 12, 2026 | 40+ security vulnerabilities patched, SSRF protection, prompt injection prevention, directory traversal fixes, enhanced sandbox isolation |
| **v2026.2.9** | Feb 9, 2026 | iOS alpha node app, device pairing/phone control plugins, Grok (xAI) web search, agent management RPC |
| **v2026.2.6** | Feb 7, 2026 | Anthropic Opus 4.6 support, Voyage AI native memory support, built-in safety scanner for skills |
| **v2026.2.3** | Feb 5, 2026 | Performance improvements, bug fixes |
| **v2026.2.2** | Feb 2026 | Feishu/Lark support, onchain integrations |
| **v2026.2.1** | Feb 2026 | Security hardening, streaming stability, path traversal fixes |
| **v2026.1.30** | Jan 30, 2026 | CVE-2026-25593 & CVE-2026-25475 patches |
| **v2026.1.29** | Jan 29, 2026 | CVE-2026-24763, CVE-2026-25253 patches, VirusTotal scanning |
| **v2026.1.24-1** | Jan 24, 2026 | DigitalOcean 1-Click base version |

---

## 20. Key Contributors

| Contributor | Role | GitHub |
|-------------|------|--------|
| **Peter Steinberger** | Creator | [@steipete](https://github.com/steipete) |
| **Mario Zechner** | Pi creator, security pen-tester | [@badlogicc](https://github.com/badlogicc) |
| **Maxim Vovshin** | Blogwatcher skill | [@Hyaxia](https://github.com/Hyaxia) |
| **Nacho Iacovino** | Location parsing | [@nachoiacovino](https://github.com/nachoiacovino) |
| **600+ contributors** | Community | [All contributors](https://github.com/openclaw/openclaw/graphs/contributors) |

---

## 21. Contributing

### How to Add a Resource

1. Fork this repository
2. Edit `README.md` and add your resource to the appropriate section
3. Follow the existing format:
   - **For links/tools:** `- [Resource Name](https://link.com) — Short description (1-2 sentences)`
   - **For table rows:** `| **Provider** | Link | Price | Details |`
4. Submit a pull request

### How to Add a Project to the Ecosystem Directory

The Ecosystem Directory showcases projects built with OpenClaw. Edit `directory.html` and add a card in the appropriate category section using the template (see CONTRIBUTING.md).

**Categories:** `social`, `devtools`, `automation`, `infra`, `hardware`, `defi`, `voice`, `memory`

**Tiers:** `s` (must-see), `a` (excellent), `b` (solid), `c` (notable)

### Guidelines

- Ensure the resource is relevant to OpenClaw
- Check that the link is working
- Keep descriptions concise (1-2 sentences)
- Add new resources at the bottom of the relevant section
- One resource per pull request is preferred
- Report broken links, outdated information, or incorrect pricing via [issues](https://github.com/rohitg00/awesome-openclaw/issues)

---

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

This list is released under CC0 1.0 Universal (Public Domain).
