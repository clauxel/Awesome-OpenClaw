# Awesome OpenClaw - دليل يركز على المطورين

**اللغات:** [English](README.md) | [简体中文](README.zh-CN.md) | [हिन्दी](README.hi.md) | [Español](README.es.md) | **العربية** | [Français](README.fr.md) | [বাংলা](README.bn.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Bahasa Indonesia](README.id.md)

[![Stars](https://img.shields.io/github/stars/openclaw/openclaw?style=flat&logo=github&label=Stars&color=gold)](https://github.com/openclaw/openclaw/stargazers)
[![Forks](https://img.shields.io/github/forks/openclaw/openclaw?style=flat&label=Forks&color=silver)](https://github.com/openclaw/openclaw/network/members)
[![Contributors](https://img.shields.io/github/contributors/openclaw/openclaw?label=Contributors&color=green)](https://github.com/openclaw/openclaw/graphs/contributors)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0 1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

هذا دليل منسق لـ OpenClaw يضع المطورين أولاً. يركز هذا README على الوثائق الرسمية، وترتيب الإعداد العملي، وخطوط الأمان الأساسية، وروابط النظام البيئي التي تبقى مفيدة لفترة طويلة، بدلاً من الضجة التسويقية وجداول الأسعار والمقارنات سريعة التقادم.

---

## جدول المحتويات

1. [نظرة عامة على المنتج](#product-overview)
2. [البدء السريع وطرق التثبيت](#quick-start-setup-methods)
3. [مسارات التثبيت](#install-paths)
4. [المفاهيم الأساسية والأوامر](#core-concepts-commands)
5. [القنوات: ماذا توصل أولاً](#channels-what-to-connect-first)
6. [خيارات النشر](#deployment-choices)
7. [الخط الأساسي للأمان](#security-baseline)
8. [الوثائق الرسمية حسب الهدف](#official-docs-by-goal)
9. [روابط منتقاة من النظام البيئي](#curated-ecosystem-links)
10. [أخطاء شائعة](#common-mistakes)
11. [المساهمة](#contributing)

---

<a id="product-overview"></a>
## 1. نظرة عامة على المنتج

**OpenClaw** هو مساعد ذكاء اصطناعي شخصي تشغله على أجهزتك الخاصة. وفي المركز يوجد **Gateway** الذي يعمل كطبقة التحكم للـ agents وchannels وsessions وtools وdashboard/web UI والوصول البعيد. والطريقة الأفضل لفهمه هي: OpenClaw ليس "مجرد bot"، بل runtime محلي أولاً يمكنه العيش داخل واجهات الدردشة التي تستخدمها بالفعل.

### ماذا يقدم OpenClaw فعلاً للمطورين

- Gateway محلي مع CLI وdashboard وWebChat وخيارات وصول بعيد
- مراسلة متعددة القنوات عبر WhatsApp وTelegram وSlack وDiscord وWebChat وغير ذلك
- عدة agents مع workspaces وsessions وbindings وسياسات نماذج منفصلة
- إعداد مرن للنماذج مع providers مستضافة ومصادقة OAuth وAPI keys ومسارات نماذج محلية
- skills وأتمتة المتصفح وnodes وcron jobs وسير عمل أخرى تعتمد على الأدوات
- نموذج ثقة لمساعد شخصي، وليس نموذج SaaS متعدد المستأجرين في بيئة عدائية

### البنية الأساسية (6 طبقات)

| الطبقة | الغرض |
|--------|-------|
| **Gateway** | طبقة التحكم المركزية: توجيه الرسائل، الجلسات، الإضافات، وسياسة تنفيذ الأدوات |
| **Channels** | محولات توحد Telegram وWhatsApp وDiscord وiMessage في شكل رسائل موحد |
| **Routing + Sessions** | تحدد أي agent يعالج أي محادثة |
| **Agent Runtime** | يعالج السياق، يستدعي مزودي النماذج، يبث الردود، ويطلب الأدوات |
| **Tools** | قدرات مثل web fetch والتحكم بالمتصفح وتنفيذ الأوامر وربط الأجهزة |
| **Surfaces** | نقاط التفاعل مثل تطبيقات الدردشة واللوحة web dashboard وشريط macOS وLive Canvas |

### تاريخ الاسم

| التاريخ | الاسم | السبب |
|---------|------|-------|
| نوفمبر 2025 | **Clawdbot** | الاسم الأصلي عند الإطلاق |
| 27 يناير 2026 | **Moltbot** | شكوى علامة تجارية من Anthropic بسبب التشابه مع "Claude" |
| 30 يناير 2026 | **OpenClaw** | إعادة التسمية النهائية بعد تصويت المجتمع |

### مناسب لمن / غير مناسب لمن

**مناسب إذا كنت تريد:**

- تشغيل مساعد شخصي على اللابتوب أو الحاسوب المكتبي أو الخادم المنزلي أو VPS
- الاحتفاظ بسجل دردشة طويل الأمد وملفات وأتمتة داخل workspace واحد
- توصيل نفس المساعد بعدة قنوات مراسلة تستخدمها بالفعل
- تجربة tools وskills وأتمتة المتصفح أو routing متعدد agents

**ليس الخيار الأفضل إذا كنت تحتاج:**

- عزلاً عدائياً متعدد المستأجرين على gateway مشترك
- تطبيقاً استهلاكياً بلا إعداد ولا مسؤولية تشغيلية
- امتثالاً مؤسسياً أو SLA أو دعم مورد بشكل جاهز

---

<a id="quick-start-setup-methods"></a>
## 2. البدء السريع وطرق التثبيت

إذا فعلت شيئاً واحداً فقط، فاجعل الـ dashboard المحلي يعمل قبل توصيل أي قناة خارجية.

### متطلبات النظام

| العنصر | التوصية |
|--------|---------|
| Runtime | يوصى بـ Node 24؛ الحد الأدنى Node 22.16+ |
| نظام التشغيل | macOS أو Linux؛ وعلى Windows يوصى باستخدام WSL2 |
| الواجهة الأولى | Dashboard / WebChat |
| أول مسار إعداد | `openclaw onboard` |

### البدء السريع (دقيقة واحدة)

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
openclaw dashboard
```

### طرق التثبيت

### الطريقة 1: سكربت التثبيت الرسمي

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
openclaw onboard --install-daemon
```

### الطريقة 2: npm / pnpm

```bash
npm install -g openclaw@latest
# أو
pnpm add -g openclaw@latest
```

### الطريقة 3: Docker

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
./docker-setup.sh
```

### الطريقة 4: نشر سحابي بنقرة واحدة

| المنصة | الرابط | ملاحظات |
|--------|--------|---------|
| **OpenClaw Launch** | [1-Click Deploy](https://www.aigeamy.com/) | رسمي وأسرع طريقة للبدء |
| **Railway** | [Template](https://railway.com/deploy/openclaw) | معالج إعداد عبر الويب |
| **DigitalOcean** | [1-Click Deploy](https://marketplace.digitalocean.com/apps/openclaw) | مهيأ مسبقاً ومقوى أمنياً |
| **Render** | [render.yaml](https://docs.openclaw.ai/render) | بنية تحتية ككود |
| **SimpleClaw** | [simpleclaw.com](https://www.simpleclaw.com/) | نشر في أقل من دقيقة |
| **Zeabur** | [Template](https://zeabur.com/templates/VTZ4FX) | نشر Docker بنقرة واحدة |
| **Northflank** | [Stack](https://northflank.com/stacks/deploy-openclaw) | لا يحتاج إلى terminal على الخادم |
| **Lightning.AI** | [Environment](https://lightning.ai/lightning-ai/environments/openclaw) | عبر المتصفح ومن دون عتاد محلي |
| **Coolify** | [Template](https://github.com/essamamdani/openclaw-coolify) | قالب PaaS مستضاف ذاتياً |
| **Elestio** | [Open Source](https://elest.io/open-source/openclaw) | مُدار بالكامل في أقل من 3 دقائق |

### منتجات AI Agent مشابهة

| # | المنتج | الموقع | النوع | Self-Host | منصات المراسلة |
|---|--------|--------|-------|-----------|----------------|
| 1 | **Hermes Agent** | [hermesagent.studio](https://hermesagent.studio/) | agent ذاتي + مركز مراسلة | نعم | WhatsApp وTelegram وSlack وDiscord وغير ذلك |
| 2 | **Multica** | [multica.uk](https://multica.uk/) | أتمتة AI متعددة القنوات | نعم | متعدد المنصات |
| 3 | **GenericAgent** | [genericagent.org](https://www.genericagent.org/) | مساحة عمل agent مع تحكم في المتصفح والطرفية ونظام الملفات والذاكرة | غير محدد | مساحة عمل Web |
| 4 | **AutoGPT** | [agpt.co](https://agpt.co/) | agent مهام ذاتي | نعم | API / web UI |
| 5 | **LangChain** | [langchain.com](https://www.langchain.com/) | إطار orchestration لـ LLM | نعم | أي منصة عبر تكاملات مخصصة |
| 6 | **n8n** | [n8n.io](https://n8n.io/) | أتمتة workflows + عقد AI | نعم | Slack وTelegram وDiscord وأكثر من 400 تطبيق |
| 7 | **AgentGPT** | [agentgpt.reworkd.ai](https://agentgpt.reworkd.ai/) | agent ذاتي قائم على المتصفح | نعم | Web UI |
| 8 | **CrewAI** | [crewai.com](https://www.crewai.com/) | تعاون متعدد agents حسب الأدوار | نعم | API / تكاملات مخصصة |
| 9 | **SuperAGI** | [superagi.com](https://superagi.com/) | بنية تحتية لوكلاء ذاتيين | نعم | Slack وEmail وAPI |

### قائمة تحقق الساعة الأولى

1. شغّل `openclaw onboard` واختر QuickStart ما لم تكن تعرف بالضبط الإعداد الذي تريده.
2. اختر مزود نماذج واحداً ونموذجاً افتراضياً واحداً.
3. أبقِ الـ gateway محلياً فقط في التشغيل الأول.
4. افتح الـ dashboard وتأكد من أنك تستطيع الدردشة بدون أي قناة خارجية.
5. بعد ذلك أضف قناة واحدة فقط.
6. شغّل `openclaw doctor` و`openclaw security audit` قبل تعريض أي شيء للوصول البعيد.

### ترتيب تعلم منطقي

1. ابدأ بـ Dashboard أو WebChat
2. مزود نماذج واحد
3. قناة واحدة
4. تدقيق أمني
5. skills وأتمتة المتصفح
6. وصول بعيد أو VPS أو نشر دائم

---

<a id="install-paths"></a>
## 3. مسارات التثبيت

| المسار | الأفضل لـ | لماذا يفيد | الرابط |
|--------|-----------|------------|--------|
| CLI onboarding | معظم المطورين | أسرع طريق رسمي؛ يضبط gateway وworkspace وchannels وdaemon وskills | [Getting Started](https://docs.openclaw.ai/start/getting-started) / [Onboarding](https://docs.openclaw.ai/start/wizard) |
| Docker | VPS وعزل أنظف للـ runtime | أسهل في الاحتواء وإعادة النشر بنظافة | [Docker](https://docs.openclaw.ai/install/docker) |
| من المصدر | المساهمون ومصححو الأخطاء | سير build ومراقبة كامل عبر `pnpm` من المستودع الرئيسي | [openclaw/openclaw](https://github.com/openclaw/openclaw) |
| Nix | البيئات القابلة لإعادة الإنتاج | إعداد وتحديثات تعريفية | [nix-openclaw](https://github.com/openclaw/nix-openclaw) |
| مسار تطبيق macOS | بيئات تعتمد على أجهزة Apple | مفيد إذا كانت الأولوية للصوت وcanvas والميزات الأصلية | [macOS Platform Docs](https://docs.openclaw.ai/platforms/macos) |

### التوصية

بالنسبة لمعظم المطورين، يبقى الجواب الافتراضي هو: ثبّت من npm، شغّل onboarding، وتحقق من كل شيء في dashboard قبل أي خطوة أكثر طموحاً.

---

<a id="core-concepts-commands"></a>
## 4. المفاهيم الأساسية والأوامر

### مفاهيم مهمة من اليوم الأول

| المفهوم | معناه | لماذا يهم |
|---------|-------|-----------|
| Gateway | طبقة التحكم المحلية | يملك config وsessions وchannels وtools وdashboard وauth |
| Agent | هوية منطقية للمساعد | تسمح بفصل حالات الاستخدام وworkspaces وسياسات النماذج |
| Workspace | ملفات وموجهات agent | هنا تعيش skills والملاحظات ومخرجات المهام |
| Channel | تكامل مراسلة | يحدد كيف يصل المستخدمون إلى المساعد |
| Session | سياق محادثة | يتحكم في استمرارية الذاكرة وسلوك routing |
| Skill | قدرة مغلفة | prompt + ملفات + سكربتات قابلة لإعادة الاستخدام |
| Tool profile | مجموعة القدرات المسموح بها | من أهم مفاتيح الأمان والسلوك |
| Model policy | النموذج الأساسي مع fallback | يتحكم في الجودة والتكلفة ووضع الأمان |

### أوامر ينبغي حفظها مبكراً

| المهمة | الأمر |
|--------|-------|
| تشغيل الإعداد الموجّه | `openclaw onboard` |
| إعادة الضبط لاحقاً | `openclaw configure` |
| فتح dashboard في المتصفح | `openclaw dashboard` |
| فحص الصحة والترحيلات | `openclaw doctor` |
| تدقيق الوضع الأمني | `openclaw security audit` |
| تدقيق أمني عميق | `openclaw security audit --deep` |
| إضافة agent جديد | `openclaw agents add <name>` |
| فحص config | `openclaw config get <path>` |
| تحديث config | `openclaw config set <path> <value>` |
| التحقق من auth أو حالة النموذج | `openclaw models status` |
| prompt محلي سريع | `openclaw agent --message "Ship checklist"` |

### نصائح عملية

- استخدم onboarding و`openclaw configure` قبل تعديل الكثير من JSON يدوياً.
- أنشئ agent ثانياً مبكراً إذا أردت فصل الاستخدام الشخصي عن أتمتة العمل.
- افحص `openclaw models status` كلما بدا أن المزود "مُعد ولكنه لا يعمل".

---

<a id="channels-what-to-connect-first"></a>
## 5. القنوات: ماذا توصل أولاً

لا توصل خمس قنوات في اليوم الأول. اختر السطح الذي يطابق هدفك الفعلي وقدرتك على تحمل تعقيد الإعداد.

| القناة | أفضل استخدام أول | ملاحظات | الوثائق |
|--------|------------------|---------|---------|
| WebChat | أسرع اختبار أولي | لا يحتاج إلى إعداد bot خارجي؛ مثالي لأول تحقق | [WebChat](https://docs.openclaw.ai/web/webchat) |
| Telegram | أسهل مسار لبوت خارجي | قناة أولى ممتازة للمطورين | [Telegram](https://docs.openclaw.ai/channels/telegram) |
| WhatsApp | مساعد شخصي يومي | ممتاز للاستخدام الحقيقي لكن شدد سياسات DM | [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) |
| Slack | فريق أو workflow داخلي | افهم حدود الثقة قبل توسيع وصول workspace | [Slack](https://docs.openclaw.ai/channels/slack) |
| Discord | خادم خاص أو تجارب مجتمع | شدد قواعد DM والمجموعات قبل فتحه | [Discord](https://docs.openclaw.ai/channels/discord) |
| Signal | استخدام شخصي يركز على الخصوصية | يحتاج اعتماداً إضافياً لكنه يستحق إذا كنت تستخدم Signal أصلاً | [Signal](https://docs.openclaw.ai/channels/signal) |

### قاعدة عملية مفيدة

- تريد أسرع طريق للنجاح: ابدأ بـ WebChat أو Telegram.
- تريد مساعداً يومياً حقيقياً: انتقل إلى WhatsApp بعد أن يعمل dashboard.
- تريد استخداماً للفريق: تعلم الأمان وفصل agents أولاً ثم استخدم Slack أو Discord.

---

<a id="deployment-choices"></a>
## 6. خيارات النشر

| السيناريو | المسار الموصى به | لماذا |
|-----------|------------------|-------|
| التقييم الأولي | onboarding محلي عبر CLI + dashboard | أقل تعقيداً وأسهل في التصحيح |
| مساعد شخصي دائم | خادم منزلي / Mac mini / جهاز Linux + daemon | إعداد ثابت للاستخدام اليومي مع ملكية محلية |
| VPS رخيص | Docker | حدود أوضح للمضيف وإعادة نشر أبسط |
| بنية شخصية قابلة لإعادة الإنتاج | Nix | config تعريفية وتثبيتات قابلة للتكرار |
| وصول بعيد | Tailscale أو نفق SSH | أكثر أماناً من تعريض gateway مباشرة للإنترنت |
| حدود ثقة متعددة | Gateways منفصلة، ويفضل مستخدمو نظام أو مضيفون منفصلون | OpenClaw غير مصمم لعزل عدائي متعدد المستأجرين على gateway واحد |

### اقرأ هذا قبل النشر البعيد

الوصول البعيد شيء تضيفه بعد نجاح الإعداد المحلي، وليس قبله. أكثر نمط فشل شائع هو تعريض مساعد قوي قبل التفكير في pairing rules وallowlists وtool profiles وحدود agents.

---

<a id="security-baseline"></a>
## 7. الخط الأساسي للأمان

هذا هو القسم الذي تتجاوزه كثير من قوائم "awesome" بينما يحتاجه المطورون فعلاً.

### القواعد الأساسية

- تعامل مع DMs الواردة ومحتوى الويب والمحادثات المشتركة والملفات المرفوعة كمدخلات غير موثوقة.
- أبقِ وصول DM في وضع pairing أو allowlist صارم بينما ما زلت تتعلم النظام.
- إذا كان أكثر من شخص يستطيع إرسال DM إلى bot فاستخدم `session.dmScope: "per-channel-peer"` أو ما هو أشد.
- أبقِ قنوات المجموعات مقيدة بالمنشن ما لم يكن لديك سبب واضح لغير ذلك.
- ابدأ بـ tool profile مقيد ولا توسع الصلاحيات إلا عندما تعرف السبب تماماً.
- للجلسات المشتركة أو غير الرئيسية، فضّل sandboxing بدلاً من الاعتماد على الانضباط في prompts فقط.
- أبقِ الـ gateway محلياً فقط حتى تضبط الوصول البعيد وauth بشكل مقصود.
- شغّل `openclaw security audit` بانتظام واستخدم `--deep` قبل توسيع التعرض.
- افصل حدود الثقة الشخصية وحدود العمل في agents مختلفة، ويفضل في gateways أو hosts منفصلة.

### روابط أمان عالية القيمة

- [Security Guide](https://docs.openclaw.ai/gateway/security)
- [Sandboxing](https://docs.openclaw.ai/gateway/sandboxing)
- [Remote Access](https://docs.openclaw.ai/gateway/remote)
- [Tailscale](https://docs.openclaw.ai/gateway/tailscale)
- [Doctor](https://docs.openclaw.ai/gateway/doctor)

---

<a id="official-docs-by-goal"></a>
## 8. الوثائق الرسمية حسب الهدف

| الهدف | أفضل رابط |
|-------|-----------|
| أول تثبيت | [Getting Started](https://docs.openclaw.ai/start/getting-started) |
| إعداد موجّه | [Onboarding (CLI)](https://docs.openclaw.ai/start/wizard) |
| اختبار يبدأ من المتصفح | [Dashboard](https://docs.openclaw.ai/web/dashboard) |
| الإعدادات | [Configuration](https://docs.openclaw.ai/gateway/configuration) |
| إعداد النماذج | [Models CLI](https://docs.openclaw.ai/concepts/models) |
| نظرة عامة على القنوات | [Channels](https://docs.openclaw.ai/channels) |
| Skills | [Skills](https://docs.openclaw.ai/tools/skills) |
| أتمتة المتصفح | [Browser Tool](https://docs.openclaw.ai/tools/browser) |
| تثبيت Docker | [Docker](https://docs.openclaw.ai/install/docker) |
| تقوية الأمان | [Security](https://docs.openclaw.ai/gateway/security) |
| التعريض البعيد | [Remote Access](https://docs.openclaw.ai/gateway/remote) |
| الوصول البعيد عبر Tailscale | [Tailscale](https://docs.openclaw.ai/gateway/tailscale) |
| استكشاف الأخطاء | [FAQ](https://docs.openclaw.ai/help/faq) |

### ترتيب قراءة مقترح

1. Getting Started
2. Onboarding
3. Dashboard
4. Configuration
5. وثيقة قناة واحدة
6. Security
7. Skills وأتمتة المتصفح والوصول البعيد

---

<a id="curated-ecosystem-links"></a>
## 9. روابط منتقاة من النظام البيئي

تصفح هذه الروابط بعد أن يصبح لديك تثبيت يعمل فعلاً. تصبح أكثر فائدة بكثير عندما يكون مسار onboarding الرسمي واضحاً لديك.

### رسمي

| المورد | لماذا يهم |
|--------|-----------|
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | المستودع الرئيسي وREADME المرجعي |
| [docs.openclaw.ai](https://docs.openclaw.ai) | مركز الوثائق الرسمي |
| [openclaw/clawhub](https://github.com/openclaw/clawhub) | دليل skills الرسمي وفهرس الحزم |
| [openclaw/nix-openclaw](https://github.com/openclaw/nix-openclaw) | تغليف Nix لتثبيتات قابلة لإعادة الإنتاج |

### المجتمع

| المورد | لماذا يهم |
|--------|-----------|
| [essamamdani/openclaw-coolify](https://github.com/essamamdani/openclaw-coolify) | قالب Coolify لمستخدمي PaaS المستضاف ذاتياً |
| [serhanekicii/openclaw-helm](https://github.com/serhanekicii/openclaw-helm) | Helm chart إذا كان عالم النشر لديك هو Kubernetes |
| [lunarpulse/openclaw-mcp-plugin](https://github.com/lunarpulse/openclaw-mcp-plugin) | نقطة انطلاق لتكاملات MCP |
| [centminmod/explain-openclaw](https://github.com/centminmod/explain-openclaw) | وثائق تقنية عميقة وملاحظات حول النشر أو الأمان |

---

<a id="common-mistakes"></a>
## 10. أخطاء شائعة

- قراءة جداول استضافة ضخمة قبل أن يعمل chat المحلي
- توصيل قنوات كثيرة دفعة واحدة ثم تصحيح ضوضاء الإعداد بدلاً من مسار واضح
- التعامل مع agent مشترك يملك tools كأنه تطبيق آمن متعدد المستأجرين
- تعريض gateway للوصول البعيد قبل اختبار pairing وallowlists وauth محلياً
- خلط حدود الثقة الشخصية وحدود العمل داخل runtime مساعد قوي واحد
- توقع أداء قوي للنماذج المحلية على عتاد ضعيف من دون تخطيط
- تعديل كثير من config يدوياً قبل أن يصنع onboarding خطاً أساسياً سليماً

---

<a id="contributing"></a>
## 11. المساهمة

راجع [CONTRIBUTING.ar.md](./CONTRIBUTING.ar.md).

عند إضافة روابط جديدة، فضّل الموارد التي تساعد المطور العادي على إنجاز واحد من هذه الأعمال بشكل جيد:

- تثبيت OpenClaw
- ضبطه بشكل صحيح
- تأمينه بشكل معقول
- تسريع تصحيح مشكلاته
- توسيعه بعائد تطويري حقيقي

---

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

هذه القائمة منشورة تحت رخصة CC0 1.0 Universal (الملكية العامة).
