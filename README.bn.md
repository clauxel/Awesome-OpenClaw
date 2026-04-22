# Awesome OpenClaw - ডেভেলপার-কেন্দ্রিক গাইড

**ভাষাসমূহ:** [English](README.md) | [简体中文](README.zh-CN.md) | [हिन्दी](README.hi.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Français](README.fr.md) | **বাংলা** | [Português](README.pt.md) | [Русский](README.ru.md) | [Bahasa Indonesia](README.id.md)

[![Stars](https://img.shields.io/github/stars/openclaw/openclaw?style=flat&logo=github&label=Stars&color=gold)](https://github.com/openclaw/openclaw/stargazers)
[![Forks](https://img.shields.io/github/forks/openclaw/openclaw?style=flat&label=Forks&color=silver)](https://github.com/openclaw/openclaw/network/members)
[![Contributors](https://img.shields.io/github/contributors/openclaw/openclaw?label=Contributors&color=green)](https://github.com/openclaw/openclaw/graphs/contributors)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0 1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

এটি OpenClaw-এর জন্য ডেভেলপার-প্রথম কিউরেটেড গাইড। এই README প্রচারণা, মূল্যতালিকা আর দ্রুত পুরোনো হয়ে যাওয়া মার্কেটিং দাবি বাদ দিয়ে অফিসিয়াল ডকুমেন্টেশন, ব্যবহারিক সেটআপের ক্রম, নিরাপত্তার বেসলাইন এবং দীর্ঘমেয়াদি কাজে লাগে এমন ইকোসিস্টেম লিংককে অগ্রাধিকার দেয়।

---

## সূচিপত্র

1. [প্রোডাক্ট ওভারভিউ](#product-overview)
2. [দ্রুত শুরু ও সেটআপ পদ্ধতি](#quick-start-setup-methods)
3. [ইনস্টলেশন পথ](#install-paths)
4. [মূল ধারণা ও কমান্ড](#core-concepts-commands)
5. [চ্যানেল: আগে কোনটি যুক্ত করবেন](#channels-what-to-connect-first)
6. [ডিপ্লয়মেন্ট পছন্দ](#deployment-choices)
7. [নিরাপত্তার বেসলাইন](#security-baseline)
8. [উদ্দেশ্যভিত্তিক অফিসিয়াল ডকস](#official-docs-by-goal)
9. [নির্বাচিত ইকোসিস্টেম লিংক](#curated-ecosystem-links)
10. [সাধারণ ভুল](#common-mistakes)
11. [অবদান](#contributing)

---

<a id="product-overview"></a>
## 1. প্রোডাক্ট ওভারভিউ

**OpenClaw** হলো একটি ব্যক্তিগত AI সহকারী, যা আপনি নিজের ডিভাইসে চালান। এর কেন্দ্রে আছে **Gateway**, যা agents, channels, sessions, tools, dashboard/web UI এবং remote access-এর control plane হিসেবে কাজ করে। সহজভাবে বললে, OpenClaw শুধু "একটা bot" নয়; এটি local-first assistant runtime, যা আপনার ব্যবহৃত চ্যাট সারফেসগুলোর ভেতরেই থাকতে পারে।

### OpenClaw ডেভেলপারদের কী দেয়

- CLI, dashboard, WebChat এবং remote access অপশনসহ একটি local Gateway
- WhatsApp, Telegram, Slack, Discord, WebChat এবং আরও অনেক জায়গায় multi-channel messaging
- আলাদা workspace, session, binding এবং model policy-সহ একাধিক agent
- hosted provider, OAuth auth, API key এবং local model path-সহ flexible model setup
- skills, browser automation, nodes, cron jobs এবং অন্যান্য tool-driven workflow
- personal assistant trust model; hostile multi-tenant SaaS security model নয়

### মূল আর্কিটেকচার (৬ স্তর)

| স্তর | কাজ |
|------|-----|
| **Gateway** | কেন্দ্রীয় control plane - message routing, session, plugin এবং tool execution policy |
| **Channels** | Telegram, WhatsApp, Discord, iMessage ইত্যাদিকে standard message shape-এ রূপান্তরকারী adapter |
| **Routing + Sessions** | কোন conversation কোন agent সামলাবে তা ঠিক করে |
| **Agent Runtime** | context প্রক্রিয়াকরণ, model provider call, response stream এবং tool request সামলায় |
| **Tools** | web fetch, browser control, command execution, device pairing-এর মতো capability |
| **Surfaces** | chat app, web dashboard, macOS menu bar এবং Live Canvas-এর মতো interaction point |

### নামের ইতিহাস

| তারিখ | নাম | কারণ |
|-------|-----|------|
| Nov 2025 | **Clawdbot** | লঞ্চের সময়কার মূল নাম |
| 27 Jan 2026 | **Moltbot** | Anthropic-এর trademark complaint ("Claude"-এর সঙ্গে মিল) |
| 30 Jan 2026 | **OpenClaw** | কমিউনিটি ভোটের পর চূড়ান্ত rebrand |

### কার জন্য ভালো / কার জন্য নয়

**এটি ভালো, যদি আপনি চান:**

- নিজের laptop, desktop, home server বা VPS-এ personal assistant চালাতে
- দীর্ঘমেয়াদি chat history, file এবং automation এক workspace-এ রাখতে
- একই assistant-কে একাধিক messaging channel-এর সঙ্গে যুক্ত করতে
- tools, skills, browser automation বা multi-agent routing নিয়ে পরীক্ষা করতে

**এটি সেরা পছন্দ নয়, যদি আপনার দরকার হয়:**

- shared gateway-এ hostile multi-tenant isolation
- setup বা operational ownership ছাড়া zero-maintenance consumer app
- out-of-the-box enterprise compliance, SLA এবং vendor support

---

<a id="quick-start-setup-methods"></a>
## 2. দ্রুত শুরু ও সেটআপ পদ্ধতি

আপনি যদি একটি কাজই করেন, তাহলে কোনো external channel যোগ করার আগে local dashboard চালু করুন।

### সিস্টেমের প্রয়োজনীয়তা

| আইটেম | পরামর্শ |
|------|---------|
| Runtime | Node 24 recommended; minimum Node 22.16+ |
| OS | macOS বা Linux; Windows-এর জন্য WSL2 সুপারিশ করা হয় |
| প্রথম interface | Dashboard / WebChat |
| প্রথম setup flow | `openclaw onboard` |

### দ্রুত শুরু (১ মিনিট)

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
openclaw dashboard
```

### ইনস্টলেশনের পদ্ধতি

### পদ্ধতি ১: অফিসিয়াল installer script

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
openclaw onboard --install-daemon
```

### পদ্ধতি ২: npm / pnpm

```bash
npm install -g openclaw@latest
# অথবা
pnpm add -g openclaw@latest
```

### পদ্ধতি ৩: Docker

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
./docker-setup.sh
```

### পদ্ধতি ৪: one-click cloud deploy

| প্ল্যাটফর্ম | লিংক | নোট |
|------------|------|-----|
| **OpenClaw Launch** | [1-Click Deploy](https://www.aigeamy.com/) | অফিসিয়াল, শুরু করার দ্রুততম পথ |
| **Railway** | [Template](https://railway.com/deploy/openclaw) | web-based setup wizard |
| **DigitalOcean** | [1-Click Deploy](https://marketplace.digitalocean.com/apps/openclaw) | security-hardened, pre-configured |
| **Render** | [render.yaml](https://docs.openclaw.ai/render) | Infrastructure as Code |
| **SimpleClaw** | [simpleclaw.com](https://www.simpleclaw.com/) | এক মিনিটের কম সময়ে deploy |
| **Zeabur** | [Template](https://zeabur.com/templates/VTZ4FX) | one-click Docker deploy |
| **Northflank** | [Stack](https://northflank.com/stacks/deploy-openclaw) | server-side terminal দরকার নেই |
| **Lightning.AI** | [Environment](https://lightning.ai/lightning-ai/environments/openclaw) | browser-based, local hardware ছাড়াই |
| **Coolify** | [Template](https://github.com/essamamdani/openclaw-coolify) | self-hosted PaaS template |
| **Elestio** | [Open Source](https://elest.io/open-source/openclaw) | ৩ মিনিটের কম সময়ে fully managed |

### তুলনাযোগ্য AI Agent পণ্য

| # | পণ্য | ওয়েবসাইট | ধরন | Self-Host | Messaging Platforms |
|---|------|-----------|------|-----------|---------------------|
| 1 | **Hermes Agent** | [hermesagent.studio](https://hermesagent.studio/) | autonomous agent + messaging hub | Yes | WhatsApp, Telegram, Slack, Discord এবং আরও |
| 2 | **Multica** | [multica.uk](https://multica.uk/) | multi-channel AI automation | Yes | multi-platform |
| 3 | **GenericAgent** | [genericagent.org](https://www.genericagent.org/) | browser, terminal, filesystem এবং memory control সহ agent workspace | Not specified | Web workspace |
| 4 | **AutoGPT** | [agpt.co](https://agpt.co/) | autonomous task agent | Yes | API / web UI |
| 5 | **LangChain** | [langchain.com](https://www.langchain.com/) | LLM orchestration framework | Yes | যেকোনো প্ল্যাটফর্ম (custom integration-এর মাধ্যমে) |
| 6 | **n8n** | [n8n.io](https://n8n.io/) | workflow automation + AI nodes | Yes | Slack, Telegram, Discord এবং 400+ apps |
| 7 | **AgentGPT** | [agentgpt.reworkd.ai](https://agentgpt.reworkd.ai/) | browser-based autonomous agent | Yes | Web UI |
| 8 | **CrewAI** | [crewai.com](https://www.crewai.com/) | multi-agent role collaboration | Yes | API / custom integrations |
| 9 | **SuperAGI** | [superagi.com](https://superagi.com/) | autonomous agent infrastructure | Yes | Slack, Email, API |

### প্রথম ঘণ্টার চেকলিস্ট

1. `openclaw onboard` চালান এবং QuickStart বেছে নিন, যদি না আপনি আগেই exact config জানেন।
2. একটি model provider এবং একটি default model বেছে নিন।
3. প্রথম run-এ gateway local-only রাখুন।
4. dashboard খুলে নিশ্চিত করুন যে external channel ছাড়াই chat কাজ করছে।
5. এরপর একবারে শুধু একটি channel যোগ করুন।
6. remote exposure-এর আগে `openclaw doctor` এবং `openclaw security audit` চালান।

### শেখার যুক্তিসঙ্গত ক্রম

1. Dashboard বা WebChat দিয়ে শুরু
2. একটি model provider
3. একটি channel
4. security audit
5. skills এবং browser automation
6. remote access, VPS বা always-on deployment

---

<a id="install-paths"></a>
## 3. ইনস্টলেশন পথ

| পথ | কার জন্য | কেন কাজে লাগে | লিংক |
|-----|----------|----------------|------|
| CLI onboarding | বেশিরভাগ ডেভেলপার | দ্রুততম অফিসিয়াল পথ; gateway, workspace, channels, daemon এবং skills configure করে | [Getting Started](https://docs.openclaw.ai/start/getting-started) / [Onboarding](https://docs.openclaw.ai/start/wizard) |
| Docker | VPS, পরিষ্কার runtime isolation | runtime আলাদা রাখা এবং clean redeploy সহজ | [Docker](https://docs.openclaw.ai/install/docker) |
| Source থেকে | contributor এবং debugger | মূল repo থেকে পূর্ণ `pnpm` build ও watch workflow | [openclaw/openclaw](https://github.com/openclaw/openclaw) |
| Nix | reproducible environment | declarative setup এবং update | [nix-openclaw](https://github.com/openclaw/nix-openclaw) |
| macOS app path | Apple-কেন্দ্রিক setup | voice, canvas এবং native platform feature দরকার হলে উপকারী | [macOS Platform Docs](https://docs.openclaw.ai/platforms/macos) |

### সুপারিশ

সাধারণ ডেভেলপারের জন্য ডিফল্ট উত্তর এখনো একই: npm থেকে install করুন, onboarding চালান, এবং আরও বড় কিছু করার আগে dashboard-এ সব যাচাই করুন।

---

<a id="core-concepts-commands"></a>
## 4. মূল ধারণা ও কমান্ড

### প্রথম দিনেই বোঝা দরকার এমন ধারণা

| ধারণা | মানে | কেন গুরুত্বপূর্ণ |
|-------|------|------------------|
| Gateway | local control plane | config, session, channel, tool, dashboard এবং auth নিয়ন্ত্রণ করে |
| Agent | logical assistant identity | use case, workspace এবং model policy আলাদা করতে সাহায্য করে |
| Workspace | agent-এর file এবং prompt | skills, notes এবং task artifact এখানে থাকে |
| Channel | messaging integration | ব্যবহারকারীরা কীভাবে assistant-এ পৌঁছাবে তা নির্ধারণ করে |
| Session | conversation context | memory continuity এবং routing behavior নিয়ন্ত্রণ করে |
| Skill | packaged capability | common task-এর জন্য reusable prompt + file + script |
| Tool profile | allowed capability set | security এবং behavior-এর বড় lever |
| Model policy | primary model plus fallback | quality, cost এবং tool-safety posture নিয়ন্ত্রণ করে |

### তাড়াতাড়ি মনে রাখার মতো কমান্ড

| কাজ | কমান্ড |
|-----|--------|
| guided setup চালানো | `openclaw onboard` |
| পরে reconfigure করা | `openclaw configure` |
| browser dashboard খোলা | `openclaw dashboard` |
| health এবং migration দেখা | `openclaw doctor` |
| security posture audit | `openclaw security audit` |
| deep security audit | `openclaw security audit --deep` |
| নতুন agent যোগ করা | `openclaw agents add <name>` |
| config দেখা | `openclaw config get <path>` |
| config আপডেট | `openclaw config set <path> <value>` |
| model auth/status দেখা | `openclaw models status` |
| quick local prompt | `openclaw agent --message "Ship checklist"` |

### ব্যবহারিক পরামর্শ

- অনেক JSON হাতে edit করার আগে onboarding এবং `openclaw configure` ব্যবহার করুন।
- personal use এবং work automation আলাদা রাখতে চাইলে দ্রুত দ্বিতীয় agent তৈরি করুন।
- provider যদি "configured but not working" মনে হয়, `openclaw models status` দেখুন।

---

<a id="channels-what-to-connect-first"></a>
## 5. চ্যানেল: আগে কোনটি যুক্ত করবেন

প্রথম দিনেই পাঁচটি channel যুক্ত করবেন না। আপনার লক্ষ্য এবং setup tolerance অনুযায়ী surface বেছে নিন।

| চ্যানেল | সেরা প্রথম ব্যবহার | নোট | ডকস |
|---------|-------------------|------|------|
| WebChat | দ্রুততম smoke test | third-party bot setup লাগে না; প্রথম validation-এর জন্য আদর্শ | [WebChat](https://docs.openclaw.ai/web/webchat) |
| Telegram | সবচেয়ে সহজ external bot path | ডেভেলপারদের জন্য ভালো প্রথম real channel | [Telegram](https://docs.openclaw.ai/channels/telegram) |
| WhatsApp | দৈনন্দিন personal assistant | বাস্তব ব্যবহারে দারুণ, তবে DM policy কড়া রাখুন | [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) |
| Slack | টিম বা internal workflow | workspace access বাড়ানোর আগে trust boundary বুঝুন | [Slack](https://docs.openclaw.ai/channels/slack) |
| Discord | private server বা community experiment | খোলার আগে DM এবং group rule tighten করুন | [Discord](https://docs.openclaw.ai/channels/discord) |
| Signal | privacy-focused personal use | অতিরিক্ত dependency, তবে আপনি Signal ব্যবহার করলে সার্থক | [Signal](https://docs.openclaw.ai/channels/signal) |

### সহজ নিয়ম

- সবচেয়ে দ্রুত success path চান: WebChat বা Telegram দিয়ে শুরু করুন।
- সত্যিকারের daily-driver চান: dashboard স্থিতিশীল হলে WhatsApp-এ যান।
- টিম ব্যবহার চান: আগে security এবং agent separation শিখুন, তারপর Slack বা Discord ব্যবহার করুন।

---

<a id="deployment-choices"></a>
## 6. ডিপ্লয়মেন্ট পছন্দ

| পরিস্থিতি | সুপারিশকৃত পথ | কেন |
|-----------|----------------|-----|
| প্রথম মূল্যায়ন | local CLI onboarding + dashboard | কম complexity, সহজ debugging |
| personal always-on assistant | home server / Mac mini / Linux box + daemon | local ownership-সহ স্থিতিশীল daily-driver setup |
| সস্তা VPS | Docker | পরিষ্কার host boundary এবং সহজ redeploy |
| reproducible personal infra | Nix | declarative config এবং repeatable install |
| remote access | Tailscale বা SSH tunnel | gateway সরাসরি internet-এ expose করার চেয়ে নিরাপদ |
| multiple trust boundary | আলাদা gateway, আর আদর্শভাবে আলাদা OS user বা host | OpenClaw shared gateway-এ hostile multi-tenant isolation-এর জন্য ডিজাইন করা নয় |

### Remote deploy-এর আগে এটি পড়ুন

Remote access হলো এমন কিছু, যা local setup স্থিতিশীল হওয়ার পর যোগ করা উচিত। সবচেয়ে সাধারণ failure mode হলো pairing rule, allowlist, tool profile এবং agent boundary না ভেবেই শক্তিশালী assistant expose করে দেওয়া।

---

<a id="security-baseline"></a>
## 7. নিরাপত্তার বেসলাইন

এটি সেই অংশ, যা অনেক "awesome" তালিকা বাদ দেয়, কিন্তু ডেভেলপারদের সত্যিই দরকার।

### মৌলিক নিয়ম

- incoming DM, web content, shared chat এবং uploaded file-কে untrusted input হিসেবে দেখুন।
- সিস্টেম শেখার সময় DM access pairing বা strict allowlist mode-এ রাখুন।
- একাধিক ব্যক্তি bot-এ DM পাঠাতে পারলে `session.dmScope: "per-channel-peer"` বা তার চেয়েও কড়া সমতুল্য ব্যবহার করুন।
- group channel-কে mention-gated রাখুন, যদি না শক্তিশালী কারণ থাকে।
- restrictive tool profile দিয়ে শুরু করুন, এবং কারণ পরিষ্কার হলে তবেই access বাড়ান।
- shared বা non-main session-এর জন্য শুধু prompt discipline-এর উপর নির্ভর না করে sandboxing পছন্দ করুন।
- remote access এবং auth ইচ্ছাকৃতভাবে configure না করা পর্যন্ত gateway local-only রাখুন।
- নিয়মিত `openclaw security audit` চালান, আর exposure বাড়ানোর আগে `--deep` ব্যবহার করুন।
- personal এবং company trust boundary আলাদা agent-এ রাখুন, ভালো হলে আলাদা gateway বা host-এও রাখুন।

### উচ্চমূল্যের নিরাপত্তা লিংক

- [Security Guide](https://docs.openclaw.ai/gateway/security)
- [Sandboxing](https://docs.openclaw.ai/gateway/sandboxing)
- [Remote Access](https://docs.openclaw.ai/gateway/remote)
- [Tailscale](https://docs.openclaw.ai/gateway/tailscale)
- [Doctor](https://docs.openclaw.ai/gateway/doctor)

---

<a id="official-docs-by-goal"></a>
## 8. উদ্দেশ্যভিত্তিক অফিসিয়াল ডকস

| উদ্দেশ্য | সেরা লিংক |
|----------|-----------|
| প্রথম ইনস্টল | [Getting Started](https://docs.openclaw.ai/start/getting-started) |
| guided setup | [Onboarding (CLI)](https://docs.openclaw.ai/start/wizard) |
| browser-first testing | [Dashboard](https://docs.openclaw.ai/web/dashboard) |
| configuration | [Configuration](https://docs.openclaw.ai/gateway/configuration) |
| model setup | [Models CLI](https://docs.openclaw.ai/concepts/models) |
| channels overview | [Channels](https://docs.openclaw.ai/channels) |
| skills | [Skills](https://docs.openclaw.ai/tools/skills) |
| browser automation | [Browser Tool](https://docs.openclaw.ai/tools/browser) |
| Docker install | [Docker](https://docs.openclaw.ai/install/docker) |
| security hardening | [Security](https://docs.openclaw.ai/gateway/security) |
| remote exposure | [Remote Access](https://docs.openclaw.ai/gateway/remote) |
| Tailscale-এর মাধ্যমে remote access | [Tailscale](https://docs.openclaw.ai/gateway/tailscale) |
| troubleshooting | [FAQ](https://docs.openclaw.ai/help/faq) |

### সুপারিশকৃত পড়ার ক্রম

1. Getting Started
2. Onboarding
3. Dashboard
4. Configuration
5. একটি channel doc
6. Security
7. Skills, browser automation এবং remote access

---

<a id="curated-ecosystem-links"></a>
## 9. নির্বাচিত ইকোসিস্টেম লিংক

একটি working install হয়ে গেলে এই লিংকগুলো বেশি কাজে লাগবে। অফিসিয়াল onboarding পথ পরিষ্কার বোঝার পর এগুলোর মূল্য আরও বাড়ে।

### অফিসিয়াল

| রিসোর্স | কেন গুরুত্বপূর্ণ |
|---------|-----------------|
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | মূল codebase এবং authoritative README |
| [docs.openclaw.ai](https://docs.openclaw.ai) | অফিসিয়াল documentation hub |
| [openclaw/clawhub](https://github.com/openclaw/clawhub) | অফিসিয়াল skill directory এবং package catalog |
| [openclaw/nix-openclaw](https://github.com/openclaw/nix-openclaw) | reproducible install-এর জন্য Nix packaging |

### কমিউনিটি

| রিসোর্স | কেন গুরুত্বপূর্ণ |
|---------|-----------------|
| [essamamdani/openclaw-coolify](https://github.com/essamamdani/openclaw-coolify) | self-hosted PaaS ব্যবহারকারীদের জন্য Coolify template |
| [serhanekicii/openclaw-helm](https://github.com/serhanekicii/openclaw-helm) | Kubernetes-কেন্দ্রিক deployment হলে এটি কার্যকর Helm chart |
| [lunarpulse/openclaw-mcp-plugin](https://github.com/lunarpulse/openclaw-mcp-plugin) | MCP-oriented integration starting point |
| [centminmod/explain-openclaw](https://github.com/centminmod/explain-openclaw) | গভীর technical documentation এবং deployment/security notes |

---

<a id="common-mistakes"></a>
## 10. সাধারণ ভুল

- local chat কাজ করার আগে বিশাল hosting table পড়া
- একসঙ্গে অনেক channel যুক্ত করে পরিষ্কার পথের বদলে setup noise debug করা
- shared tool-enabled agent-কে safe multi-tenant app ধরে নেওয়া
- local-এ pairing, allowlist এবং auth পরীক্ষা করার আগে gateway expose করা
- personal এবং company trust boundary একই শক্তিশালী assistant runtime-এ মিশিয়ে ফেলা
- পরিকল্পনা ছাড়া কম শক্তিশালী hardware-এ strong local-model performance আশা করা
- onboarding sane baseline তৈরির আগেই অনেক config হাতে edit করা

---

<a id="contributing"></a>
## 11. অবদান

দেখুন [CONTRIBUTING.bn.md](./CONTRIBUTING.bn.md)।

নতুন লিংক যোগ করার সময় এমন রিসোর্সকে অগ্রাধিকার দিন, যা একজন সাধারণ ডেভেলপারকে নিচের যেকোনো কাজ ভালোভাবে করতে সাহায্য করে:

- OpenClaw ইনস্টল করা
- ঠিকভাবে configure করা
- যুক্তিসঙ্গতভাবে secure করা
- দ্রুত debug করা
- বাস্তব development payoff-সহ extend করা

---

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

এই তালিকা CC0 1.0 Universal (Public Domain) লাইসেন্সে প্রকাশিত।
