# Awesome OpenClaw - Guia voltado para desenvolvedores

**Idiomas:** [English](README.md) | [简体中文](README.zh-CN.md) | [हिन्दी](README.hi.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Français](README.fr.md) | [বাংলা](README.bn.md) | **Português** | [Русский](README.ru.md) | [Bahasa Indonesia](README.id.md)

[![Stars](https://img.shields.io/github/stars/openclaw/openclaw?style=flat&logo=github&label=Stars&color=gold)](https://github.com/openclaw/openclaw/stargazers)
[![Forks](https://img.shields.io/github/forks/openclaw/openclaw?style=flat&label=Forks&color=silver)](https://github.com/openclaw/openclaw/network/members)
[![Contributors](https://img.shields.io/github/contributors/openclaw/openclaw?label=Contributors&color=green)](https://github.com/openclaw/openclaw/graphs/contributors)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0 1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

Guia curado de OpenClaw com foco em desenvolvedores. Este README prioriza documentação oficial, ordem prática de setup, linha de base de segurança e links duráveis do ecossistema em vez de hype, tabelas de preço e promessas de marketing que envelhecem rápido.

---

## Sumário

1. [Visão geral do produto](#product-overview)
2. [Início rápido e métodos de instalação](#quick-start-setup-methods)
3. [Caminhos de instalação](#install-paths)
4. [Conceitos e comandos principais](#core-concepts-commands)
5. [Canais: o que conectar primeiro](#channels-what-to-connect-first)
6. [Escolhas de implantação](#deployment-choices)
7. [Linha de base de segurança](#security-baseline)
8. [Documentação oficial por objetivo](#official-docs-by-goal)
9. [Links selecionados do ecossistema](#curated-ecosystem-links)
10. [Erros comuns](#common-mistakes)
11. [Contribuição](#contributing)

---

<a id="product-overview"></a>
## 1. Visão geral do produto

**OpenClaw** é um assistente pessoal de IA que você executa nos seus próprios dispositivos. No centro está o **Gateway**, que atua como plano de controle para agents, channels, sessions, tools, dashboard/web UI e acesso remoto. Uma boa forma de pensar nisso é: OpenClaw não é "apenas um bot"; é um runtime de assistente local-first que pode viver dentro das superfícies de chat que você já usa.

### O que o OpenClaw realmente entrega aos desenvolvedores

- Um Gateway local com CLI, dashboard, WebChat e opções de acesso remoto
- Mensageria multicanal em superfícies como WhatsApp, Telegram, Slack, Discord, WebChat e mais
- Vários agents com workspaces, sessions, bindings e políticas de modelo separadas
- Configuração flexível de modelos com providers hospedados, auth via OAuth, API keys e caminhos para modelos locais
- skills, automação de navegador, nodes, cron jobs e outros workflows guiados por ferramentas
- Um modelo de confiança de assistente pessoal, e não um modelo SaaS multi-tenant hostil

### Arquitetura principal (6 camadas)

| Camada | Propósito |
|--------|-----------|
| **Gateway** | Plano de controle central - roteamento de mensagens, sessions, plugins e política de execução de ferramentas |
| **Channels** | Adaptadores que normalizam Telegram, WhatsApp, Discord e iMessage em formatos de mensagem padrão |
| **Routing + Sessions** | Determina qual agent lida com cada conversa |
| **Agent Runtime** | Processa contexto, chama providers de modelo, transmite respostas e solicita ferramentas |
| **Tools** | Capacidades como web fetch, controle do navegador, execução de comandos e pareamento de dispositivos |
| **Surfaces** | Pontos de interação como apps de chat, dashboard web, barra de menu do macOS e Live Canvas |

### Histórico do nome

| Data | Nome | Motivo |
|------|------|--------|
| Nov 2025 | **Clawdbot** | Nome original no lançamento |
| 27 jan 2026 | **Moltbot** | Reclamação de marca da Anthropic (semelhança com "Claude") |
| 30 jan 2026 | **OpenClaw** | Rebranding final decidido pela comunidade |

### Quando faz sentido / quando não faz

**Faz sentido se você quer:**

- rodar um assistente pessoal no laptop, desktop, servidor doméstico ou VPS
- manter histórico longo de chat, arquivos e automações dentro de um workspace
- conectar o mesmo assistente a vários canais de mensagem que você já usa
- experimentar com tools, skills, automação de navegador ou routing multi-agent

**Não é a melhor opção se você precisa de:**

- isolamento multi-tenant hostil em um gateway compartilhado
- um app de consumo sem manutenção e sem responsabilidade operacional
- compliance empresarial, SLA e suporte do fornecedor prontos de fábrica

---

<a id="quick-start-setup-methods"></a>
## 2. Início rápido e métodos de instalação

Se você fizer só uma coisa, faça o dashboard local funcionar antes de conectar qualquer canal externo.

### Requisitos do sistema

| Item | Recomendação |
|------|--------------|
| Runtime | Node 24 recomendado; mínimo Node 22.16+ |
| SO | macOS ou Linux; no Windows, o caminho recomendado é WSL2 |
| Primeira interface | Dashboard / WebChat |
| Primeiro fluxo de setup | `openclaw onboard` |

### Início rápido (1 minuto)

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
openclaw dashboard
```

### Métodos de instalação

### Método 1: script oficial de instalação

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
openclaw onboard --install-daemon
```

### Método 2: npm / pnpm

```bash
npm install -g openclaw@latest
# ou
pnpm add -g openclaw@latest
```

### Método 3: Docker

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
./docker-setup.sh
```

### Método 4: deploys em nuvem com um clique

| Plataforma | Link | Notas |
|------------|------|-------|
| **OpenClaw Launch** | [1-Click Deploy](https://www.aigeamy.com/) | Oficial, o caminho mais rápido para começar |
| **Railway** | [Template](https://railway.com/deploy/openclaw) | Assistente de setup baseado na web |
| **DigitalOcean** | [1-Click Deploy](https://marketplace.digitalocean.com/apps/openclaw) | Pré-configurado e endurecido em segurança |
| **Render** | [render.yaml](https://docs.openclaw.ai/render) | Infraestrutura como código |
| **SimpleClaw** | [simpleclaw.com](https://www.simpleclaw.com/) | Deploy em menos de 1 minuto |
| **Zeabur** | [Template](https://zeabur.com/templates/VTZ4FX) | Deploy Docker com um clique |
| **Northflank** | [Stack](https://northflank.com/stacks/deploy-openclaw) | Não exige terminal no servidor |
| **Lightning.AI** | [Environment](https://lightning.ai/lightning-ai/environments/openclaw) | Baseado em navegador, sem hardware local |
| **Coolify** | [Template](https://github.com/essamamdani/openclaw-coolify) | Template PaaS self-hosted |
| **Elestio** | [Open Source](https://elest.io/open-source/openclaw) | Totalmente gerenciado em menos de 3 minutos |

### Produtos de AI Agent comparáveis

| # | Produto | Site | Tipo | Self-Host | Plataformas de mensagem |
|---|---------|------|------|-----------|-------------------------|
| 1 | **Hermes Agent** | [hermesagent.studio](https://hermesagent.studio/) | Agente autônomo + hub de mensageria | Sim | WhatsApp, Telegram, Slack, Discord e mais |
| 2 | **Multica** | [multica.uk](https://multica.uk/) | Automação de IA multicanal | Sim | Multiplataforma |
| 3 | **GenericAgent** | [genericagent.org](https://www.genericagent.org/) | Workspace de agente com controle de navegador, terminal, sistema de arquivos e memória | Não especificado | Workspace web |
| 4 | **AutoGPT** | [agpt.co](https://agpt.co/) | Agente autônomo de tarefas | Sim | API / web UI |
| 5 | **LangChain** | [langchain.com](https://www.langchain.com/) | Framework de orquestração de LLM | Sim | Qualquer plataforma via integrações customizadas |
| 6 | **n8n** | [n8n.io](https://n8n.io/) | Automação de workflow + nós de IA | Sim | Slack, Telegram, Discord e mais de 400 apps |
| 7 | **AgentGPT** | [agentgpt.reworkd.ai](https://agentgpt.reworkd.ai/) | Agente autônomo no navegador | Sim | Web UI |
| 8 | **CrewAI** | [crewai.com](https://www.crewai.com/) | Colaboração multi-agent por papéis | Sim | API / integrações personalizadas |
| 9 | **SuperAGI** | [superagi.com](https://superagi.com/) | Infraestrutura para agentes autônomos | Sim | Slack, Email, API |

### Checklist da primeira hora

1. Rode `openclaw onboard` e escolha QuickStart, a menos que você já saiba exatamente o config que quer.
2. Escolha um provider de modelos e um modelo padrão.
3. Mantenha o gateway local-only na primeira execução.
4. Abra o dashboard e confirme que dá para conversar sem nenhum canal externo.
5. Depois disso, adicione exatamente um canal.
6. Execute `openclaw doctor` e `openclaw security audit` antes de expor qualquer coisa remotamente.

### Ordem de aprendizado sensata

1. Dashboard ou WebChat primeiro
2. Um provider de modelos
3. Um canal
4. Auditoria de segurança
5. skills e automação de navegador
6. Acesso remoto, VPS ou deploy always-on

---

<a id="install-paths"></a>
## 3. Caminhos de instalação

| Caminho | Melhor para | Por que ajuda | Link |
|---------|-------------|---------------|------|
| Onboarding via CLI | A maioria dos desenvolvedores | Caminho oficial mais rápido; configura gateway, workspace, channels, daemon e skills | [Getting Started](https://docs.openclaw.ai/start/getting-started) / [Onboarding](https://docs.openclaw.ai/start/wizard) |
| Docker | VPS e isolamento mais limpo do runtime | Facilita conter o runtime e redeploy limpo | [Docker](https://docs.openclaw.ai/install/docker) |
| Do código-fonte | Contribuidores e debugging | Workflow completo de build e watch com `pnpm` a partir do repo principal | [openclaw/openclaw](https://github.com/openclaw/openclaw) |
| Nix | Ambientes reproduzíveis | Setup declarativo e atualizações repetíveis | [nix-openclaw](https://github.com/openclaw/nix-openclaw) |
| Caminho do app macOS | Setup centrado em dispositivos Apple | Útil se voz, canvas e recursos nativos forem prioridade | [macOS Platform Docs](https://docs.openclaw.ai/platforms/macos) |

### Recomendação

Para um desenvolvedor comum, a resposta padrão continua sendo: instale via npm, execute o onboarding e valide tudo no dashboard antes de tentar algo mais ambicioso.

---

<a id="core-concepts-commands"></a>
## 4. Conceitos e comandos principais

### Conceitos importantes no primeiro dia

| Conceito | O que significa | Por que importa |
|----------|-----------------|-----------------|
| Gateway | O plano de controle local | Controla config, sessions, channels, tools, dashboard e auth |
| Agent | Uma identidade lógica de assistente | Permite separar casos de uso, workspaces e políticas de modelo |
| Workspace | Arquivos e prompts de um agent | Onde vivem skills, notas e artefatos de tarefa |
| Channel | Uma integração de mensageria | Define como os usuários chegam ao assistente |
| Session | Um contexto de conversa | Controla continuidade de memória e routing |
| Skill | Uma capacidade empacotada | Prompt + arquivos + scripts reutilizáveis |
| Tool profile | Conjunto de capacidades permitidas | Uma das maiores alavancas de segurança e comportamento |
| Model policy | Modelo principal com fallback | Controla qualidade, custo e postura de segurança |

### Comandos que valem decorar cedo

| Tarefa | Comando |
|--------|---------|
| Rodar setup guiado | `openclaw onboard` |
| Reconfigurar depois | `openclaw configure` |
| Abrir dashboard no navegador | `openclaw dashboard` |
| Inspecionar saúde e migrações | `openclaw doctor` |
| Auditar postura de segurança | `openclaw security audit` |
| Auditoria profunda de segurança | `openclaw security audit --deep` |
| Adicionar outro agent | `openclaw agents add <name>` |
| Inspecionar config | `openclaw config get <path>` |
| Atualizar config | `openclaw config set <path> <value>` |
| Ver auth/status do modelo | `openclaw models status` |
| Prompt local rápido | `openclaw agent --message "Ship checklist"` |

### Conselhos práticos

- Use onboarding e `openclaw configure` antes de editar muito JSON na mão.
- Crie cedo um segundo agent se quiser separar uso pessoal de automação de trabalho.
- Confira `openclaw models status` sempre que um provider parecer "configurado, mas não funcionando".

---

<a id="channels-what-to-connect-first"></a>
## 5. Canais: o que conectar primeiro

Não conecte cinco canais no primeiro dia. Escolha a surface que combina com seu objetivo real e com a sua tolerância ao setup.

| Canal | Melhor primeiro uso | Notas | Docs |
|-------|---------------------|-------|------|
| WebChat | Smoke test mais rápido | Não precisa de setup de bot de terceiros; ideal para a primeira validação | [WebChat](https://docs.openclaw.ai/web/webchat) |
| Telegram | Caminho mais fácil para um bot externo | Bom primeiro canal real para desenvolvedores | [Telegram](https://docs.openclaw.ai/channels/telegram) |
| WhatsApp | Assistente pessoal do dia a dia | Excelente para uso real, mas mantenha políticas de DM apertadas | [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) |
| Slack | Time ou workflow interno | Entenda os limites de confiança antes de abrir acesso amplo ao workspace | [Slack](https://docs.openclaw.ai/channels/slack) |
| Discord | Servidor privado ou experimentos de comunidade | Aperte as regras de DM e grupos antes de abrir | [Discord](https://docs.openclaw.ai/channels/discord) |
| Signal | Uso pessoal voltado à privacidade | Dependência extra, mas vale a pena se você já vive no Signal | [Signal](https://docs.openclaw.ai/channels/signal) |

### Regra prática

- Quer o caminho mais rápido para sucesso: comece com WebChat ou Telegram.
- Quer um daily-driver real: migre para WhatsApp quando o dashboard já estiver funcionando.
- Quer uso em equipe: aprenda primeiro segurança e separação de agents, depois use Slack ou Discord.

---

<a id="deployment-choices"></a>
## 6. Escolhas de implantação

| Cenário | Caminho recomendado | Por quê |
|---------|---------------------|--------|
| Primeira avaliação | Onboarding local via CLI + dashboard | Menor complexidade e debugging mais fácil |
| Assistente pessoal always-on | Servidor doméstico / Mac mini / Linux box + daemon | Setup estável de uso diário com controle local |
| VPS barato | Docker | Fronteira do host mais limpa e redeploy mais simples |
| Infra pessoal reproduzível | Nix | Config declarativa e instalações repetíveis |
| Acesso remoto | Tailscale ou túnel SSH | Mais seguro do que expor o gateway diretamente à internet |
| Múltiplas fronteiras de confiança | Gateways separados e, idealmente, usuários de SO ou hosts distintos | OpenClaw não foi projetado para isolamento multi-tenant hostil em um único gateway |

### Leia isto antes de implantar remotamente

Acesso remoto é algo para adicionar depois que o setup local estiver funcionando, não antes. O modo de falha mais comum é expor um assistente poderoso antes de pensar em pairing rules, allowlists, tool profiles e fronteiras entre agents.

---

<a id="security-baseline"></a>
## 7. Linha de base de segurança

Esta é a seção que muitas listas "awesome" pulam e da qual os desenvolvedores realmente precisam.

### Regras básicas

- Trate DMs recebidas, conteúdo web, chats compartilhados e arquivos enviados como entrada não confiável.
- Mantenha o acesso por DM em modo pairing ou allowlist estrita enquanto ainda aprende o sistema.
- Se mais de uma pessoa puder enviar DM ao bot, use `session.dmScope: "per-channel-peer"` ou equivalente mais rígido.
- Mantenha canais em grupo ativados por menção, a menos que exista um motivo claro para não fazer isso.
- Comece com um tool profile restritivo e só amplie o acesso quando souber exatamente por quê.
- Para sessions compartilhadas ou não principais, prefira sandboxing em vez de confiar apenas em disciplina de prompts.
- Mantenha o gateway local-only até configurar intencionalmente acesso remoto e auth.
- Rode `openclaw security audit` com regularidade e use `--deep` antes de ampliar a exposição.
- Separe fronteiras de confiança pessoais e da empresa em agents distintos e, de preferência, em gateways ou hosts diferentes.

### Links de segurança de alto valor

- [Security Guide](https://docs.openclaw.ai/gateway/security)
- [Sandboxing](https://docs.openclaw.ai/gateway/sandboxing)
- [Remote Access](https://docs.openclaw.ai/gateway/remote)
- [Tailscale](https://docs.openclaw.ai/gateway/tailscale)
- [Doctor](https://docs.openclaw.ai/gateway/doctor)

---

<a id="official-docs-by-goal"></a>
## 8. Documentação oficial por objetivo

| Objetivo | Melhor link |
|----------|-------------|
| Primeira instalação | [Getting Started](https://docs.openclaw.ai/start/getting-started) |
| Setup guiado | [Onboarding (CLI)](https://docs.openclaw.ai/start/wizard) |
| Teste browser-first | [Dashboard](https://docs.openclaw.ai/web/dashboard) |
| Configuração | [Configuration](https://docs.openclaw.ai/gateway/configuration) |
| Setup de modelos | [Models CLI](https://docs.openclaw.ai/concepts/models) |
| Visão geral de canais | [Channels](https://docs.openclaw.ai/channels) |
| Skills | [Skills](https://docs.openclaw.ai/tools/skills) |
| Automação de navegador | [Browser Tool](https://docs.openclaw.ai/tools/browser) |
| Instalação via Docker | [Docker](https://docs.openclaw.ai/install/docker) |
| Endurecimento de segurança | [Security](https://docs.openclaw.ai/gateway/security) |
| Exposição remota | [Remote Access](https://docs.openclaw.ai/gateway/remote) |
| Acesso remoto via Tailscale | [Tailscale](https://docs.openclaw.ai/gateway/tailscale) |
| Solução de problemas | [FAQ](https://docs.openclaw.ai/help/faq) |

### Ordem sugerida de leitura

1. Getting Started
2. Onboarding
3. Dashboard
4. Configuration
5. Um doc de canal
6. Security
7. Skills, automação de navegador e acesso remoto

---

<a id="curated-ecosystem-links"></a>
## 9. Links selecionados do ecossistema

Veja estes links depois que você tiver uma instalação realmente funcional. Eles ficam muito mais úteis quando o caminho oficial de onboarding já faz sentido para você.

### Oficial

| Recurso | Por que importa |
|---------|-----------------|
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | Codebase principal e README de referência |
| [docs.openclaw.ai](https://docs.openclaw.ai) | Hub oficial de documentação |
| [openclaw/clawhub](https://github.com/openclaw/clawhub) | Diretório oficial de skills e catálogo de pacotes |
| [openclaw/nix-openclaw](https://github.com/openclaw/nix-openclaw) | Empacotamento Nix para instalações reproduzíveis |

### Comunidade

| Recurso | Por que importa |
|---------|-----------------|
| [essamamdani/openclaw-coolify](https://github.com/essamamdani/openclaw-coolify) | Template Coolify para usuários de PaaS self-hosted |
| [serhanekicii/openclaw-helm](https://github.com/serhanekicii/openclaw-helm) | Helm chart se o seu mundo de deploy é Kubernetes |
| [lunarpulse/openclaw-mcp-plugin](https://github.com/lunarpulse/openclaw-mcp-plugin) | Ponto de partida para integração orientada a MCP |
| [centminmod/explain-openclaw](https://github.com/centminmod/explain-openclaw) | Documentação técnica profunda e notas de deploy ou segurança |

---

<a id="common-mistakes"></a>
## 10. Erros comuns

- Ler tabelas enormes de hosting antes de ter um chat local funcionando
- Conectar canais demais de uma vez e acabar depurando ruído em vez de um caminho claro
- Tratar um agent compartilhado com tools como se fosse um app multi-tenant seguro
- Expor o gateway remotamente antes de validar pairing, allowlists e auth em local
- Misturar fronteiras de confiança pessoais e da empresa em um único runtime poderoso
- Esperar forte desempenho de modelos locais em hardware limitado sem planejamento
- Editar muita config manualmente antes de o onboarding criar uma base saudável

---

<a id="contributing"></a>
## 11. Contribuição

Veja [CONTRIBUTING.pt.md](./CONTRIBUTING.pt.md).

Ao adicionar links, prefira recursos que ajudem um desenvolvedor comum a fazer bem um destes trabalhos:

- instalar o OpenClaw
- configurá-lo corretamente
- protegê-lo com bom senso
- depurá-lo mais rápido
- estendê-lo com ganho real de desenvolvimento

---

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

Esta lista é publicada sob CC0 1.0 Universal (Domínio Público).
