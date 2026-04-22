# Awesome OpenClaw - Руководство для разработчиков

**Языки:** [English](README.md) | [简体中文](README.zh-CN.md) | [हिन्दी](README.hi.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Français](README.fr.md) | [বাংলা](README.bn.md) | [Português](README.pt.md) | **Русский** | [Bahasa Indonesia](README.id.md)

[![Stars](https://img.shields.io/github/stars/openclaw/openclaw?style=flat&logo=github&label=Stars&color=gold)](https://github.com/openclaw/openclaw/stargazers)
[![Forks](https://img.shields.io/github/forks/openclaw/openclaw?style=flat&label=Forks&color=silver)](https://github.com/openclaw/openclaw/network/members)
[![Contributors](https://img.shields.io/github/contributors/openclaw/openclaw?label=Contributors&color=green)](https://github.com/openclaw/openclaw/graphs/contributors)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0 1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

Это curated guide по OpenClaw с приоритетом на разработчиков. В этом README важнее официальная документация, практичный порядок старта, базовая безопасность и долговечные ссылки на экосистему, а не хайп, прайс-таблицы и быстро устаревающие маркетинговые обещания.

---

## Содержание

1. [Обзор продукта](#product-overview)
2. [Быстрый старт и способы установки](#quick-start-setup-methods)
3. [Пути установки](#install-paths)
4. [Ключевые концепции и команды](#core-concepts-commands)
5. [Каналы: что подключать первым](#channels-what-to-connect-first)
6. [Варианты развертывания](#deployment-choices)
7. [Базовый уровень безопасности](#security-baseline)
8. [Официальные документы по целям](#official-docs-by-goal)
9. [Подборка ссылок экосистемы](#curated-ecosystem-links)
10. [Частые ошибки](#common-mistakes)
11. [Как внести вклад](#contributing)

---

<a id="product-overview"></a>
## 1. Обзор продукта

**OpenClaw** — это персональный AI-ассистент, который вы запускаете на своих устройствах. В центре находится **Gateway**, выступающий control plane для agents, channels, sessions, tools, dashboard/web UI и удаленного доступа. Удобно думать о нем так: OpenClaw — это не "просто bot", а local-first runtime для ассистента, который может жить внутри тех чатов, которыми вы уже пользуетесь.

### Что OpenClaw реально дает разработчикам

- Локальный Gateway с CLI, dashboard, WebChat и вариантами удаленного доступа
- Multi-channel messaging через WhatsApp, Telegram, Slack, Discord, WebChat и другие поверхности
- Несколько agents с отдельными workspaces, sessions, bindings и model policies
- Гибкую настройку моделей: hosted providers, OAuth auth, API keys и пути к локальным моделям
- skills, browser automation, nodes, cron jobs и другие tool-driven workflow
- Модель доверия личного ассистента, а не hostile multi-tenant SaaS security model

### Базовая архитектура (6 слоев)

| Слой | Назначение |
|------|------------|
| **Gateway** | Центральный control plane: routing сообщений, sessions, plugins и policy выполнения tools |
| **Channels** | Адаптеры, приводящие Telegram, WhatsApp, Discord и iMessage к единому формату сообщений |
| **Routing + Sessions** | Определяет, какой agent обрабатывает какой диалог |
| **Agent Runtime** | Обрабатывает контекст, вызывает providers моделей, стримит ответы и запрашивает tools |
| **Tools** | Возможности вроде web fetch, управления браузером, выполнения команд и pairing устройств |
| **Surfaces** | Точки взаимодействия: чат-приложения, web dashboard, строка меню macOS и Live Canvas |

### История названия

| Дата | Название | Причина |
|------|----------|---------|
| Ноябрь 2025 | **Clawdbot** | Исходное название при запуске |
| 27 января 2026 | **Moltbot** | Жалоба Anthropic по товарному знаку из-за сходства с "Claude" |
| 30 января 2026 | **OpenClaw** | Финальный ребрендинг после голосования сообщества |

### Когда подходит / когда нет

**Подходит, если вы хотите:**

- запускать личного ассистента на ноутбуке, десктопе, домашнем сервере или VPS
- хранить долгую историю чатов, файлы и автоматизацию в одном workspace
- подключить одного и того же ассистента к нескольким каналам связи, которыми вы уже пользуетесь
- экспериментировать с tools, skills, browser automation и multi-agent routing

**Подходит хуже, если вам нужны:**

- hostile multi-tenant isolation на одном общем gateway
- consumer app без настройки и без эксплуатационной ответственности
- корпоративный compliance, SLA и vendor support из коробки

---

<a id="quick-start-setup-methods"></a>
## 2. Быстрый старт и способы установки

Если сделать только одну вещь, пусть это будет запуск локального dashboard до подключения внешних каналов.

### Системные требования

| Элемент | Рекомендация |
|---------|--------------|
| Runtime | Рекомендуется Node 24; минимум Node 22.16+ |
| ОС | macOS или Linux; для Windows рекомендуется WSL2 |
| Первый интерфейс | Dashboard / WebChat |
| Первый путь настройки | `openclaw onboard` |

### Быстрый старт (1 минута)

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
openclaw dashboard
```

### Способы установки

### Способ 1: официальный installer script

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
openclaw onboard --install-daemon
```

### Способ 2: npm / pnpm

```bash
npm install -g openclaw@latest
# или
pnpm add -g openclaw@latest
```

### Способ 3: Docker

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
./docker-setup.sh
```

### Способ 4: облачные деплои в один клик

| Платформа | Ссылка | Примечания |
|-----------|--------|------------|
| **OpenClaw Launch** | [1-Click Deploy](https://www.aigeamy.com/) | Официальный и самый быстрый старт |
| **Railway** | [Template](https://railway.com/deploy/openclaw) | Web-based setup wizard |
| **DigitalOcean** | [1-Click Deploy](https://marketplace.digitalocean.com/apps/openclaw) | Преднастроено и усилено по безопасности |
| **Render** | [render.yaml](https://docs.openclaw.ai/render) | Infrastructure as Code |
| **SimpleClaw** | [simpleclaw.com](https://www.simpleclaw.com/) | Развертывание меньше чем за минуту |
| **Zeabur** | [Template](https://zeabur.com/templates/VTZ4FX) | Docker deploy в один клик |
| **Northflank** | [Stack](https://northflank.com/stacks/deploy-openclaw) | Не нужен server-side terminal |
| **Lightning.AI** | [Environment](https://lightning.ai/lightning-ai/environments/openclaw) | Через браузер, без локального железа |
| **Coolify** | [Template](https://github.com/essamamdani/openclaw-coolify) | Self-hosted PaaS template |
| **Elestio** | [Open Source](https://elest.io/open-source/openclaw) | Полностью managed менее чем за 3 минуты |

### Сопоставимые продукты AI Agent

| # | Продукт | Сайт | Тип | Self-Host | Платформы сообщений |
|---|---------|------|-----|-----------|---------------------|
| 1 | **Hermes Agent** | [hermesagent.studio](https://hermesagent.studio/) | Автономный agent + messaging hub | Да | WhatsApp, Telegram, Slack, Discord и другие |
| 2 | **Multica** | [multica.uk](https://multica.uk/) | Многоканальная AI-автоматизация | Да | Мультиплатформенно |
| 3 | **GenericAgent** | [genericagent.org](https://www.genericagent.org/) | Agent workspace с контролем браузера, терминала, файловой системы и памяти | Не указано | Web workspace |
| 4 | **AutoGPT** | [agpt.co](https://agpt.co/) | Автономный агент задач | Да | API / web UI |
| 5 | **LangChain** | [langchain.com](https://www.langchain.com/) | Framework оркестрации LLM | Да | Любая платформа через custom integrations |
| 6 | **n8n** | [n8n.io](https://n8n.io/) | Автоматизация workflow + AI nodes | Да | Slack, Telegram, Discord и 400+ приложений |
| 7 | **AgentGPT** | [agentgpt.reworkd.ai](https://agentgpt.reworkd.ai/) | Browser-based autonomous agent | Да | Web UI |
| 8 | **CrewAI** | [crewai.com](https://www.crewai.com/) | Multi-agent collaboration по ролям | Да | API / custom integrations |
| 9 | **SuperAGI** | [superagi.com](https://superagi.com/) | Инфраструктура автономных agents | Да | Slack, Email, API |

### Чеклист первого часа

1. Запустите `openclaw onboard` и выберите QuickStart, если только вы уже не знаете точный config.
2. Выберите одного provider моделей и одну модель по умолчанию.
3. На первом запуске держите gateway local-only.
4. Откройте dashboard и убедитесь, что чат работает без внешних каналов.
5. После этого добавьте ровно один канал.
6. Перед удаленным доступом выполните `openclaw doctor` и `openclaw security audit`.

### Разумный порядок обучения

1. Сначала Dashboard или WebChat
2. Один provider моделей
3. Один канал
4. Аудит безопасности
5. skills и browser automation
6. Remote access, VPS или always-on deployment

---

<a id="install-paths"></a>
## 3. Пути установки

| Путь | Лучше всего подходит | Почему помогает | Ссылка |
|------|----------------------|-----------------|--------|
| CLI onboarding | Большинству разработчиков | Самый быстрый официальный путь; настраивает gateway, workspace, channels, daemon и skills | [Getting Started](https://docs.openclaw.ai/start/getting-started) / [Onboarding](https://docs.openclaw.ai/start/wizard) |
| Docker | VPS и более чистая изоляция runtime | Проще контейнеризовать runtime и чисто переустанавливать | [Docker](https://docs.openclaw.ai/install/docker) |
| Из исходников | Контрибьюторам и отладке | Полный `pnpm` build/watch workflow из основного repo | [openclaw/openclaw](https://github.com/openclaw/openclaw) |
| Nix | Воспроизводимым окружениям | Декларативная установка и обновления | [nix-openclaw](https://github.com/openclaw/nix-openclaw) |
| Путь приложения macOS | Сетапам с Apple-устройствами | Полезно, если важны voice, canvas и нативные платформенные возможности | [macOS Platform Docs](https://docs.openclaw.ai/platforms/macos) |

### Рекомендация

Для обычного разработчика ответ по умолчанию все тот же: установите через npm, запустите onboarding и проверьте все в dashboard, прежде чем двигаться к более амбициозным сценариям.

---

<a id="core-concepts-commands"></a>
## 4. Ключевые концепции и команды

### Концепции, важные в первый день

| Концепция | Что это значит | Почему важно |
|-----------|----------------|--------------|
| Gateway | Локальный control plane | Управляет config, sessions, channels, tools, dashboard и auth |
| Agent | Логическая идентичность ассистента | Позволяет разделять use cases, workspaces и model policies |
| Workspace | Файлы и prompts для agent | Здесь живут skills, заметки и артефакты задач |
| Channel | Интеграция мессенджера | Определяет, как пользователи достучатся до ассистента |
| Session | Контекст диалога | Управляет continuity памяти и routing behavior |
| Skill | Упакованная capability | Reusable prompt + files + scripts для типовых задач |
| Tool profile | Разрешенный набор возможностей | Один из главных рычагов безопасности и поведения |
| Model policy | Основная модель плюс fallback | Управляет качеством, стоимостью и безопасностью |

### Команды, которые стоит запомнить

| Задача | Команда |
|--------|---------|
| Запустить guided setup | `openclaw onboard` |
| Перенастроить позже | `openclaw configure` |
| Открыть browser dashboard | `openclaw dashboard` |
| Проверить здоровье и миграции | `openclaw doctor` |
| Аудит security posture | `openclaw security audit` |
| Глубокий security audit | `openclaw security audit --deep` |
| Добавить еще одного agent | `openclaw agents add <name>` |
| Посмотреть config | `openclaw config get <path>` |
| Обновить config | `openclaw config set <path> <value>` |
| Проверить auth/status моделей | `openclaw models status` |
| Быстрый локальный prompt | `openclaw agent --message "Ship checklist"` |

### Практические советы

- Используйте onboarding и `openclaw configure`, прежде чем вручную править много JSON.
- Рано создайте второго agent, если хотите отделить personal use от work automation.
- Проверяйте `openclaw models status`, когда provider выглядит как "настроен, но не работает".

---

<a id="channels-what-to-connect-first"></a>
## 5. Каналы: что подключать первым

Не подключайте пять каналов в первый день. Выберите surface, которая соответствует вашей реальной цели и терпимости к сложности setup.

| Канал | Лучший первый сценарий | Примечания | Docs |
|-------|------------------------|------------|------|
| WebChat | Самый быстрый smoke test | Не требует настройки стороннего bot; идеален для первой проверки | [WebChat](https://docs.openclaw.ai/web/webchat) |
| Telegram | Самый простой путь к внешнему bot | Отличный первый реальный канал для разработчиков | [Telegram](https://docs.openclaw.ai/channels/telegram) |
| WhatsApp | Ежедневный personal assistant | Очень полезен в реальной жизни, но держите DM policies жесткими | [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) |
| Slack | Команда или внутренний workflow | Сначала разберитесь с trust boundaries, потом расширяйте доступ к workspace | [Slack](https://docs.openclaw.ai/channels/slack) |
| Discord | Частный сервер или community experiments | Сначала ужесточите правила DM и групп | [Discord](https://docs.openclaw.ai/channels/discord) |
| Signal | Личное использование с фокусом на privacy | Дополнительная dependency, но стоит того, если вы уже живете в Signal | [Signal](https://docs.openclaw.ai/channels/signal) |

### Простое правило

- Нужен самый быстрый путь к успеху: начните с WebChat или Telegram.
- Нужен настоящий daily-driver: переходите в WhatsApp после того, как заработает dashboard.
- Нужна командная работа: сначала изучите безопасность и separation agents, потом используйте Slack или Discord.

---

<a id="deployment-choices"></a>
## 6. Варианты развертывания

| Сценарий | Рекомендуемый путь | Почему |
|----------|--------------------|--------|
| Первая оценка | Local CLI onboarding + dashboard | Минимальная сложность и самая простая отладка |
| Personal always-on assistant | Домашний сервер / Mac mini / Linux box + daemon | Стабильный daily-driver с локальным владением |
| Дешевый VPS | Docker | Более чистая граница хоста и простой redeploy |
| Воспроизводимая личная инфраструктура | Nix | Декларативный config и repeatable install |
| Удаленный доступ | Tailscale или SSH tunnel | Безопаснее, чем слепо открывать gateway в интернет |
| Несколько trust boundaries | Раздельные gateways и, желательно, разные OS users или hosts | OpenClaw не рассчитан на hostile multi-tenant isolation в одном gateway |

### Прочитайте это перед удаленным деплоем

Удаленный доступ — это то, что стоит добавлять после работающего local setup, а не до него. Самый частый failure mode — открыть мощного ассистента до того, как продуманы pairing rules, allowlists, tool profiles и границы между agents.

---

<a id="security-baseline"></a>
## 7. Базовый уровень безопасности

Это раздел, который многие списки "awesome" пропускают, хотя разработчикам он действительно нужен.

### Базовые правила

- Считайте входящие DMs, web content, shared chats и uploaded files недоверенным вводом.
- Пока вы изучаете систему, держите доступ по DM в режиме pairing или strict allowlist.
- Если бот может получать DMs более чем от одного человека, используйте `session.dmScope: "per-channel-peer"` или еще более строгий эквивалент.
- Групповые каналы держите mention-gated, если только нет явной причины поступить иначе.
- Начинайте с restrictive tool profile и расширяйте доступ только когда точно понимаете зачем.
- Для shared или non-main sessions предпочитайте sandboxing вместо надежды только на prompt discipline.
- Держите gateway local-only, пока осознанно не настроите remote access и auth.
- Регулярно запускайте `openclaw security audit`, а перед расширением exposure используйте `--deep`.
- Разделяйте personal и company trust boundaries на разные agents, а лучше и на разные gateways или hosts.

### Полезные ссылки по безопасности

- [Security Guide](https://docs.openclaw.ai/gateway/security)
- [Sandboxing](https://docs.openclaw.ai/gateway/sandboxing)
- [Remote Access](https://docs.openclaw.ai/gateway/remote)
- [Tailscale](https://docs.openclaw.ai/gateway/tailscale)
- [Doctor](https://docs.openclaw.ai/gateway/doctor)

---

<a id="official-docs-by-goal"></a>
## 8. Официальные документы по целям

| Цель | Лучшая ссылка |
|------|---------------|
| Первая установка | [Getting Started](https://docs.openclaw.ai/start/getting-started) |
| Guided setup | [Onboarding (CLI)](https://docs.openclaw.ai/start/wizard) |
| Browser-first testing | [Dashboard](https://docs.openclaw.ai/web/dashboard) |
| Configuration | [Configuration](https://docs.openclaw.ai/gateway/configuration) |
| Настройка моделей | [Models CLI](https://docs.openclaw.ai/concepts/models) |
| Обзор каналов | [Channels](https://docs.openclaw.ai/channels) |
| Skills | [Skills](https://docs.openclaw.ai/tools/skills) |
| Browser automation | [Browser Tool](https://docs.openclaw.ai/tools/browser) |
| Установка Docker | [Docker](https://docs.openclaw.ai/install/docker) |
| Усиление безопасности | [Security](https://docs.openclaw.ai/gateway/security) |
| Remote exposure | [Remote Access](https://docs.openclaw.ai/gateway/remote) |
| Remote access через Tailscale | [Tailscale](https://docs.openclaw.ai/gateway/tailscale) |
| Troubleshooting | [FAQ](https://docs.openclaw.ai/help/faq) |

### Рекомендуемый порядок чтения

1. Getting Started
2. Onboarding
3. Dashboard
4. Configuration
5. Одна doc по каналу
6. Security
7. Skills, browser automation и remote access

---

<a id="curated-ecosystem-links"></a>
## 9. Подборка ссылок экосистемы

Смотрите эти ссылки после того, как у вас уже есть working install. Они намного полезнее, когда официальный путь onboarding уже понятен.

### Официальные

| Ресурс | Почему важен |
|--------|--------------|
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | Главный codebase и авторитетный README |
| [docs.openclaw.ai](https://docs.openclaw.ai) | Официальный documentation hub |
| [openclaw/clawhub](https://github.com/openclaw/clawhub) | Официальный каталог skills и пакетов |
| [openclaw/nix-openclaw](https://github.com/openclaw/nix-openclaw) | Nix packaging для воспроизводимых установок |

### Сообщество

| Ресурс | Почему важен |
|--------|--------------|
| [essamamdani/openclaw-coolify](https://github.com/essamamdani/openclaw-coolify) | Template Coolify для self-hosted PaaS |
| [serhanekicii/openclaw-helm](https://github.com/serhanekicii/openclaw-helm) | Helm chart, если ваш деплой-мир — Kubernetes |
| [lunarpulse/openclaw-mcp-plugin](https://github.com/lunarpulse/openclaw-mcp-plugin) | Стартовая точка для MCP-oriented integrations |
| [centminmod/explain-openclaw](https://github.com/centminmod/explain-openclaw) | Глубокая техническая документация и заметки по деплою/безопасности |

---

<a id="common-mistakes"></a>
## 10. Частые ошибки

- Читать огромные таблицы хостинга до того, как заработал локальный chat
- Подключать слишком много каналов сразу и дебажить шум вместо ясного пути
- Считать shared tool-enabled agent безопасным multi-tenant приложением
- Открывать gateway наружу до локальной проверки pairing, allowlists и auth
- Смешивать personal и company trust boundaries в одном мощном runtime ассистента
- Ждать сильной локальной model performance на слабом железе без планирования
- Массово править config руками до того, как onboarding создал разумную базу

---

<a id="contributing"></a>
## 11. Как внести вклад

См. [CONTRIBUTING.ru.md](./CONTRIBUTING.ru.md).

При добавлении ссылок отдавайте приоритет ресурсам, которые помогают обычному разработчику хорошо сделать одну из этих задач:

- установить OpenClaw
- правильно его настроить
- разумно его защитить
- быстрее его отладить
- расширить его с реальной пользой для разработки

---

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

Список опубликован по лицензии CC0 1.0 Universal (Public Domain).
