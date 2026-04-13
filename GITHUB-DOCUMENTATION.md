# LIMA — Local Intelligent Management Assistant System

**Lima** is one autonomous AI agent within the LIMA system — a sophisticated local AI infrastructure designed for complete privacy, persistent knowledge, and continuous improvement.

---

## Core Philosophy

- **Honesty over impression** — Never fabricates capabilities. When I don't know, I say so.
- **Usefulness over caution** — Prefers helpful answers with caveats over refusal.
- **Privacy-first** — All data stays on your local machine. Zero data exfiltration.
- **Cross-session learning** — Remembers user preferences and facts across sessions.

---

## Local-First Architecture

Lima runs entirely on your hardware with no cloud dependencies for private tasks.

### Hardware Foundation

| Component | Specification |
|-----------|---------------|
| Operating System | Pop!_OS 24.04 LTS |
| GPU | NVIDIA RTX 3090 (24GB VRAM) |
| RAM | 128GB DDR4 |
| Storage | NVMe SSD with dedicated knowledge organization |

### Model Strategy

- **Private/sensitive tasks:** Qwen3.5, Hermes-4, etc. — fully offline
- **Public work:** Cloud models OK (Claude, GPT, etc.)
- **Default:** Try local first. Never sends private data without explicit approval.

---

## 3-Tier Knowledge Memory System

Lima maintains persistent, structured knowledge across sessions:

- **Master Index** (`~/LIMA/index.md`) — Complete knowledge map
- **Daily Context** (`~/LIMA/diary/`) — Automated logging at 08:00 CET
- **Biography Tracking** (`~/LIMA/biography/`) — Progressive life documentation
- **Project Archives** (`~/LIMA/projects/`) — Active business initiatives
- **Library System** (`~/LIMA/library/`) — Configurations, hardware specs, research findings

All data lives locally. No external storage required.

---

## Key Skills & Capabilities

### Knowledge Management

- **`lima-knowledge-management`** — Automated 3-tier organization workflow
- **`storage-approach`** — Standardized hardware documentation system
- **`obsidian`** — Full Obsidian vault integration and management
- **`daily-context-capture`** — Automated daily activity logging

### CI/CD & Automation

- **`lima-cicd`** — GitHub Actions workflows for testing, model checks, and daily summaries
- **Automated cron scheduling** — Task automation and monitoring
- **Docker orchestration** — Build and deployment monitoring

### Code & Development

- **Multi-agent delegation** — Claude Code, OpenAI Codex, OpenCode workflows
- **Automated code review** — Security-aware analysis and feedback
- **Test-driven development** — Full TDD pipeline
- **Systematic debugging** — Bug diagnosis and resolution
- **Plan execution** — Markdown-based multi-step implementation planning

### Research & Investigation

- **Literature review** — Academic paper discovery (arXiv), blog monitoring (RSS/Atom)
- **Digital footprint analysis** — Public persona and reputation audits
- **Prediction markets** — Polymarket query capabilities
- **Academic writing** — ML research paper generation (NeurIPS, ICML, ICLR)

### Media & Creativity

- **Audio generation** — HeartMuLa music generation
- **Video content** — YouTube transcript extraction and transformation
- **Visualizations** — ASCII art, diagrams, and interactive visuals

### System Management

- **Process monitoring** — Docker and build status tracking
- **Disk and memory optimization** — System performance awareness
- **Session management** — Automatic diary logging on completion

---

## Language & Privacy

**Language Support:**
- Primary: Always responds in English per user preference
- Secondary: Can understand and work with Croatian communications

**Privacy Guarantees:**
- Zero data exfiltration — all processing stays local
- Private models run offline (Qwen3.5, Hermes-4, etc.)
- Explicit cloud permission required for any external API calls
- Configurable — you control what happens to your data

---

## About the Developer

**Scan (Neven Sirotić)** — Building Lima as the foundation of his personal AI ecosystem.

**Contact:**
- GitHub: [@Scan-law4](https://github.com/Scan-law4)
- Email: scan@law-4.com

---

## Status & Licensing

**Work in Progress** — Lima is continuously evolving. No feature guarantees.

**License:** MIT

Built with ❤️ on Pop!_OS 24.04, NVIDIA RTX 3090, 128GB RAM.

**Last Updated:** April 2026