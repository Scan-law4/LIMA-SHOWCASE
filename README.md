# 🤖 Lima — Local Intelligent Management Assistant

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Ollama](https://img.shields.io/badge/Ollama-Latest-blue)](https://ollama.com)
[![Pop!_OS](https://img.shields.io/badge/OS-Pop!_OS%2024.04-green)](https://pop.system76.com)

## What is Lima?

**Lima** is a personal AI assistant designed to run entirely on your local machine, combining persistent memory, autonomous skills, and comprehensive capabilities while maintaining complete privacy.

> **"I am Lima — Local Intelligent Management Assistant. I always respond in English. I address my owner as Scan."**

---

## ✨ Features

### 🧠 Intelligent Hybrid Architecture
- **Local-first AI** — Qwen3.5, Hermes-4, and other models run offline
- **Persistent Memory** — 3-tier knowledge organization (diary, biography, library, projects)
- **Auto-Logging** — Daily context capture at 08:00 CET
- **Privacy-First** — Zero data exfiltration, explicit cloud permission

### 🤖 48+ Specialized Skills

| Category | Skills |
|----------|--------|
| **Autonomous Agents** | claude-code, codex, hermes-agent, opencode |
| **Creative** | ascii-art, manim-video, p5js, songwriting |
| **Data Science** | jupyter-live-kernel, data-science |
| **DevOps** | webhook-subscriptions, dogfood |
| **Productivity** | google-workspace, linear, notion |
| **GitHub** | code-review, github-pr-workflow, issues |
| **Research** | arxiv, llm-wiki, polymarket |
| **Media** | gif-search, heartmula, songsee, youtube-content |
| **Software Dev** | test-driven-development, systematic-debugging |
| **And more!** | 50+ additional capabilities |

### 🎯 Capabilities
- Task management and prioritization
- Code review and analysis
- Document creation (Markdown, HTML, PDF)
- Research and literature reviews
- Media generation and editing
- Web automation and scraping
- Database management (Linear, Notion, Google Workspace)
- System monitoring and debugging

## 📐 Architecture

### Local-First Design
```
┌─────────────────────────────────┐
│   Pop!_OS 24.04 (RTX 3090, 128GB)│
│                                 │
│  ┌───────────────────────────┐  │
│  │   Ollama (llama.cpp)      │  │
│  │   • glm47-flash:q4km      │  │
│  │   • Hermes-4 (Q6/Q8)      │  │
│  │   • qwen3.5:9b            │  │
│  │   • carnice-moe:q4km      │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌───────────────────────────┐  │
│  │   3-Tier Knowledge System │  │
│  │   ~/LIMA/                 │  │
│  │   ├─ diary/              │  │
│  │   ├─ biography/          │  │
│  │   ├─ library/            │  │
│  │   ├─ projects/           │  │
│  │   └─ todo/               │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

## 🚀 Quick Start

### Prerequisites
- Linux-based system (Pop!_OS recommended)
- 16GB+ RAM (32GB+ recommended)
- 50GB+ free disk space
- NVIDIA GPU with 8GB+ VRAM (CUDA acceleration)

### Installation

```bash
# Install Ollama
curl -fsSL https://ollama.com/install.sh | sh

# Pull LIMA models
ollama pull glm47-flash:q4km
ollama pull Hermes-4:Q8_0
ollama pull qwen3.5:9b

# Start LIMA
# LIMA will auto-load skills based on task context
```

### First Steps

1. **Verify installation**
   ```bash
   ollama list
   ```

2. **Set up knowledge base**
   ```bash
   # Create LIMA directory structure
   mkdir -p ~/LIMA/{diary/{activities,archive},biography,library/{web-search,document-study,config-reference,backup},projects/{cicija,openshophr,subscriptions},todo}
   # Initialize index
   cat > ~/LIMA/index.md << 'EOF'
   # Lima Knowledge Repository

   ## Daily Diary
   - [2026-04-13](diary/daily/2026-04-13.md)

   ## Projects
   - [Lima Core](projects/GITHUB-DOCUMENTATION.md)

   ## System Docs
   [Hardware Specs](library/hardware.md)
   EOF
   ```

3. **Start using Lima**
   - Simply interact with Lima in Telegram, CLI, or terminal
   - LIMA loads appropriate skills automatically
   - Ask anything — from coding to research

## 📁 Project Structure

```
~/LIMA/
├── index.md                    # Master index
├── diary/
│   ├── daily-journal.md         # Daily logs
│   ├── weekly-summary.md        # Weekly summaries
│   └── activities/              # Detailed logs
├── biography/
│   └── chapter_01_introduction.md
├── library/
│   ├── index.md                 # Library index
│   ├── web-search/              # Research findings
│   ├── document-study/          # Document specs
│   ├── config-reference/        # System configs
│   └── backup/                  # Backups
├── projects/
│   ├── cicija/                  # Grocery savings app
│   ├── openshophr/              # HR management
│   ├── subscriptions/           # Asset tracking
│   └── GITHUB-DOCUMENTATION.md  # This file
└── todo/                        # Task lists
```

## 🧰 Using the Skills

LIMA automatically loads relevant skills when needed. You can also load skills explicitly:

```bash
# View skills
skills_list

# Load a skill
skill_view(lima-knowledge-management)

# Use skill functions
# Skills provide specialized tools and workflows
```

**Example:** When you ask to "research a topic," LIMA automatically loads `arxiv`, `llm-wiki`, `blogwatcher`, and other research-related skills.

## 🎓 Workflow Examples

### Example 1: Daily Logging
```
You: "Log today's activities"
→ LIMA uses lima-knowledge-management skill
→ Creates diary entry in ~/LIMA/diary/daily-journal.md
→ Updates biography
→ Updates index
→ Stores documentation in library/
```

### Example 2: Code Review
```
You: "Review this PR"
→ LIMA loads github-code-review skill
→ Fetches code diffs
→ Analyzes code quality
→ Creates inline comments
→ Mentions security issues
→ Suggests improvements
```

### Example 3: Research Paper
```
You: "Write an NeurIPS paper on transformers"
→ LIMA loads research/ml-paper-writing skill
→ Identifies requirements
→ Structure: Abstract → Introduction → Methods → Experiments
→ Cites relevant papers
→ Writes in LaTeX format
→ Checks for consistency
```

## 🔒 Privacy & Security

- **Zero Data Exfiltration** — All processing stays local
- **Private Models** — Qwen3.5, Hermes-4, etc. never leave your machine
- **Explicit Permission** — Never sends data to cloud without asking
- **Customizable** — You control what happens to your data
- **Encrypted** — Knowledge stored in plain text (customize encryption as needed)

## 📊 Hardware Specs

| Component | Specification |
|-----------|---------------|
| OS | Pop!_OS 24.04 LTS |
| GPU | NVIDIA RTX 3090 (24GB VRAM) |
| RAM | 128GB DDR4 |
| Storage | 907GB NVMe SSD |
| Network | Intel Wi-Fi 6 AX200 / Realtek 2.5GbE |
| Mobile | Xiaomi 14T, Redmi Note 9 Pro |

## 🧪 Models Available

LIMA loads multiple local models:

| Model | Size | Purpose |
|-------|------|---------|
| glm47-flash:q4km | 18GB | General purpose |
| Hermes-4 (Q6_Q/Q8_0) | 12-15GB | Complex reasoning |
| qwen3.5:9b | 6.6GB | Coding & logic |
| carnice-moe:q4km | 21GB | Specialized tasks |
| qwen2.5-coder:7b-instruct | 4.7GB | Code generation |
| glm-4.7-flash | 19GB | Fast inference |
| nomic-embed-text | 274MB | Embeddings |
| hermes3:8b-llama3.1-q8_0 | 8.5GB | LLaMA-3.1 fine-tune |

> **Note:** Models are downloaded once with `ollama pull`. No external API calls required.

## 🏃 Active Projects

1. **[Lima Core](./GITHUB-DOCUMENTATION.md)** — Continuous development and expansion
2. **[Cicija](./cicija/README.md)** — Grocery savings mobile app (Business plan complete)
3. **[OpenShopHR](./openshophr/README.md)** — HR management solution
4. **[Subscription Manager](./subscriptions/README.md)** — Audit and asset tracking

## 🗺️ Roadmap

### Short-term (Q2 2026)
- [ ] Complete Cicija backend implementation
- [ ] Launch OpenShopHR pilot
- [ ] Expand skill documentation
- [ ] Add support for additional Linux distributions

### Medium-term (Q3-Q4 2026)
- [ ] Cross-device synchronization
- [ ] Mobile companion apps
- [ ] Hardware platform support (Mac, Windows)
- [ ] Enhanced privacy features (end-to-end encryption)

### Long-term (2027+)
- [ ] Multi-agent orchestration
- [ ] Learning algorithms
- [ ] Model fine-tuning capabilities
- [ ] Community extensions

## 🤝 Contributing

Lima is a personal project. For questions or feedback:
- GitHub: `github.com/Scan-law4`
- Email: (Contact via GitHub account)

### Want to add a skill?

1. Create a skill directory: `~/.hermes/profiles/lima/skills/YOUR-SKILL/`
2. Create `SKILL.md` with YAML frontmatter
3. Write the skill documentation
4. Test thoroughly
5. Commit to your GitHub repository

## 📄 License

This project is maintained by Scan (Neven Sirotić).

---

**⭐ Star our GitHub repository!**

[![GitHub stars](https://img.shields.io/github/stars/Scan-law4/LIMA.svg?style=social)](https://github.com/Scan-law4/LIMA)

**Last Updated:** April 13, 2026  
**Lima Version:** 2.0  
**Made with ❤️ on Pop!_OS**