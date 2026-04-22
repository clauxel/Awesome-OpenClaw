# Awesome OpenClaw - डेवलपर-केंद्रित मार्गदर्शिका

**भाषाएं:** [English](README.md) | [简体中文](README.zh-CN.md) | **हिन्दी** | [Español](README.es.md) | [العربية](README.ar.md) | [Français](README.fr.md) | [বাংলা](README.bn.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Bahasa Indonesia](README.id.md)

[![Stars](https://img.shields.io/github/stars/openclaw/openclaw?style=flat&logo=github&label=Stars&color=gold)](https://github.com/openclaw/openclaw/stargazers)
[![Forks](https://img.shields.io/github/forks/openclaw/openclaw?style=flat&label=Forks&color=silver)](https://github.com/openclaw/openclaw/network/members)
[![Contributors](https://img.shields.io/github/contributors/openclaw/openclaw?label=Contributors&color=green)](https://github.com/openclaw/openclaw/graphs/contributors)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0 1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

यह OpenClaw के लिए डेवलपर-प्रथम क्यूरेटेड गाइड है। यह README प्रचार, कीमत तुलना तालिकाओं और जल्दी पुरानी हो जाने वाली मार्केटिंग दावों की जगह आधिकारिक दस्तावेज़ों, व्यावहारिक सेटअप क्रम, सुरक्षा आधाररेखा और लंबे समय तक उपयोगी रहने वाले इकोसिस्टम लिंक को प्राथमिकता देता है।

---

## विषय सूची

1. [उत्पाद अवलोकन](#product-overview)
2. [त्वरित शुरुआत और सेटअप तरीके](#quick-start-setup-methods)
3. [इंस्टॉल पथ](#install-paths)
4. [मुख्य अवधारणाएं और कमांड](#core-concepts-commands)
5. [चैनल: पहले क्या जोड़ें](#channels-what-to-connect-first)
6. [डिप्लॉयमेंट विकल्प](#deployment-choices)
7. [सुरक्षा आधाररेखा](#security-baseline)
8. [लक्ष्य के अनुसार आधिकारिक दस्तावेज़](#official-docs-by-goal)
9. [चयनित इकोसिस्टम लिंक](#curated-ecosystem-links)
10. [सामान्य गलतियां](#common-mistakes)
11. [योगदान](#contributing)

---

<a id="product-overview"></a>
## 1. उत्पाद अवलोकन

**OpenClaw** एक व्यक्तिगत AI सहायक है जिसे आप अपने उपकरणों पर चलाते हैं। इसका केंद्र **Gateway** है, जो agents, channels, sessions, tools, dashboard/web UI और remote access के लिए control plane की तरह काम करता है। इसे समझने का अच्छा तरीका यह है: OpenClaw "सिर्फ एक bot" नहीं है, बल्कि एक local-first assistant runtime है जो उन chat surfaces के भीतर रह सकता है जिनका आप पहले से उपयोग करते हैं।

### OpenClaw डेवलपर्स को वास्तव में क्या देता है

- CLI, dashboard, WebChat और remote access विकल्पों वाला एक local Gateway
- WhatsApp, Telegram, Slack, Discord, WebChat और अन्य सतहों पर multi-channel messaging
- अलग-अलग workspaces, sessions, bindings और model policies वाले कई agents
- hosted providers, OAuth-आधारित auth, API keys और local-model paths सहित flexible model setup
- skills, browser automation, nodes, cron jobs और अन्य tool-driven workflows
- personal-assistant trust model, न कि hostile multi-tenant SaaS security model

### मुख्य आर्किटेक्चर (6 परतें)

| परत | उद्देश्य |
|------|----------|
| **Gateway** | केंद्रीय control plane - message routing, sessions, plugins और tool execution policy |
| **Channels** | Telegram, WhatsApp, Discord, iMessage आदि को standard message shapes में normalize करने वाले adapters |
| **Routing + Sessions** | तय करता है कि कौन सा agent कौन सी conversation संभालेगा |
| **Agent Runtime** | context process करता है, model providers को call करता है, responses stream करता है और tools मांगता है |
| **Tools** | capabilities - web fetch, browser control, command execution, device pairing |
| **Surfaces** | interaction points - chat apps, web dashboard, macOS menu bar, Live Canvas |

### नाम का इतिहास

| तारीख | नाम | कारण |
|-------|-----|------|
| Nov 2025 | **Clawdbot** | लॉन्च के समय का मूल नाम |
| Jan 27, 2026 | **Moltbot** | Anthropic की trademark complaint ("Claude" से समानता) |
| Jan 30, 2026 | **OpenClaw** | अंतिम rebrand, community vote |

### किसके लिए अच्छा है / किसके लिए नहीं

**अच्छा है अगर आप चाहते हैं:**

- अपने laptop, desktop, home server या VPS पर personal assistant चलाना
- लंबे समय की chat history, files और automation को एक workspace में रखना
- उसी assistant को कई messaging channels से जोड़ना जो आप पहले से उपयोग करते हैं
- tools, skills, browser automation या multi-agent routing के साथ प्रयोग करना

**सबसे अच्छा विकल्प नहीं है अगर आपको चाहिए:**

- एक shared gateway पर hostile multi-tenant isolation
- बिना setup या operational ownership वाला zero-maintenance consumer app
- out-of-the-box enterprise compliance, SLA और vendor support

---

<a id="quick-start-setup-methods"></a>
## 2. त्वरित शुरुआत और सेटअप तरीके

अगर आप केवल एक काम करें, तो किसी भी external channel को जोड़ने से पहले local dashboard को काम करता हुआ देखें।

### सिस्टम आवश्यकताएं

| आइटम | सिफारिश |
|------|----------|
| Runtime | Node 24 recommended; न्यूनतम Node 22.16+ |
| OS | macOS या Linux; Windows के लिए WSL2 सुझाया गया रास्ता है |
| पहला interface | Dashboard / WebChat |
| पहला setup flow | `openclaw onboard` |

### त्वरित शुरुआत (1 मिनट)

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
openclaw dashboard
```

### इंस्टॉलेशन तरीके

### तरीका 1: आधिकारिक installer script

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
openclaw onboard --install-daemon
```

### तरीका 2: npm / pnpm

```bash
npm install -g openclaw@latest
# या
pnpm add -g openclaw@latest
```

### तरीका 3: Docker

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
./docker-setup.sh
```

### तरीका 4: one-click cloud deploys

| प्लेटफ़ॉर्म | लिंक | नोट्स |
|-------------|------|-------|
| **OpenClaw Launch** | [1-Click Deploy](https://www.aigeamy.com/) | आधिकारिक, शुरू करने का सबसे तेज रास्ता |
| **Railway** | [Template](https://railway.com/deploy/openclaw) | web-based setup wizard |
| **DigitalOcean** | [1-Click Deploy](https://marketplace.digitalocean.com/apps/openclaw) | security-hardened, pre-configured |
| **Render** | [render.yaml](https://docs.openclaw.ai/render) | Infrastructure as Code |
| **SimpleClaw** | [simpleclaw.com](https://www.simpleclaw.com/) | 1 मिनट से कम में deploy |
| **Zeabur** | [Template](https://zeabur.com/templates/VTZ4FX) | one-click Docker deploy |
| **Northflank** | [Stack](https://northflank.com/stacks/deploy-openclaw) | server-side terminal की जरूरत नहीं |
| **Lightning.AI** | [Environment](https://lightning.ai/lightning-ai/environments/openclaw) | browser-based, local hardware की जरूरत नहीं |
| **Coolify** | [Template](https://github.com/essamamdani/openclaw-coolify) | self-hosted PaaS template |
| **Elestio** | [Open Source](https://elest.io/open-source/openclaw) | 3 मिनट से कम में fully managed |

### मिलते-जुलते AI Agent प्रोडक्ट्स

| # | प्रोडक्ट | वेबसाइट | प्रकार | Self-Host | Messaging Platforms |
|---|----------|---------|--------|-----------|---------------------|
| 1 | **Hermes Agent** | [hermesagent.studio](https://hermesagent.studio/) | autonomous agent + messaging hub | Yes | WhatsApp, Telegram, Slack, Discord, और अन्य |
| 2 | **Multica** | [multica.uk](https://multica.uk/) | multi-channel AI automation | Yes | multi-platform |
| 3 | **GenericAgent** | [genericagent.org](https://www.genericagent.org/) | browser, terminal, filesystem और memory control वाला agent workspace | Not specified | Web workspace |
| 4 | **AutoGPT** | [agpt.co](https://agpt.co/) | autonomous task agent | Yes | API / web UI |
| 5 | **LangChain** | [langchain.com](https://www.langchain.com/) | LLM orchestration framework | Yes | कोई भी (custom integrations के जरिए) |
| 6 | **n8n** | [n8n.io](https://n8n.io/) | workflow automation + AI nodes | Yes | Slack, Telegram, Discord, और 400+ apps |
| 7 | **AgentGPT** | [agentgpt.reworkd.ai](https://agentgpt.reworkd.ai/) | browser-based autonomous agent | Yes | Web UI |
| 8 | **CrewAI** | [crewai.com](https://www.crewai.com/) | multi-agent role collaboration | Yes | API / custom integrations |
| 9 | **SuperAGI** | [superagi.com](https://superagi.com/) | autonomous agent infrastructure | Yes | Slack, Email, API |

### पहले घंटे की चेकलिस्ट

1. `openclaw onboard` चलाएं और QuickStart चुनें, जब तक कि आपको अपना exact config पहले से न पता हो।
2. एक model provider और एक default model चुनें।
3. पहली run में gateway को केवल local रखें।
4. dashboard खोलें और verify करें कि बिना external channel के भी chat काम कर रही है।
5. उसके बाद ठीक एक channel जोड़ें।
6. remote exposure से पहले `openclaw doctor` और `openclaw security audit` चलाएं।

### समझदार सीखने का क्रम

1. पहले Dashboard या WebChat
2. एक model provider
3. एक channel
4. security audit
5. skills और browser automation
6. remote access, VPS या always-on deployment

---

<a id="install-paths"></a>
## 3. इंस्टॉल पथ

| पथ | किसके लिए अच्छा | यह क्यों मदद करता है | लिंक |
|-----|------------------|----------------------|------|
| CLI onboarding | अधिकांश developers | सबसे तेज आधिकारिक रास्ता; gateway, workspace, channels, daemon और skills configure करता है | [Getting Started](https://docs.openclaw.ai/start/getting-started) / [Onboarding](https://docs.openclaw.ai/start/wizard) |
| Docker | VPS, साफ runtime isolation | runtime को contain करना और clean redeploy करना आसान | [Docker](https://docs.openclaw.ai/install/docker) |
| Source से | contributors और debuggers | main repo से पूरा `pnpm` build और watch workflow | [openclaw/openclaw](https://github.com/openclaw/openclaw) |
| Nix | reproducible environments | declarative setup और updates | [nix-openclaw](https://github.com/openclaw/nix-openclaw) |
| macOS app path | Apple-device-heavy setups | अगर आपको voice, canvas और native platform features की खास परवाह है तो उपयोगी | [macOS Platform Docs](https://docs.openclaw.ai/platforms/macos) |

### सिफारिश

सामान्य developer के लिए default जवाब अब भी यही है: npm से install करें, onboarding चलाएं, और कुछ ज्यादा महत्वाकांक्षी करने से पहले dashboard में सब verify करें।

---

<a id="core-concepts-commands"></a>
## 4. मुख्य अवधारणाएं और कमांड

### पहले दिन समझने लायक अवधारणाएं

| अवधारणा | अर्थ | यह क्यों महत्वपूर्ण है |
|---------|------|------------------------|
| Gateway | local control plane | config, sessions, channels, tools, dashboard और auth का मालिक |
| Agent | logical assistant identity | अलग use cases, workspaces और model policies रखने देता है |
| Workspace | agent के लिए files और prompts | skills, notes और task artifacts यहीं रहते हैं |
| Channel | messaging integration | तय करता है कि users assistant तक कैसे पहुंचेंगे |
| Session | conversation context | memory continuity और routing behavior नियंत्रित करता है |
| Skill | packaged capability | common tasks के लिए reusable prompt + files + scripts |
| Tool profile | allowed capability set | security और behavior के सबसे बड़े levers में से एक |
| Model policy | primary model plus fallbacks | quality, cost और tool-safety posture नियंत्रित करता है |

### जल्दी याद रखने लायक कमांड

| काम | कमांड |
|-----|--------|
| guided setup चलाना | `openclaw onboard` |
| बाद में reconfigure करना | `openclaw configure` |
| browser dashboard खोलना | `openclaw dashboard` |
| health और migrations देखना | `openclaw doctor` |
| security posture audit करना | `openclaw security audit` |
| deep security audit | `openclaw security audit --deep` |
| नया agent जोड़ना | `openclaw agents add <name>` |
| config देखना | `openclaw config get <path>` |
| config अपडेट करना | `openclaw config set <path> <value>` |
| model auth या status देखना | `openclaw models status` |
| quick local prompt | `openclaw agent --message "Ship checklist"` |

### व्यावहारिक सलाह

- बहुत सारा JSON हाथ से edit करने से पहले onboarding और `openclaw configure` का उपयोग करें।
- अगर personal use और work automation अलग रखना है, तो जल्दी दूसरा agent बनाएं।
- जब भी provider "configured but not working" जैसा लगे, `openclaw models status` देखें।

---

<a id="channels-what-to-connect-first"></a>
## 5. चैनल: पहले क्या जोड़ें

पहले दिन पांच चैनल मत जोड़ें। वही surface चुनें जो आपके वास्तविक लक्ष्य और setup tolerance से मेल खाता हो।

| चैनल | सबसे अच्छा पहला उपयोग | नोट्स | दस्तावेज़ |
|------|------------------------|-------|----------|
| WebChat | सबसे तेज smoke test | third-party bot setup की जरूरत नहीं; first validation के लिए आदर्श | [WebChat](https://docs.openclaw.ai/web/webchat) |
| Telegram | सबसे आसान external bot path | developers के लिए अच्छा पहला real channel | [Telegram](https://docs.openclaw.ai/channels/telegram) |
| WhatsApp | दैनिक personal assistant | real-world usage के लिए बढ़िया, पर DM policies tight रखें | [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) |
| Slack | टीम या internal workflow | broad workspace access से पहले trust boundaries समझें | [Slack](https://docs.openclaw.ai/channels/slack) |
| Discord | private server या community experiments | खोलने से पहले DM और group rules tighten करें | [Discord](https://docs.openclaw.ai/channels/discord) |
| Signal | privacy-oriented personal usage | extra dependency है, पर अगर आप Signal में रहते हैं तो worth it | [Signal](https://docs.openclaw.ai/channels/signal) |

### उपयोगी thumb rule

- सबसे तेज success path चाहिए: WebChat या Telegram से शुरू करें।
- असली daily-driver चाहिए: dashboard काम करने के बाद WhatsApp पर जाएं।
- team usage चाहिए: पहले security और agent separation सीखें, फिर Slack या Discord इस्तेमाल करें।

---

<a id="deployment-choices"></a>
## 6. डिप्लॉयमेंट विकल्प

| परिदृश्य | सुझाया गया रास्ता | क्यों |
|----------|-------------------|------|
| पहली evaluation | local CLI onboarding + dashboard | सबसे कम complexity और सबसे आसान debugging |
| personal always-on assistant | home server / Mac mini / Linux box + daemon | local ownership के साथ स्थिर daily-driver setup |
| सस्ता VPS | Docker | host boundary साफ और redeploy story सरल |
| reproducible personal infra | Nix | declarative config और repeatable installs |
| remote access | Tailscale या SSH tunnel | gateway को अंधाधुंध internet पर expose करने से सुरक्षित |
| multiple trust boundaries | अलग gateways, और आदर्श रूप से अलग OS users या hosts | OpenClaw एक shared gateway पर hostile multi-tenant isolation के लिए डिज़ाइन नहीं है |

### Remote deploy करने से पहले यह पढ़ें

Remote access वह चीज है जिसे local setup के बाद जोड़ना चाहिए, पहले नहीं। सबसे आम failure mode यह है कि pairing rules, allowlists, tool profiles और agent boundaries सोचे बिना एक शक्तिशाली assistant को expose कर दिया जाता है।

---

<a id="security-baseline"></a>
## 7. सुरक्षा आधाररेखा

यह वह सेक्शन है जिसे कई "awesome" lists छोड़ देती हैं, लेकिन developers को वास्तव में इसकी जरूरत होती है।

### आधारभूत नियम

- incoming DMs, web content, shared chats और uploaded files को untrusted input मानें।
- जब तक आप system सीख रहे हैं, DM access को pairing या strict allowlist mode में रखें।
- अगर एक से अधिक लोग bot को DM कर सकते हैं, तो `session.dmScope: "per-channel-peer"` या उससे सख्त equivalent उपयोग करें।
- group channels को mention-gated रखें, जब तक आपके पास कोई खास कारण न हो।
- restrictive tool profile से शुरू करें और केवल तभी access बढ़ाएं जब आपको कारण साफ पता हो।
- shared या non-main sessions के लिए सिर्फ prompt discipline पर भरोसा करने के बजाय sandboxing को प्राथमिकता दें।
- जब तक आप remote access और auth जानबूझकर configure न कर लें, gateway को local-only रखें।
- `openclaw security audit` नियमित रूप से चलाएं, और exposure बढ़ाने से पहले `--deep` का उपयोग करें।
- personal और company trust boundaries को अलग agents में रखें, और बेहतर हो तो अलग gateways या hosts पर।

### उच्च-मूल्य सुरक्षा लिंक

- [Security Guide](https://docs.openclaw.ai/gateway/security)
- [Sandboxing](https://docs.openclaw.ai/gateway/sandboxing)
- [Remote Access](https://docs.openclaw.ai/gateway/remote)
- [Tailscale](https://docs.openclaw.ai/gateway/tailscale)
- [Doctor](https://docs.openclaw.ai/gateway/doctor)

---

<a id="official-docs-by-goal"></a>
## 8. लक्ष्य के अनुसार आधिकारिक दस्तावेज़

| लक्ष्य | सबसे अच्छा लिंक |
|--------|-----------------|
| पहली install | [Getting Started](https://docs.openclaw.ai/start/getting-started) |
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
| Tailscale के जरिए remote access | [Tailscale](https://docs.openclaw.ai/gateway/tailscale) |
| troubleshooting | [FAQ](https://docs.openclaw.ai/help/faq) |

### सुझाया गया पढ़ने का क्रम

1. Getting Started
2. Onboarding
3. Dashboard
4. Configuration
5. एक channel का document
6. Security
7. Skills, browser automation, और remote access

---

<a id="curated-ecosystem-links"></a>
## 9. चयनित इकोसिस्टम लिंक

इन लिंक को तब देखें जब आपका एक working install तैयार हो जाए। official onboarding path समझ आने के बाद ये बहुत ज्यादा उपयोगी लगते हैं।

### आधिकारिक

| संसाधन | यह क्यों महत्वपूर्ण है |
|--------|------------------------|
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | main codebase और authoritative README |
| [docs.openclaw.ai](https://docs.openclaw.ai) | आधिकारिक documentation hub |
| [openclaw/clawhub](https://github.com/openclaw/clawhub) | आधिकारिक skill directory और package catalog |
| [openclaw/nix-openclaw](https://github.com/openclaw/nix-openclaw) | reproducible installs के लिए Nix packaging |

### समुदाय

| संसाधन | यह क्यों महत्वपूर्ण है |
|--------|------------------------|
| [essamamdani/openclaw-coolify](https://github.com/essamamdani/openclaw-coolify) | self-hosted PaaS users के लिए Coolify template |
| [serhanekicii/openclaw-helm](https://github.com/serhanekicii/openclaw-helm) | अगर आपका deployment world Kubernetes है तो Helm chart |
| [lunarpulse/openclaw-mcp-plugin](https://github.com/lunarpulse/openclaw-mcp-plugin) | MCP-oriented integration starting point |
| [centminmod/explain-openclaw](https://github.com/centminmod/explain-openclaw) | गहरी technical documentation और deployment या security notes |

---

<a id="common-mistakes"></a>
## 10. सामान्य गलतियां

- local chat काम करने से पहले ही बड़े hosting tables पढ़ना
- बहुत सारे channels एक साथ जोड़ना और साफ path की जगह setup noise debug करना
- shared tool-enabled agent को safe multi-tenant app समझना
- pairing, allowlists और auth को locally test करने से पहले gateway expose करना
- personal और company trust boundaries को एक ही शक्तिशाली assistant runtime में मिलाना
- underpowered hardware पर बिना planning के strong local-model performance की उम्मीद करना
- onboarding से sane baseline बनने से पहले बहुत सारा config हाथ से edit करना

---

<a id="contributing"></a>
## 11. योगदान

देखें [CONTRIBUTING.hi.md](./CONTRIBUTING.hi.md)।

लिंक जोड़ते समय उन संसाधनों को प्राथमिकता दें जो किसी सामान्य developer को इनमें से कोई काम अच्छे से करने में मदद करें:

- OpenClaw install करना
- इसे सही तरीके से configure करना
- इसे समझदारी से secure करना
- इसे तेजी से debug करना
- इसे वास्तविक development payoff के साथ extend करना

---

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

यह सूची CC0 1.0 Universal (Public Domain) के तहत जारी की गई है।
