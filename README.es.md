# Awesome OpenClaw - Guía centrada en desarrolladores

**Idiomas:** [English](README.md) | [简体中文](README.zh-CN.md) | [हिन्दी](README.hi.md) | **Español** | [العربية](README.ar.md) | [Français](README.fr.md) | [বাংলা](README.bn.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Bahasa Indonesia](README.id.md)

[![Stars](https://img.shields.io/github/stars/openclaw/openclaw?style=flat&logo=github&label=Stars&color=gold)](https://github.com/openclaw/openclaw/stargazers)
[![Forks](https://img.shields.io/github/forks/openclaw/openclaw?style=flat&label=Forks&color=silver)](https://github.com/openclaw/openclaw/network/members)
[![Contributors](https://img.shields.io/github/contributors/openclaw/openclaw?label=Contributors&color=green)](https://github.com/openclaw/openclaw/graphs/contributors)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0 1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

Guía curada de OpenClaw pensada para desarrolladores. Este README prioriza la documentación oficial, el orden práctico de puesta en marcha, las bases de seguridad y los enlaces duraderos del ecosistema por encima del hype, las tablas de precios y las afirmaciones de marketing que envejecen rápido.

---

## Tabla de contenidos

1. [Resumen del producto](#product-overview)
2. [Inicio rápido y métodos de instalación](#quick-start-setup-methods)
3. [Rutas de instalación](#install-paths)
4. [Conceptos y comandos clave](#core-concepts-commands)
5. [Canales: qué conectar primero](#channels-what-to-connect-first)
6. [Opciones de despliegue](#deployment-choices)
7. [Línea base de seguridad](#security-baseline)
8. [Documentación oficial por objetivo](#official-docs-by-goal)
9. [Enlaces del ecosistema seleccionados](#curated-ecosystem-links)
10. [Errores comunes](#common-mistakes)
11. [Cómo contribuir](#contributing)

---

<a id="product-overview"></a>
## 1. Resumen del producto

**OpenClaw** es un asistente personal de IA que ejecutas en tus propios dispositivos. En el centro está el **Gateway**, que actúa como plano de control para agents, channels, sessions, tools, dashboard/web UI y acceso remoto. Una buena forma de entenderlo es esta: OpenClaw no es "solo un bot"; es un runtime local-first para asistentes que puede vivir dentro de las superficies de chat que ya usas.

### Qué ofrece realmente OpenClaw a los desarrolladores

- Un Gateway local con CLI, dashboard, WebChat y opciones de acceso remoto
- Mensajería multicanal en superficies como WhatsApp, Telegram, Slack, Discord, WebChat y más
- Varios agents con workspaces, sessions, bindings y políticas de modelo separadas
- Configuración flexible de modelos con providers alojados, autenticación basada en OAuth, API keys y rutas a modelos locales
- Skills, automatización de navegador, nodes, cron jobs y otros flujos impulsados por herramientas
- Un modelo de confianza de asistente personal, no un modelo SaaS multi-tenant hostil

### Arquitectura principal (6 capas)

| Capa | Propósito |
|------|-----------|
| **Gateway** | Plano de control central: enrutamiento de mensajes, sesiones, plugins y política de ejecución de herramientas |
| **Channels** | Adaptadores que normalizan Telegram, WhatsApp, Discord e iMessage a formatos de mensaje estándar |
| **Routing + Sessions** | Determina qué agent maneja cada conversación |
| **Agent Runtime** | Procesa contexto, llama a proveedores de modelos, transmite respuestas y solicita herramientas |
| **Tools** | Capacidades como web fetch, control del navegador, ejecución de comandos y emparejamiento de dispositivos |
| **Surfaces** | Puntos de interacción como apps de chat, dashboard web, barra de menú de macOS y Live Canvas |

### Historial del nombre

| Fecha | Nombre | Motivo |
|-------|--------|--------|
| Nov 2025 | **Clawdbot** | Nombre original en el lanzamiento |
| 27 ene 2026 | **Moltbot** | Reclamo de marca por parte de Anthropic (similitud con "Claude") |
| 30 ene 2026 | **OpenClaw** | Cambio final de marca decidido por la comunidad |

### Cuándo encaja bien / cuándo no

**Encaja bien si quieres:**

- ejecutar un asistente personal en tu portátil, sobremesa, servidor casero o VPS
- mantener historial de chat, archivos y automatizaciones de larga duración en un solo workspace
- conectar el mismo asistente a varios canales de mensajería que ya utilizas
- experimentar con tools, skills, automatización del navegador o routing multi-agent

**No es la mejor opción si necesitas:**

- aislamiento multi-tenant hostil en un gateway compartido
- una app de consumo sin mantenimiento ni responsabilidad operativa
- cumplimiento empresarial, SLA y soporte del proveedor de serie

---

<a id="quick-start-setup-methods"></a>
## 2. Inicio rápido y métodos de instalación

Si solo haces una cosa, haz que el dashboard local funcione antes de conectar cualquier canal externo.

### Requisitos del sistema

| Elemento | Recomendación |
|----------|---------------|
| Runtime | Node 24 recomendado; mínimo Node 22.16+ |
| SO | macOS o Linux; en Windows se recomienda WSL2 |
| Primera interfaz | Dashboard / WebChat |
| Primer flujo de configuración | `openclaw onboard` |

### Inicio rápido (1 minuto)

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
openclaw dashboard
```

### Métodos de instalación

### Método 1: script instalador oficial

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
openclaw onboard --install-daemon
```

### Método 2: npm / pnpm

```bash
npm install -g openclaw@latest
# o
pnpm add -g openclaw@latest
```

### Método 3: Docker

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
./docker-setup.sh
```

### Método 4: despliegues cloud con un clic

| Plataforma | Enlace | Notas |
|------------|--------|-------|
| **OpenClaw Launch** | [1-Click Deploy](https://www.aigeamy.com/) | Oficial, la vía más rápida para empezar |
| **Railway** | [Template](https://railway.com/deploy/openclaw) | Asistente de instalación basado en web |
| **DigitalOcean** | [1-Click Deploy](https://marketplace.digitalocean.com/apps/openclaw) | Endurecido en seguridad y preconfigurado |
| **Render** | [render.yaml](https://docs.openclaw.ai/render) | Infraestructura como código |
| **SimpleClaw** | [simpleclaw.com](https://www.simpleclaw.com/) | Despliegue en menos de 1 minuto |
| **Zeabur** | [Template](https://zeabur.com/templates/VTZ4FX) | Despliegue Docker con un clic |
| **Northflank** | [Stack](https://northflank.com/stacks/deploy-openclaw) | No requiere terminal en el servidor |
| **Lightning.AI** | [Environment](https://lightning.ai/lightning-ai/environments/openclaw) | Basado en navegador, sin hardware local |
| **Coolify** | [Template](https://github.com/essamamdani/openclaw-coolify) | Plantilla PaaS autoalojada |
| **Elestio** | [Open Source](https://elest.io/open-source/openclaw) | Gestionado por completo en menos de 3 minutos |

### Productos de AI Agent comparables

| # | Producto | Sitio web | Tipo | Self-Host | Plataformas de mensajería |
|---|----------|-----------|------|-----------|---------------------------|
| 1 | **Hermes Agent** | [hermesagent.studio](https://hermesagent.studio/) | Agente autónomo + hub de mensajería | Sí | WhatsApp, Telegram, Slack, Discord y más |
| 2 | **Multica** | [multica.uk](https://multica.uk/) | Automatización AI multicanal | Sí | Multiplataforma |
| 3 | **GenericAgent** | [genericagent.org](https://www.genericagent.org/) | Workspace de agente con control de navegador, terminal, sistema de archivos y memoria | No especificado | Workspace web |
| 4 | **AutoGPT** | [agpt.co](https://agpt.co/) | Agente autónomo de tareas | Sí | API / web UI |
| 5 | **LangChain** | [langchain.com](https://www.langchain.com/) | Framework de orquestación LLM | Sí | Cualquiera (mediante integraciones personalizadas) |
| 6 | **n8n** | [n8n.io](https://n8n.io/) | Automatización de flujos + nodos AI | Sí | Slack, Telegram, Discord y más de 400 apps |
| 7 | **AgentGPT** | [agentgpt.reworkd.ai](https://agentgpt.reworkd.ai/) | Agente autónomo basado en navegador | Sí | Web UI |
| 8 | **CrewAI** | [crewai.com](https://www.crewai.com/) | Colaboración multi-agent por roles | Sí | API / integraciones personalizadas |
| 9 | **SuperAGI** | [superagi.com](https://superagi.com/) | Infraestructura para agentes autónomos | Sí | Slack, Email, API |

### Lista de verificación de la primera hora

1. Ejecuta `openclaw onboard` y elige QuickStart salvo que ya tengas claro el config exacto que quieres.
2. Elige un provider de modelos y un modelo por defecto.
3. Mantén el gateway solo en local durante la primera ejecución.
4. Abre el dashboard y verifica que puedes chatear sin ningún canal externo.
5. Añade exactamente un canal después de eso.
6. Ejecuta `openclaw doctor` y `openclaw security audit` antes de exponer nada en remoto.

### Un orden de aprendizaje sensato

1. Primero Dashboard o WebChat
2. Un provider de modelos
3. Un canal
4. Auditoría de seguridad
5. Skills y automatización del navegador
6. Acceso remoto, VPS o despliegue always-on

---

<a id="install-paths"></a>
## 3. Rutas de instalación

| Ruta | Mejor para | Por qué ayuda | Enlace |
|------|------------|---------------|--------|
| Onboarding por CLI | La mayoría de los desarrolladores | Ruta oficial más rápida; configura gateway, workspace, channels, daemon y skills | [Getting Started](https://docs.openclaw.ai/start/getting-started) / [Onboarding](https://docs.openclaw.ai/start/wizard) |
| Docker | VPS, aislamiento más limpio del runtime | Facilita contener el runtime y volver a desplegarlo con limpieza | [Docker](https://docs.openclaw.ai/install/docker) |
| Desde el código fuente | Contribuidores y depuradores | Flujo completo de build y watch con `pnpm` desde el repo principal | [openclaw/openclaw](https://github.com/openclaw/openclaw) |
| Nix | Entornos reproducibles | Instalación y actualizaciones declarativas | [nix-openclaw](https://github.com/openclaw/nix-openclaw) |
| Ruta de app macOS | Entornos centrados en dispositivos Apple | Útil si te importan especialmente la voz, canvas y las capacidades nativas de la plataforma | [macOS Platform Docs](https://docs.openclaw.ai/platforms/macos) |

### Recomendación

Para un desarrollador normal, la respuesta por defecto sigue siendo: instala desde npm, ejecuta el onboarding y valida todo en el dashboard antes de intentar algo más ambicioso.

---

<a id="core-concepts-commands"></a>
## 4. Conceptos y comandos clave

### Conceptos que importan desde el primer día

| Concepto | Qué significa | Por qué importa |
|----------|---------------|-----------------|
| Gateway | El plano de control local | Gestiona config, sessions, channels, tools, dashboard y auth |
| Agent | Una identidad lógica de asistente | Permite separar casos de uso, workspaces y políticas de modelo |
| Workspace | Archivos y prompts de un agent | Donde viven skills, notas y artefactos de tareas |
| Channel | Una integración de mensajería | Determina cómo los usuarios llegan al asistente |
| Session | El contexto de una conversación | Controla continuidad de memoria y comportamiento de routing |
| Skill | Una capacidad empaquetada | Prompt + archivos + scripts reutilizables para tareas comunes |
| Tool profile | Conjunto de capacidades permitidas | Uno de los mayores palancas de seguridad y comportamiento |
| Model policy | Modelo principal más fallback | Controla calidad, coste y postura de seguridad de herramientas |

### Comandos que conviene memorizar pronto

| Tarea | Comando |
|------|---------|
| Ejecutar configuración guiada | `openclaw onboard` |
| Reconfigurar después | `openclaw configure` |
| Abrir el dashboard en el navegador | `openclaw dashboard` |
| Inspeccionar salud y migraciones | `openclaw doctor` |
| Auditar postura de seguridad | `openclaw security audit` |
| Auditoría profunda de seguridad | `openclaw security audit --deep` |
| Añadir otro agent | `openclaw agents add <name>` |
| Inspeccionar config | `openclaw config get <path>` |
| Actualizar config | `openclaw config set <path> <value>` |
| Revisar auth o estado del modelo | `openclaw models status` |
| Prompt local rápido | `openclaw agent --message "Ship checklist"` |

### Consejos prácticos

- Usa onboarding y `openclaw configure` antes de editar a mano mucho JSON.
- Crea pronto un segundo agent si quieres separar el uso personal de la automatización del trabajo.
- Revisa `openclaw models status` siempre que un provider parezca "configurado pero sin funcionar".

---

<a id="channels-what-to-connect-first"></a>
## 5. Canales: qué conectar primero

No conectes cinco canales el primer día. Elige la superficie que mejor encaje con tu objetivo real y tu tolerancia a la complejidad de setup.

| Canal | Mejor primer uso | Notas | Docs |
|-------|------------------|-------|------|
| WebChat | Prueba de humo más rápida | No necesita configuración de bots de terceros; ideal para la primera validación | [WebChat](https://docs.openclaw.ai/web/webchat) |
| Telegram | La vía más sencilla para un bot externo | Buen primer canal real para desarrolladores | [Telegram](https://docs.openclaw.ai/channels/telegram) |
| WhatsApp | Asistente personal diario | Excelente para uso real, pero mantén estrictas las políticas de DM | [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) |
| Slack | Equipo o flujo interno | Aprende primero los límites de confianza antes de abrir acceso amplio al workspace | [Slack](https://docs.openclaw.ai/channels/slack) |
| Discord | Servidor privado o experimentos de comunidad | Endurece las reglas de DM y grupos antes de abrirlo | [Discord](https://docs.openclaw.ai/channels/discord) |
| Signal | Uso personal orientado a la privacidad | Añade una dependencia extra, pero merece la pena si ya vives en Signal | [Signal](https://docs.openclaw.ai/channels/signal) |

### Regla práctica útil

- ¿Quieres el camino más rápido al éxito? Empieza con WebChat o Telegram.
- ¿Quieres un asistente de uso diario? Pasa a WhatsApp cuando el dashboard ya funcione.
- ¿Quieres uso de equipo? Aprende primero seguridad y separación entre agents, y después usa Slack o Discord.

---

<a id="deployment-choices"></a>
## 6. Opciones de despliegue

| Escenario | Ruta recomendada | Por qué |
|-----------|------------------|---------|
| Primera evaluación | Onboarding local por CLI + dashboard | Menor complejidad y depuración más fácil |
| Asistente personal always-on | Servidor casero / Mac mini / caja Linux + daemon | Configuración estable para el día a día con propiedad local |
| VPS barato | Docker | Límite de host más limpio y redeploy más sencillo |
| Infra personal reproducible | Nix | Config declarativa e instalaciones repetibles |
| Acceso remoto | Tailscale o túnel SSH | Más seguro que exponer el gateway ciegamente a internet |
| Múltiples límites de confianza | Gateways separados y, si es posible, usuarios de SO o hosts separados | OpenClaw no está diseñado para aislamiento multi-tenant hostil en un solo gateway compartido |

### Lee esto antes de desplegar en remoto

El acceso remoto es algo que debes añadir después del setup local, no antes. El modo de fallo más común es exponer un asistente potente antes de pensar bien en reglas de pairing, allowlists, tool profiles y límites entre agents.

---

<a id="security-baseline"></a>
## 7. Línea base de seguridad

Esta es la sección que muchas listas "awesome" se saltan y que los desarrolladores sí necesitan.

### Reglas base

- Trata los DMs entrantes, el contenido web, los chats compartidos y los archivos subidos como entrada no confiable.
- Mantén el acceso por DM en modo pairing o allowlist estricta mientras aún aprendes el sistema.
- Si más de una persona puede enviar DMs al bot, usa `session.dmScope: "per-channel-peer"` o un equivalente más estricto.
- Mantén los canales grupales activados por mención, salvo que tengas un motivo concreto para no hacerlo.
- Empieza con un tool profile restrictivo y amplía el acceso solo cuando sepas exactamente por qué.
- Para sesiones compartidas o no principales, prioriza sandboxing en lugar de confiar solo en disciplina de prompts.
- Mantén el gateway solo en local hasta que configures de forma intencional el acceso remoto y la auth.
- Ejecuta `openclaw security audit` con regularidad y usa `--deep` cuando estés a punto de ampliar la exposición.
- Separa los límites de confianza personales y de empresa en agents distintos y, preferiblemente, en gateways o hosts diferentes.

### Enlaces de seguridad de alto valor

- [Security Guide](https://docs.openclaw.ai/gateway/security)
- [Sandboxing](https://docs.openclaw.ai/gateway/sandboxing)
- [Remote Access](https://docs.openclaw.ai/gateway/remote)
- [Tailscale](https://docs.openclaw.ai/gateway/tailscale)
- [Doctor](https://docs.openclaw.ai/gateway/doctor)

---

<a id="official-docs-by-goal"></a>
## 8. Documentación oficial por objetivo

| Objetivo | Mejor enlace |
|----------|--------------|
| Primera instalación | [Getting Started](https://docs.openclaw.ai/start/getting-started) |
| Configuración guiada | [Onboarding (CLI)](https://docs.openclaw.ai/start/wizard) |
| Prueba browser-first | [Dashboard](https://docs.openclaw.ai/web/dashboard) |
| Configuración | [Configuration](https://docs.openclaw.ai/gateway/configuration) |
| Setup de modelos | [Models CLI](https://docs.openclaw.ai/concepts/models) |
| Vista general de canales | [Channels](https://docs.openclaw.ai/channels) |
| Skills | [Skills](https://docs.openclaw.ai/tools/skills) |
| Automatización del navegador | [Browser Tool](https://docs.openclaw.ai/tools/browser) |
| Instalación con Docker | [Docker](https://docs.openclaw.ai/install/docker) |
| Endurecimiento de seguridad | [Security](https://docs.openclaw.ai/gateway/security) |
| Exposición remota | [Remote Access](https://docs.openclaw.ai/gateway/remote) |
| Acceso remoto con Tailscale | [Tailscale](https://docs.openclaw.ai/gateway/tailscale) |
| Solución de problemas | [FAQ](https://docs.openclaw.ai/help/faq) |

### Orden sugerido de lectura

1. Getting Started
2. Onboarding
3. Dashboard
4. Configuration
5. Un documento de canal
6. Security
7. Skills, automatización del navegador y acceso remoto

---

<a id="curated-ecosystem-links"></a>
## 9. Enlaces del ecosistema seleccionados

Revisa estos enlaces después de tener una instalación funcionando. Son mucho más útiles cuando la ruta oficial de onboarding ya te resulta clara.

### Oficial

| Recurso | Por qué importa |
|---------|-----------------|
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | Repositorio principal y README de referencia |
| [docs.openclaw.ai](https://docs.openclaw.ai) | Centro oficial de documentación |
| [openclaw/clawhub](https://github.com/openclaw/clawhub) | Directorio oficial de skills y catálogo de paquetes |
| [openclaw/nix-openclaw](https://github.com/openclaw/nix-openclaw) | Empaquetado Nix para instalaciones reproducibles |

### Comunidad

| Recurso | Por qué importa |
|---------|-----------------|
| [essamamdani/openclaw-coolify](https://github.com/essamamdani/openclaw-coolify) | Plantilla Coolify para usuarios de PaaS autoalojado |
| [serhanekicii/openclaw-helm](https://github.com/serhanekicii/openclaw-helm) | Helm chart si tu mundo de despliegue es Kubernetes |
| [lunarpulse/openclaw-mcp-plugin](https://github.com/lunarpulse/openclaw-mcp-plugin) | Punto de partida orientado a integraciones MCP |
| [centminmod/explain-openclaw](https://github.com/centminmod/explain-openclaw) | Documentación técnica profunda y notas de despliegue o seguridad |

---

<a id="common-mistakes"></a>
## 10. Errores comunes

- Leer tablas gigantes de hosting antes de tener funcionando el chat local
- Conectar demasiados canales a la vez y terminar depurando ruido en vez de una ruta clara
- Tratar un agent compartido con tools como si fuera una app multi-tenant segura
- Exponer el gateway en remoto antes de probar pairing, allowlists y auth en local
- Mezclar límites de confianza personales y de empresa en un solo runtime potente de asistente
- Esperar buen rendimiento de modelos locales en hardware modesto sin planificarlo
- Editar mucha config a mano antes de que onboarding cree una base razonable

---

<a id="contributing"></a>
## 11. Cómo contribuir

Consulta [CONTRIBUTING.es.md](./CONTRIBUTING.es.md).

Al añadir enlaces, prioriza recursos que ayuden a un desarrollador normal a hacer bien alguno de estos trabajos:

- instalar OpenClaw
- configurarlo correctamente
- asegurarlo con criterio
- depurarlo más rápido
- extenderlo con un beneficio real para el desarrollo

---

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

Esta lista se publica bajo CC0 1.0 Universal (Dominio público).
