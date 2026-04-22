# Awesome OpenClaw - Guide orienté développeurs

**Langues :** [English](README.md) | [简体中文](README.zh-CN.md) | [हिन्दी](README.hi.md) | [Español](README.es.md) | [العربية](README.ar.md) | **Français** | [বাংলা](README.bn.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Bahasa Indonesia](README.id.md)

[![Stars](https://img.shields.io/github/stars/openclaw/openclaw?style=flat&logo=github&label=Stars&color=gold)](https://github.com/openclaw/openclaw/stargazers)
[![Forks](https://img.shields.io/github/forks/openclaw/openclaw?style=flat&label=Forks&color=silver)](https://github.com/openclaw/openclaw/network/members)
[![Contributors](https://img.shields.io/github/contributors/openclaw/openclaw?label=Contributors&color=green)](https://github.com/openclaw/openclaw/graphs/contributors)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0 1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

Guide curé d'OpenClaw pensé pour les développeurs. Ce README privilégie la documentation officielle, l'ordre pratique de mise en route, les bases de sécurité et les liens d'écosystème durables plutôt que le battage, les tableaux de prix et les promesses marketing qui vieillissent vite.

---

## Table des matières

1. [Présentation du produit](#product-overview)
2. [Démarrage rapide et méthodes d'installation](#quick-start-setup-methods)
3. [Parcours d'installation](#install-paths)
4. [Concepts clés et commandes](#core-concepts-commands)
5. [Canaux : quoi connecter d'abord](#channels-what-to-connect-first)
6. [Choix de déploiement](#deployment-choices)
7. [Base de sécurité](#security-baseline)
8. [Documentation officielle par objectif](#official-docs-by-goal)
9. [Liens d'écosystème sélectionnés](#curated-ecosystem-links)
10. [Erreurs fréquentes](#common-mistakes)
11. [Contribuer](#contributing)

---

<a id="product-overview"></a>
## 1. Présentation du produit

**OpenClaw** est un assistant IA personnel que vous exécutez sur vos propres appareils. Au centre se trouve le **Gateway**, qui sert de plan de contrôle pour les agents, channels, sessions, tools, dashboard/web UI et accès à distance. Une bonne manière de le voir est la suivante : OpenClaw n'est pas "juste un bot", c'est un runtime d'assistant local-first qui peut vivre dans les surfaces de discussion que vous utilisez déjà.

### Ce qu'OpenClaw apporte concrètement aux développeurs

- Un Gateway local avec CLI, dashboard, WebChat et options d'accès distant
- Une messagerie multi-canale via WhatsApp, Telegram, Slack, Discord, WebChat et plus encore
- Plusieurs agents avec workspaces, sessions, bindings et politiques de modèle séparés
- Une configuration de modèles flexible avec providers hébergés, auth OAuth, API keys et chemins de modèles locaux
- Des skills, l'automatisation navigateur, des nodes, des cron jobs et d'autres workflows pilotés par des outils
- Un modèle de confiance d'assistant personnel, pas un modèle SaaS multi-tenant hostile

### Architecture de base (6 couches)

| Couche | Rôle |
|--------|------|
| **Gateway** | Plan de contrôle central : routage des messages, sessions, plugins et politique d'exécution des outils |
| **Channels** | Adaptateurs qui normalisent Telegram, WhatsApp, Discord et iMessage en messages standardisés |
| **Routing + Sessions** | Détermine quel agent traite quelle conversation |
| **Agent Runtime** | Traite le contexte, appelle les providers de modèles, diffuse les réponses et demande les outils |
| **Tools** | Capacités comme web fetch, contrôle du navigateur, exécution de commandes et appairage d'appareils |
| **Surfaces** | Points d'interaction comme apps de chat, dashboard web, barre de menu macOS et Live Canvas |

### Historique du nom

| Date | Nom | Raison |
|------|-----|--------|
| Nov. 2025 | **Clawdbot** | Nom d'origine au lancement |
| 27 janv. 2026 | **Moltbot** | Réclamation de marque d'Anthropic (similarité avec "Claude") |
| 30 janv. 2026 | **OpenClaw** | Rebranding final validé par la communauté |

### Quand c'est un bon choix / quand ce ne l'est pas

**Bon choix si vous voulez :**

- faire tourner un assistant personnel sur votre laptop, desktop, serveur maison ou VPS
- conserver historique de chat, fichiers et automatisations dans un même workspace
- connecter le même assistant à plusieurs canaux de messagerie déjà utilisés
- expérimenter avec tools, skills, automatisation navigateur ou routing multi-agent

**Moins adapté si vous avez besoin de :**

- isolation multi-tenant hostile sur un gateway partagé
- application grand public sans maintenance ni responsabilité d'exploitation
- conformité entreprise, SLA et support fournisseur prêts à l'emploi

---

<a id="quick-start-setup-methods"></a>
## 2. Démarrage rapide et méthodes d'installation

Si vous ne faites qu'une chose, faites fonctionner le dashboard local avant de connecter un canal externe.

### Configuration système

| Élément | Recommandation |
|---------|----------------|
| Runtime | Node 24 recommandé ; minimum Node 22.16+ |
| OS | macOS ou Linux ; sous Windows, WSL2 est recommandé |
| Première interface | Dashboard / WebChat |
| Premier flux d'installation | `openclaw onboard` |

### Démarrage rapide (1 minute)

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
openclaw dashboard
```

### Méthodes d'installation

### Méthode 1 : script d'installation officiel

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
openclaw onboard --install-daemon
```

### Méthode 2 : npm / pnpm

```bash
npm install -g openclaw@latest
# ou
pnpm add -g openclaw@latest
```

### Méthode 3 : Docker

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
./docker-setup.sh
```

### Méthode 4 : déploiements cloud en un clic

| Plateforme | Lien | Notes |
|------------|------|-------|
| **OpenClaw Launch** | [1-Click Deploy](https://www.aigeamy.com/) | Officiel, le plus rapide pour démarrer |
| **Railway** | [Template](https://railway.com/deploy/openclaw) | Assistant d'installation web |
| **DigitalOcean** | [1-Click Deploy](https://marketplace.digitalocean.com/apps/openclaw) | Préconfiguré et renforcé côté sécurité |
| **Render** | [render.yaml](https://docs.openclaw.ai/render) | Infrastructure as Code |
| **SimpleClaw** | [simpleclaw.com](https://www.simpleclaw.com/) | Déploiement en moins d'une minute |
| **Zeabur** | [Template](https://zeabur.com/templates/VTZ4FX) | Déploiement Docker en un clic |
| **Northflank** | [Stack](https://northflank.com/stacks/deploy-openclaw) | Pas besoin de terminal serveur |
| **Lightning.AI** | [Environment](https://lightning.ai/lightning-ai/environments/openclaw) | Basé navigateur, sans matériel local |
| **Coolify** | [Template](https://github.com/essamamdani/openclaw-coolify) | Template PaaS auto-hébergé |
| **Elestio** | [Open Source](https://elest.io/open-source/openclaw) | Entièrement géré en moins de 3 minutes |

### Produits AI Agent comparables

| # | Produit | Site | Type | Self-Host | Plateformes de messagerie |
|---|---------|------|------|-----------|---------------------------|
| 1 | **Hermes Agent** | [hermesagent.studio](https://hermesagent.studio/) | Agent autonome + hub de messagerie | Oui | WhatsApp, Telegram, Slack, Discord et plus |
| 2 | **Multica** | [multica.uk](https://multica.uk/) | Automatisation IA multi-canale | Oui | Multi-plateforme |
| 3 | **GenericAgent** | [genericagent.org](https://www.genericagent.org/) | Workspace agent avec contrôle du navigateur, du terminal, du système de fichiers et de la mémoire | Non précisé | Workspace web |
| 4 | **AutoGPT** | [agpt.co](https://agpt.co/) | Agent autonome de tâches | Oui | API / web UI |
| 5 | **LangChain** | [langchain.com](https://www.langchain.com/) | Framework d'orchestration LLM | Oui | Toute plateforme via intégrations personnalisées |
| 6 | **n8n** | [n8n.io](https://n8n.io/) | Automatisation de workflows + nœuds IA | Oui | Slack, Telegram, Discord et plus de 400 apps |
| 7 | **AgentGPT** | [agentgpt.reworkd.ai](https://agentgpt.reworkd.ai/) | Agent autonome orienté navigateur | Oui | Web UI |
| 8 | **CrewAI** | [crewai.com](https://www.crewai.com/) | Collaboration multi-agent par rôles | Oui | API / intégrations personnalisées |
| 9 | **SuperAGI** | [superagi.com](https://superagi.com/) | Infrastructure pour agents autonomes | Oui | Slack, Email, API |

### Checklist de la première heure

1. Lancez `openclaw onboard` et choisissez QuickStart sauf si vous savez déjà exactement quel config vous voulez.
2. Choisissez un provider de modèles et un modèle par défaut.
3. Gardez le gateway en local uniquement lors du premier démarrage.
4. Ouvrez le dashboard et vérifiez que le chat fonctionne sans canal externe.
5. Ajoutez ensuite exactement un canal.
6. Exécutez `openclaw doctor` et `openclaw security audit` avant toute exposition distante.

### Ordre d'apprentissage raisonnable

1. Dashboard ou WebChat d'abord
2. Un provider de modèles
3. Un canal
4. Audit de sécurité
5. Skills et automatisation navigateur
6. Accès distant, VPS ou déploiement always-on

---

<a id="install-paths"></a>
## 3. Parcours d'installation

| Parcours | Idéal pour | Pourquoi c'est utile | Lien |
|----------|------------|----------------------|------|
| Onboarding CLI | La plupart des développeurs | Voie officielle la plus rapide ; configure gateway, workspace, channels, daemon et skills | [Getting Started](https://docs.openclaw.ai/start/getting-started) / [Onboarding](https://docs.openclaw.ai/start/wizard) |
| Docker | VPS, isolation plus propre du runtime | Plus simple à contenir et à redéployer proprement | [Docker](https://docs.openclaw.ai/install/docker) |
| Depuis le source | Contributeurs et débogage | Workflow complet de build et watch avec `pnpm` depuis le dépôt principal | [openclaw/openclaw](https://github.com/openclaw/openclaw) |
| Nix | Environnements reproductibles | Setup déclaratif et mises à jour reproductibles | [nix-openclaw](https://github.com/openclaw/nix-openclaw) |
| Parcours app macOS | Configurations centrées sur Apple | Utile si la voix, canvas et les fonctions natives vous importent particulièrement | [macOS Platform Docs](https://docs.openclaw.ai/platforms/macos) |

### Recommandation

Pour un développeur classique, la réponse par défaut reste : installez via npm, lancez l'onboarding, puis validez tout dans le dashboard avant de viser quelque chose de plus ambitieux.

---

<a id="core-concepts-commands"></a>
## 4. Concepts clés et commandes

### Concepts importants dès le premier jour

| Concept | Signification | Pourquoi c'est important |
|---------|---------------|--------------------------|
| Gateway | Le plan de contrôle local | Gère config, sessions, channels, tools, dashboard et auth |
| Agent | Une identité logique d'assistant | Permet de séparer cas d'usage, workspaces et politiques de modèle |
| Workspace | Fichiers et prompts d'un agent | Là où vivent skills, notes et artefacts de tâches |
| Channel | Une intégration de messagerie | Détermine comment les utilisateurs atteignent l'assistant |
| Session | Un contexte de conversation | Contrôle la continuité mémoire et le routing |
| Skill | Une capacité empaquetée | Prompt + fichiers + scripts réutilisables |
| Tool profile | Ensemble de capacités autorisées | L'un des plus gros leviers de sécurité et de comportement |
| Model policy | Modèle principal et fallback | Contrôle qualité, coût et posture de sécurité |

### Commandes à retenir tôt

| Tâche | Commande |
|------|----------|
| Lancer le setup guidé | `openclaw onboard` |
| Reconfigurer ensuite | `openclaw configure` |
| Ouvrir le dashboard navigateur | `openclaw dashboard` |
| Inspecter santé et migrations | `openclaw doctor` |
| Auditer la posture de sécurité | `openclaw security audit` |
| Audit de sécurité approfondi | `openclaw security audit --deep` |
| Ajouter un autre agent | `openclaw agents add <name>` |
| Inspecter la config | `openclaw config get <path>` |
| Mettre à jour la config | `openclaw config set <path> <value>` |
| Vérifier auth ou état des modèles | `openclaw models status` |
| Prompt local rapide | `openclaw agent --message "Ship checklist"` |

### Conseils pratiques

- Utilisez onboarding et `openclaw configure` avant d'éditer beaucoup de JSON à la main.
- Créez tôt un deuxième agent si vous voulez séparer usage personnel et automatisation du travail.
- Vérifiez `openclaw models status` chaque fois qu'un provider semble "configuré mais ne fonctionne pas".

---

<a id="channels-what-to-connect-first"></a>
## 5. Canaux : quoi connecter d'abord

Ne connectez pas cinq canaux le premier jour. Choisissez la surface qui correspond à votre objectif réel et à votre tolérance à la complexité du setup.

| Canal | Meilleur premier usage | Notes | Docs |
|-------|------------------------|-------|------|
| WebChat | Test de fumée le plus rapide | Pas de configuration de bot tiers ; idéal pour la première validation | [WebChat](https://docs.openclaw.ai/web/webchat) |
| Telegram | Le chemin le plus simple pour un bot externe | Très bon premier vrai canal pour les développeurs | [Telegram](https://docs.openclaw.ai/channels/telegram) |
| WhatsApp | Assistant personnel quotidien | Très utile en conditions réelles, mais gardez des politiques DM strictes | [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) |
| Slack | Équipe ou workflow interne | Comprenez les limites de confiance avant d'ouvrir largement le workspace | [Slack](https://docs.openclaw.ai/channels/slack) |
| Discord | Serveur privé ou expérimentation communautaire | Resserrez d'abord les règles DM et de groupe | [Discord](https://docs.openclaw.ai/channels/discord) |
| Signal | Usage personnel orienté vie privée | Dépendance supplémentaire, utile si vous vivez déjà dans Signal | [Signal](https://docs.openclaw.ai/channels/signal) |

### Règle pratique

- Vous voulez réussir le plus vite possible : commencez par WebChat ou Telegram.
- Vous voulez un vrai assistant du quotidien : passez à WhatsApp quand le dashboard fonctionne.
- Vous voulez un usage équipe : apprenez d'abord sécurité et séparation des agents, puis utilisez Slack ou Discord.

---

<a id="deployment-choices"></a>
## 6. Choix de déploiement

| Scénario | Parcours recommandé | Pourquoi |
|----------|---------------------|---------|
| Première évaluation | Onboarding CLI local + dashboard | Complexité minimale et débogage plus simple |
| Assistant personnel always-on | Serveur maison / Mac mini / box Linux + daemon | Configuration stable du quotidien avec propriété locale |
| VPS économique | Docker | Frontière hôte plus propre et redéploiement simplifié |
| Infra personnelle reproductible | Nix | Config déclarative et installations répétables |
| Accès distant | Tailscale ou tunnel SSH | Plus sûr qu'exposer le gateway directement à internet |
| Limites de confiance multiples | Gateways séparés et, idéalement, utilisateurs OS ou hôtes distincts | OpenClaw n'est pas conçu pour une isolation multi-tenant hostile sur un gateway partagé |

### À lire avant un déploiement distant

L'accès distant est une capacité à ajouter après un setup local fonctionnel, pas avant. Le mode d'échec classique consiste à exposer un assistant puissant avant d'avoir réfléchi aux pairing rules, allowlists, tool profiles et limites entre agents.

---

<a id="security-baseline"></a>
## 7. Base de sécurité

C'est la section que beaucoup de listes "awesome" sautent alors que les développeurs en ont réellement besoin.

### Règles de base

- Traitez les DMs entrants, le contenu web, les chats partagés et les fichiers téléversés comme des entrées non fiables.
- Gardez l'accès DM en mode pairing ou allowlist stricte tant que vous apprenez encore le système.
- Si plus d'une personne peut envoyer des DMs au bot, utilisez `session.dmScope: "per-channel-peer"` ou un équivalent plus strict.
- Gardez les canaux de groupe déclenchés par mention, sauf raison explicite contraire.
- Commencez avec un tool profile restrictif et n'élargissez l'accès que lorsque vous savez exactement pourquoi.
- Pour les sessions partagées ou non principales, préférez sandboxing plutôt que la seule discipline des prompts.
- Gardez le gateway local-only tant que l'accès distant et l'auth ne sont pas configurés volontairement.
- Lancez `openclaw security audit` régulièrement et utilisez `--deep` avant d'élargir l'exposition.
- Séparez les limites de confiance personnelles et professionnelles dans des agents distincts, et si possible sur des gateways ou hôtes distincts.

### Liens sécurité à forte valeur

- [Security Guide](https://docs.openclaw.ai/gateway/security)
- [Sandboxing](https://docs.openclaw.ai/gateway/sandboxing)
- [Remote Access](https://docs.openclaw.ai/gateway/remote)
- [Tailscale](https://docs.openclaw.ai/gateway/tailscale)
- [Doctor](https://docs.openclaw.ai/gateway/doctor)

---

<a id="official-docs-by-goal"></a>
## 8. Documentation officielle par objectif

| Objectif | Meilleur lien |
|----------|---------------|
| Première installation | [Getting Started](https://docs.openclaw.ai/start/getting-started) |
| Setup guidé | [Onboarding (CLI)](https://docs.openclaw.ai/start/wizard) |
| Test orienté navigateur | [Dashboard](https://docs.openclaw.ai/web/dashboard) |
| Configuration | [Configuration](https://docs.openclaw.ai/gateway/configuration) |
| Setup des modèles | [Models CLI](https://docs.openclaw.ai/concepts/models) |
| Vue d'ensemble des canaux | [Channels](https://docs.openclaw.ai/channels) |
| Skills | [Skills](https://docs.openclaw.ai/tools/skills) |
| Automatisation navigateur | [Browser Tool](https://docs.openclaw.ai/tools/browser) |
| Installation Docker | [Docker](https://docs.openclaw.ai/install/docker) |
| Renforcement sécurité | [Security](https://docs.openclaw.ai/gateway/security) |
| Exposition distante | [Remote Access](https://docs.openclaw.ai/gateway/remote) |
| Accès distant via Tailscale | [Tailscale](https://docs.openclaw.ai/gateway/tailscale) |
| Dépannage | [FAQ](https://docs.openclaw.ai/help/faq) |

### Ordre de lecture conseillé

1. Getting Started
2. Onboarding
3. Dashboard
4. Configuration
5. Une doc de canal
6. Security
7. Skills, automatisation navigateur et accès distant

---

<a id="curated-ecosystem-links"></a>
## 9. Liens d'écosystème sélectionnés

Consultez ces liens après avoir une installation réellement fonctionnelle. Ils deviennent beaucoup plus utiles une fois le parcours d'onboarding officiel déjà clair pour vous.

### Officiel

| Ressource | Pourquoi c'est important |
|-----------|--------------------------|
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | Dépôt principal et README de référence |
| [docs.openclaw.ai](https://docs.openclaw.ai) | Hub officiel de documentation |
| [openclaw/clawhub](https://github.com/openclaw/clawhub) | Répertoire officiel des skills et catalogue de packages |
| [openclaw/nix-openclaw](https://github.com/openclaw/nix-openclaw) | Packaging Nix pour installations reproductibles |

### Communauté

| Ressource | Pourquoi c'est important |
|-----------|--------------------------|
| [essamamdani/openclaw-coolify](https://github.com/essamamdani/openclaw-coolify) | Template Coolify pour utilisateurs de PaaS auto-hébergé |
| [serhanekicii/openclaw-helm](https://github.com/serhanekicii/openclaw-helm) | Helm chart si votre univers de déploiement est Kubernetes |
| [lunarpulse/openclaw-mcp-plugin](https://github.com/lunarpulse/openclaw-mcp-plugin) | Point de départ orienté intégration MCP |
| [centminmod/explain-openclaw](https://github.com/centminmod/explain-openclaw) | Documentation technique approfondie et notes de déploiement ou sécurité |

---

<a id="common-mistakes"></a>
## 10. Erreurs fréquentes

- Lire d'énormes tableaux d'hébergement avant d'avoir un chat local fonctionnel
- Connecter trop de canaux d'un coup et déboguer le bruit au lieu d'un chemin clair
- Traiter un agent partagé doté d'outils comme une app multi-tenant sûre
- Exposer le gateway à distance avant d'avoir testé pairing, allowlists et auth en local
- Mélanger limites de confiance personnelles et professionnelles dans un même runtime puissant
- Attendre de bonnes performances locales sur du matériel limité sans planification
- Modifier massivement la config à la main avant qu'onboarding n'ait créé une base saine

---

<a id="contributing"></a>
## 11. Contribuer

Voir [CONTRIBUTING.fr.md](./CONTRIBUTING.fr.md).

Quand vous ajoutez des liens, privilégiez les ressources qui aident un développeur normal à bien faire l'un de ces travaux :

- installer OpenClaw
- le configurer correctement
- le sécuriser raisonnablement
- le déboguer plus vite
- l'étendre avec un vrai gain pour le développement

---

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

Cette liste est publiée sous CC0 1.0 Universal (domaine public).
