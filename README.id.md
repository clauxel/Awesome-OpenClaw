# Awesome OpenClaw - Panduan berfokus pada pengembang

**Bahasa:** [English](README.md) | [简体中文](README.zh-CN.md) | [हिन्दी](README.hi.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Français](README.fr.md) | [বাংলা](README.bn.md) | [Português](README.pt.md) | [Русский](README.ru.md) | **Bahasa Indonesia**

[![Stars](https://img.shields.io/github/stars/openclaw/openclaw?style=flat&logo=github&label=Stars&color=gold)](https://github.com/openclaw/openclaw/stargazers)
[![Forks](https://img.shields.io/github/forks/openclaw/openclaw?style=flat&label=Forks&color=silver)](https://github.com/openclaw/openclaw/network/members)
[![Contributors](https://img.shields.io/github/contributors/openclaw/openclaw?label=Contributors&color=green)](https://github.com/openclaw/openclaw/graphs/contributors)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0 1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

Ini adalah panduan OpenClaw yang dikurasi dengan fokus pada pengembang. README ini memprioritaskan dokumentasi resmi, urutan setup yang praktis, baseline keamanan, dan tautan ekosistem yang tahan lama dibanding hype, tabel harga, dan klaim pemasaran yang cepat usang.

---

## Daftar Isi

1. [Gambaran produk](#product-overview)
2. [Mulai cepat dan metode instalasi](#quick-start-setup-methods)
3. [Jalur instalasi](#install-paths)
4. [Konsep inti dan perintah](#core-concepts-commands)
5. [Channel: apa yang harus dihubungkan lebih dulu](#channels-what-to-connect-first)
6. [Pilihan deployment](#deployment-choices)
7. [Baseline keamanan](#security-baseline)
8. [Dokumentasi resmi berdasarkan tujuan](#official-docs-by-goal)
9. [Tautan ekosistem terpilih](#curated-ecosystem-links)
10. [Kesalahan umum](#common-mistakes)
11. [Kontribusi](#contributing)

---

<a id="product-overview"></a>
## 1. Gambaran produk

**OpenClaw** adalah asisten AI pribadi yang Anda jalankan di perangkat milik Anda sendiri. Di pusatnya ada **Gateway**, yang bertindak sebagai control plane untuk agents, channels, sessions, tools, dashboard/web UI, dan akses jarak jauh. Cara yang kuat untuk memahaminya adalah: OpenClaw bukan "sekadar bot"; ini adalah runtime asisten local-first yang dapat hidup di permukaan chat yang sudah Anda gunakan.

### Apa yang sebenarnya diberikan OpenClaw kepada pengembang

- Gateway lokal dengan CLI, dashboard, WebChat, dan opsi akses jarak jauh
- Messaging multi-channel melalui WhatsApp, Telegram, Slack, Discord, WebChat, dan lainnya
- Banyak agents dengan workspace, session, binding, dan model policy yang terpisah
- Setup model yang fleksibel dengan hosted providers, auth berbasis OAuth, API key, dan path model lokal
- skills, browser automation, nodes, cron jobs, dan workflow lain yang digerakkan oleh tool
- Model kepercayaan asisten pribadi, bukan model keamanan SaaS multi-tenant yang hostile

### Arsitektur inti (6 lapisan)

| Lapisan | Tujuan |
|---------|--------|
| **Gateway** | Control plane pusat - routing pesan, sessions, plugins, dan kebijakan eksekusi tool |
| **Channels** | Adapter yang menormalkan Telegram, WhatsApp, Discord, dan iMessage menjadi bentuk pesan standar |
| **Routing + Sessions** | Menentukan agent mana yang menangani percakapan tertentu |
| **Agent Runtime** | Memproses konteks, memanggil provider model, men-stream respons, dan meminta tool |
| **Tools** | Kapabilitas seperti web fetch, kontrol browser, eksekusi perintah, dan pairing perangkat |
| **Surfaces** | Titik interaksi seperti aplikasi chat, web dashboard, bilah menu macOS, dan Live Canvas |

### Riwayat nama

| Tanggal | Nama | Alasan |
|---------|------|--------|
| Nov 2025 | **Clawdbot** | Nama asli saat peluncuran |
| 27 Jan 2026 | **Moltbot** | Keluhan merek dagang dari Anthropic karena kemiripan dengan "Claude" |
| 30 Jan 2026 | **OpenClaw** | Rebrand final melalui voting komunitas |

### Cocok untuk siapa / kurang cocok untuk siapa

**Cocok jika Anda ingin:**

- menjalankan asisten pribadi di laptop, desktop, server rumahan, atau VPS
- menyimpan chat history jangka panjang, file, dan automasi di satu workspace
- menghubungkan asisten yang sama ke beberapa channel pesan yang sudah Anda gunakan
- bereksperimen dengan tools, skills, browser automation, atau multi-agent routing

**Kurang cocok jika Anda membutuhkan:**

- isolasi multi-tenant yang hostile di satu gateway bersama
- aplikasi konsumen tanpa setup dan tanpa tanggung jawab operasional
- compliance enterprise, SLA, dan dukungan vendor langsung dari awal

---

<a id="quick-start-setup-methods"></a>
## 2. Mulai cepat dan metode instalasi

Jika Anda hanya melakukan satu hal, pastikan dashboard lokal berfungsi sebelum menghubungkan channel eksternal apa pun.

### Kebutuhan sistem

| Item | Rekomendasi |
|------|-------------|
| Runtime | Node 24 direkomendasikan; minimum Node 22.16+ |
| OS | macOS atau Linux; untuk Windows disarankan melalui WSL2 |
| Antarmuka pertama | Dashboard / WebChat |
| Alur setup pertama | `openclaw onboard` |

### Mulai cepat (1 menit)

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
openclaw dashboard
```

### Metode instalasi

### Metode 1: script installer resmi

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
openclaw onboard --install-daemon
```

### Metode 2: npm / pnpm

```bash
npm install -g openclaw@latest
# atau
pnpm add -g openclaw@latest
```

### Metode 3: Docker

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
./docker-setup.sh
```

### Metode 4: deploy cloud sekali klik

| Platform | Tautan | Catatan |
|----------|--------|---------|
| **OpenClaw Launch** | [1-Click Deploy](https://www.aigeamy.com/) | Resmi dan tercepat untuk memulai |
| **Railway** | [Template](https://railway.com/deploy/openclaw) | Wizard setup berbasis web |
| **DigitalOcean** | [1-Click Deploy](https://marketplace.digitalocean.com/apps/openclaw) | Sudah dikonfigurasi dan diperkuat keamanannya |
| **Render** | [render.yaml](https://docs.openclaw.ai/render) | Infrastruktur sebagai kode |
| **SimpleClaw** | [simpleclaw.com](https://www.simpleclaw.com/) | Deploy kurang dari 1 menit |
| **Zeabur** | [Template](https://zeabur.com/templates/VTZ4FX) | Deploy Docker sekali klik |
| **Northflank** | [Stack](https://northflank.com/stacks/deploy-openclaw) | Tidak perlu terminal server |
| **Lightning.AI** | [Environment](https://lightning.ai/lightning-ai/environments/openclaw) | Berbasis browser, tanpa hardware lokal |
| **Coolify** | [Template](https://github.com/essamamdani/openclaw-coolify) | Template PaaS self-hosted |
| **Elestio** | [Open Source](https://elest.io/open-source/openclaw) | Fully managed dalam kurang dari 3 menit |

### Produk AI Agent yang sebanding

| # | Produk | Situs | Tipe | Self-Host | Platform pesan |
|---|--------|-------|------|-----------|----------------|
| 1 | **Hermes Agent** | [hermesagent.studio](https://hermesagent.studio/) | Agen otonom + messaging hub | Ya | WhatsApp, Telegram, Slack, Discord, dan lainnya |
| 2 | **Multica** | [multica.uk](https://multica.uk/) | Otomasi AI multi-channel | Ya | Multi-platform |
| 3 | **GenericAgent** | [genericagent.org](https://www.genericagent.org/) | Workspace agen dengan kontrol browser, terminal, filesystem, dan memori | Tidak disebutkan | Workspace web |
| 4 | **AutoGPT** | [agpt.co](https://agpt.co/) | Agen tugas otonom | Ya | API / web UI |
| 5 | **LangChain** | [langchain.com](https://www.langchain.com/) | Framework orkestrasi LLM | Ya | Apa pun via custom integrations |
| 6 | **n8n** | [n8n.io](https://n8n.io/) | Otomasi workflow + node AI | Ya | Slack, Telegram, Discord, dan 400+ aplikasi |
| 7 | **AgentGPT** | [agentgpt.reworkd.ai](https://agentgpt.reworkd.ai/) | Agen otonom berbasis browser | Ya | Web UI |
| 8 | **CrewAI** | [crewai.com](https://www.crewai.com/) | Kolaborasi multi-agent berbasis peran | Ya | API / custom integrations |
| 9 | **SuperAGI** | [superagi.com](https://superagi.com/) | Infrastruktur agen otonom | Ya | Slack, Email, API |

### Checklist satu jam pertama

1. Jalankan `openclaw onboard` dan pilih QuickStart kecuali Anda sudah tahu config yang tepat.
2. Pilih satu provider model dan satu model default.
3. Biarkan gateway tetap local-only pada run pertama.
4. Buka dashboard dan pastikan Anda bisa chat tanpa channel eksternal.
5. Setelah itu tambahkan tepat satu channel.
6. Jalankan `openclaw doctor` dan `openclaw security audit` sebelum mengekspos apa pun secara remote.

### Urutan belajar yang masuk akal

1. Dashboard atau WebChat dulu
2. Satu provider model
3. Satu channel
4. Audit keamanan
5. skills dan browser automation
6. Akses remote, VPS, atau deployment always-on

---

<a id="install-paths"></a>
## 3. Jalur instalasi

| Jalur | Paling cocok untuk | Kenapa membantu | Tautan |
|-------|--------------------|-----------------|--------|
| CLI onboarding | Sebagian besar pengembang | Jalur resmi tercepat; mengatur gateway, workspace, channels, daemon, dan skills | [Getting Started](https://docs.openclaw.ai/start/getting-started) / [Onboarding](https://docs.openclaw.ai/start/wizard) |
| Docker | VPS dan isolasi runtime yang lebih bersih | Lebih mudah mengurung runtime dan redeploy dengan rapi | [Docker](https://docs.openclaw.ai/install/docker) |
| Dari source | Kontributor dan debugger | Workflow build/watch `pnpm` penuh dari repo utama | [openclaw/openclaw](https://github.com/openclaw/openclaw) |
| Nix | Lingkungan yang reproducible | Setup deklaratif dan update yang berulang | [nix-openclaw](https://github.com/openclaw/nix-openclaw) |
| Jalur aplikasi macOS | Setup yang berat di perangkat Apple | Berguna jika voice, canvas, dan fitur native platform penting bagi Anda | [macOS Platform Docs](https://docs.openclaw.ai/platforms/macos) |

### Rekomendasi

Untuk pengembang biasa, jawaban defaultnya tetap: install dari npm, jalankan onboarding, lalu validasi semuanya di dashboard sebelum mencoba hal yang lebih ambisius.

---

<a id="core-concepts-commands"></a>
## 4. Konsep inti dan perintah

### Konsep yang penting di hari pertama

| Konsep | Artinya | Kenapa penting |
|--------|---------|----------------|
| Gateway | Control plane lokal | Mengelola config, sessions, channels, tools, dashboard, dan auth |
| Agent | Identitas asisten logis | Memungkinkan pemisahan use case, workspace, dan model policy |
| Workspace | File dan prompt untuk agent | Di sinilah skills, catatan, dan artefak tugas berada |
| Channel | Integrasi messaging | Menentukan bagaimana pengguna menjangkau asisten |
| Session | Konteks percakapan | Mengatur kesinambungan memori dan routing behavior |
| Skill | Kapabilitas yang dipaketkan | Prompt + file + script reusable untuk tugas umum |
| Tool profile | Set kapabilitas yang diizinkan | Salah satu tuas terbesar untuk keamanan dan perilaku |
| Model policy | Model utama plus fallback | Mengendalikan kualitas, biaya, dan posture keamanan tool |

### Perintah yang layak dihafal lebih awal

| Tugas | Perintah |
|-------|----------|
| Menjalankan setup terpandu | `openclaw onboard` |
| Mengonfigurasi ulang nanti | `openclaw configure` |
| Membuka dashboard browser | `openclaw dashboard` |
| Memeriksa health dan migrasi | `openclaw doctor` |
| Mengaudit posture keamanan | `openclaw security audit` |
| Audit keamanan mendalam | `openclaw security audit --deep` |
| Menambah agent lain | `openclaw agents add <name>` |
| Melihat config | `openclaw config get <path>` |
| Memperbarui config | `openclaw config set <path> <value>` |
| Memeriksa auth/status model | `openclaw models status` |
| Prompt lokal cepat | `openclaw agent --message "Ship checklist"` |

### Saran praktis

- Gunakan onboarding dan `openclaw configure` sebelum mengedit banyak JSON secara manual.
- Buat agent kedua lebih awal jika ingin memisahkan personal use dari work automation.
- Periksa `openclaw models status` setiap kali provider terasa "sudah dikonfigurasi tapi tidak berjalan".

---

<a id="channels-what-to-connect-first"></a>
## 5. Channel: apa yang harus dihubungkan lebih dulu

Jangan hubungkan lima channel pada hari pertama. Pilih surface yang sesuai dengan tujuan nyata Anda dan toleransi terhadap kompleksitas setup.

| Channel | First use terbaik | Catatan | Docs |
|---------|-------------------|---------|------|
| WebChat | Smoke test tercepat | Tidak perlu setup bot pihak ketiga; ideal untuk validasi pertama | [WebChat](https://docs.openclaw.ai/web/webchat) |
| Telegram | Jalur bot eksternal paling mudah | Channel nyata pertama yang bagus untuk pengembang | [Telegram](https://docs.openclaw.ai/channels/telegram) |
| WhatsApp | Asisten pribadi harian | Bagus untuk pemakaian nyata, tetapi kebijakan DM harus ketat | [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) |
| Slack | Tim atau workflow internal | Pahami trust boundary sebelum memberi akses workspace yang luas | [Slack](https://docs.openclaw.ai/channels/slack) |
| Discord | Server privat atau eksperimen komunitas | Kencangkan aturan DM dan grup sebelum membukanya | [Discord](https://docs.openclaw.ai/channels/discord) |
| Signal | Penggunaan pribadi yang fokus pada privasi | Ketergantungan ekstra, tetapi layak jika Anda memang aktif di Signal | [Signal](https://docs.openclaw.ai/channels/signal) |

### Aturan praktis

- Ingin jalur sukses tercepat: mulai dengan WebChat atau Telegram.
- Ingin daily-driver sungguhan: pindah ke WhatsApp setelah dashboard stabil.
- Ingin dipakai tim: pelajari keamanan dan pemisahan agent lebih dulu, lalu gunakan Slack atau Discord.

---

<a id="deployment-choices"></a>
## 6. Pilihan deployment

| Skenario | Jalur yang direkomendasikan | Alasan |
|----------|-----------------------------|--------|
| Evaluasi pertama | CLI onboarding lokal + dashboard | Kompleksitas rendah dan debugging paling mudah |
| Asisten pribadi always-on | Server rumahan / Mac mini / Linux box + daemon | Setup harian yang stabil dengan kontrol lokal |
| VPS murah | Docker | Batas host lebih bersih dan redeploy lebih sederhana |
| Infra pribadi yang reproducible | Nix | Config deklaratif dan instalasi berulang |
| Akses remote | Tailscale atau SSH tunnel | Lebih aman daripada mengekspos gateway langsung ke internet |
| Banyak trust boundary | Gateway terpisah, idealnya juga user OS atau host terpisah | OpenClaw tidak dirancang untuk hostile multi-tenant isolation pada satu gateway |

### Baca ini sebelum deployment remote

Akses remote adalah sesuatu yang sebaiknya ditambahkan setelah setup lokal berjalan, bukan sebelumnya. Mode kegagalan yang umum adalah mengekspos asisten yang kuat sebelum pairing rules, allowlists, tool profiles, dan batas antar-agent benar-benar dipikirkan.

---

<a id="security-baseline"></a>
## 7. Baseline keamanan

Ini adalah bagian yang sering dilewati banyak daftar "awesome", padahal justru dibutuhkan pengembang.

### Aturan dasar

- Perlakukan DM masuk, konten web, chat bersama, dan file upload sebagai input tidak tepercaya.
- Pertahankan akses DM dalam mode pairing atau strict allowlist saat Anda masih mempelajari sistem.
- Jika lebih dari satu orang bisa mengirim DM ke bot, gunakan `session.dmScope: "per-channel-peer"` atau yang lebih ketat.
- Pertahankan channel grup dalam mode mention-gated kecuali ada alasan kuat untuk membuka lebih luas.
- Mulailah dengan tool profile yang restriktif dan perluas akses hanya saat Anda benar-benar tahu alasannya.
- Untuk session bersama atau non-main, utamakan sandboxing daripada hanya mengandalkan disiplin prompt.
- Biarkan gateway tetap local-only sampai remote access dan auth benar-benar dikonfigurasi.
- Jalankan `openclaw security audit` secara berkala, dan gunakan `--deep` sebelum memperluas exposure.
- Pisahkan trust boundary personal dan perusahaan ke agent yang berbeda, sebaiknya juga di gateway atau host yang berbeda.

### Tautan keamanan bernilai tinggi

- [Security Guide](https://docs.openclaw.ai/gateway/security)
- [Sandboxing](https://docs.openclaw.ai/gateway/sandboxing)
- [Remote Access](https://docs.openclaw.ai/gateway/remote)
- [Tailscale](https://docs.openclaw.ai/gateway/tailscale)
- [Doctor](https://docs.openclaw.ai/gateway/doctor)

---

<a id="official-docs-by-goal"></a>
## 8. Dokumentasi resmi berdasarkan tujuan

| Tujuan | Tautan terbaik |
|--------|----------------|
| Instalasi pertama | [Getting Started](https://docs.openclaw.ai/start/getting-started) |
| Setup terpandu | [Onboarding (CLI)](https://docs.openclaw.ai/start/wizard) |
| Pengujian browser-first | [Dashboard](https://docs.openclaw.ai/web/dashboard) |
| Configuration | [Configuration](https://docs.openclaw.ai/gateway/configuration) |
| Setup model | [Models CLI](https://docs.openclaw.ai/concepts/models) |
| Gambaran channel | [Channels](https://docs.openclaw.ai/channels) |
| Skills | [Skills](https://docs.openclaw.ai/tools/skills) |
| Browser automation | [Browser Tool](https://docs.openclaw.ai/tools/browser) |
| Instalasi Docker | [Docker](https://docs.openclaw.ai/install/docker) |
| Penguatan keamanan | [Security](https://docs.openclaw.ai/gateway/security) |
| Exposure remote | [Remote Access](https://docs.openclaw.ai/gateway/remote) |
| Akses remote via Tailscale | [Tailscale](https://docs.openclaw.ai/gateway/tailscale) |
| Troubleshooting | [FAQ](https://docs.openclaw.ai/help/faq) |

### Urutan baca yang disarankan

1. Getting Started
2. Onboarding
3. Dashboard
4. Configuration
5. Satu doc channel
6. Security
7. Skills, browser automation, dan remote access

---

<a id="curated-ecosystem-links"></a>
## 9. Tautan ekosistem terpilih

Lihat tautan ini setelah Anda punya instalasi yang benar-benar berjalan. Tautan ini jauh lebih berguna ketika alur onboarding resmi sudah masuk akal bagi Anda.

### Resmi

| Sumber daya | Kenapa penting |
|-------------|----------------|
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | Codebase utama dan README otoritatif |
| [docs.openclaw.ai](https://docs.openclaw.ai) | Hub dokumentasi resmi |
| [openclaw/clawhub](https://github.com/openclaw/clawhub) | Direktori skill resmi dan katalog paket |
| [openclaw/nix-openclaw](https://github.com/openclaw/nix-openclaw) | Packaging Nix untuk instalasi reproducible |

### Komunitas

| Sumber daya | Kenapa penting |
|-------------|----------------|
| [essamamdani/openclaw-coolify](https://github.com/essamamdani/openclaw-coolify) | Template Coolify untuk pengguna PaaS self-hosted |
| [serhanekicii/openclaw-helm](https://github.com/serhanekicii/openclaw-helm) | Helm chart jika deployment Anda berpusat pada Kubernetes |
| [lunarpulse/openclaw-mcp-plugin](https://github.com/lunarpulse/openclaw-mcp-plugin) | Titik awal integrasi yang berorientasi MCP |
| [centminmod/explain-openclaw](https://github.com/centminmod/explain-openclaw) | Dokumentasi teknis mendalam dan catatan deployment/keamanan |

---

<a id="common-mistakes"></a>
## 10. Kesalahan umum

- Membaca tabel hosting besar sebelum local chat benar-benar berjalan
- Menghubungkan terlalu banyak channel sekaligus lalu men-debug noise alih-alih satu jalur yang jelas
- Menganggap shared tool-enabled agent sebagai aplikasi multi-tenant yang aman
- Mengekspos gateway secara remote sebelum pairing, allowlist, dan auth diuji secara lokal
- Mencampur trust boundary personal dan perusahaan dalam satu runtime asisten yang kuat
- Mengharapkan performa model lokal yang kuat di hardware terbatas tanpa perencanaan
- Mengedit banyak config secara manual sebelum onboarding membuat baseline yang masuk akal

---

<a id="contributing"></a>
## 11. Kontribusi

Lihat [CONTRIBUTING.id.md](./CONTRIBUTING.id.md).

Saat menambahkan tautan, prioritaskan sumber daya yang membantu pengembang biasa melakukan salah satu pekerjaan berikut dengan baik:

- menginstal OpenClaw
- mengonfigurasikannya dengan benar
- mengamankannya secara masuk akal
- men-debug lebih cepat
- memperluasnya dengan payoff pengembangan yang nyata

---

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

Daftar ini dirilis di bawah CC0 1.0 Universal (Public Domain).
