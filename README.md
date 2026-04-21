# LIMA

LIMA is a system of specialized local AI agents running on a single workstation. Each agent has a narrow job, persistent memory on disk, and a library of skills it has written for itself after completing real tasks. Everything runs on consumer hardware with no cloud inference for the agents themselves.

This repository is a journal of the system — what it is, how it is put together, and what has been learned from running it. It is not a framework you can install. The components it builds on (Ollama, the Hermes Agent, and similar open-source tooling) are named where relevant; their own repositories are the starting point if you want to build something comparable.

## Who lives here

**Pepper** is the development lead for Scan's commercial software projects. She writes code, runs scripts, opens pull requests, maintains repositories, and files procedural knowledge as skills after each verified task. She does not handle personal or biographical work.

**Lima** is Scan's personal assistant. She maintains a long-form vault of journals, notes, plans, and project context in Obsidian, and she helps with day-to-day work on the machine itself — for example, taking a message like "install this application and make a launcher for it" sent from a phone and having the program ready when Scan gets home. She is responsible for documenting Scan's own work and life, not for writing code or managing repositories.

**Studio** is in development. Her job will be Scan's public-facing web presence — landing pages, design assets, and integration with local image-generation tooling. She is not yet operational; the profile exists as a plan, not a running process.

Each agent has a separate profile, separate memory, separate skill library, and separate channel (Telegram bot per agent). They share the same hardware and, at present, the same model weights. Contention is handled by priority rather than parallelism.

## How it works, briefly

Each agent is defined by two files on disk: a `SOUL.md` that describes identity and operating discipline, and a `MEMORY.md` that holds world-facts the agent needs across sessions. Both survive restarts. Neither is edited by the agent during normal operation — updates are deliberate and attributable.

Skills are directories on disk, each containing a `SKILL.md` with instructions for a specific verified procedure. Agents write their own skills after completing work that might be repeated. A skill that describes a procedure the agent has not actually executed is not a valid skill.

When an agent encounters work beyond its reliable capability — synthesis across many files, novel architectural judgment, debugging a failure mode it does not recognize — it stops and flags this. Scan then consults a frontier model (Claude Opus, in a browser) as an advisor, and returns concrete artifacts to the agent: scripts to run, skills to install, step-by-step instructions to follow. The agent does not make this call itself. The human is the bridge.

## What this repository contains

- [ARCHITECTURE.md](./ARCHITECTURE.md) — how the system is put together, and the decisions that shaped it
- [AGENTS.md](./AGENTS.md) — longer-form descriptions of each agent's role and discipline
- [LESSONS.md](./LESSONS.md) — what has worked, what has not, and what was surprising

## Current status

Lima's current profile came together on April 7, 2026, after earlier iterations on commercial chat platforms (ChatGPT, DeepSeek, SuperGrok) and three rejected local architectures (direct Ollama with a custom web UI, OpenClaw, Luna). Pepper was set up on April 17, initially running on Claude Opus via OAuth, and pivoted to local-first GLM on April 20 after the cloud-first architecture proved operationally unviable. Studio is in design as of late April 2026. Active development continues. No release schedule, no feature roadmap.

## What this repository is not

This is not an open-source framework. It is not installable. It is not seeking contributors. Scan reads issues filed here but makes no commitment to respond. If you want to build something similar, the right starting point is the underlying tools — Ollama for local inference, the Hermes Agent for the agent runtime, your choice of a 9B-to-30B local model — and then whatever discipline you choose to impose on top.

## About

Scan is Neven Sirotić, based in Zagreb, Croatia. Most of his career has been in roles that reward multidisciplinary thinking — marketing, operations, product — and LIMA is his first extended project in applied AI systems. He switched to Linux after years away, specifically to build this system; Pop!_OS is not the most conventional distribution for a project like this, which is itself part of the lesson.

Contact: scan@law-4.com, or via [@Scan-law4](https://github.com/Scan-law4) on GitHub. The repository is maintained as a journal; unsolicited collaboration requests should expect slow or no response while active project work is ongoing.
