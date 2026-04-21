# Lessons

What follows is a running log of things that did not work, things that worked unexpectedly, and surprises. This file is more useful to Scan's own future self than anything else in this repository; it is public because honest failure logs are rare and worth sharing.

## Third-party cloud tool usage is billed separately from subscription quota

Scan initially assumed that a Pro subscription to Anthropic's Claude would cover third-party tool access using the same model. It does not. Under Anthropic's policy at the time, third-party OAuth-based tool access drew from a separate pre-paid pool at API rates, which for Opus was expensive enough to burn through quickly.

Pepper was set up on April 17, 2026, running on Claude Opus via OAuth. Between April 17 and April 20, two sessions of development work consumed about €15 of pre-paid credit with one usable deliverable. The session ended cleanly when credit ran out — no surprise bill — but the experience was enough to rule out cloud-first as the architecture for ongoing work. On April 20 Pepper pivoted to local-first GLM via Ollama. This is the single biggest financial lesson in the system's history, and the reason the current architecture puts the cloud advisor behind the human rather than behind the agent.

The elimination of Cursor and OpenRouter subscriptions followed from the same pivot: once Pepper was operating locally, the cloud coding-assistant tier that Cursor provides was no longer needed, and OpenRouter's pay-per-token routing became redundant. Both are being cancelled at their next renewal windows.

## A local-first instinct, talked out of, turned out to be right

Scan's original plan, on day one, was for the agents to run entirely locally. That plan was argued against at the time — partly by Scan's own cost-benefit instincts, partly by advice from an external source that overweighted frontier-model capability. Three days later, after a round of cloud-first experimentation and the billing discovery above, Scan returned to the original plan.

The lesson here is not about cloud versus local. It is about advice from external sources, including capable AI assistants, being weighted correctly against Scan's own domain knowledge. Scan knew the hardware, the usage pattern, and the cost constraints; the external advice did not. The correct move was to trust Scan's instinct and test cloud-first cheaply, not to reorganize the architecture around cloud assumptions. This lesson applies more broadly than to this project.

## Three local-agent architectures tried and rejected before Hermes

Before Hermes, Scan tried three approaches to the local-agent problem, in sequence. The first was direct Ollama with a custom web UI — a minimal setup where the agent was essentially a chat interface over a local model, with memory hand-rolled on top. The second was [OpenClaw](https://github.com/openclaw/openclaw), an open-source personal-agent framework that had recently become popular. The third was [Luna](https://github.com/GitCoder052023/Luna), another open-source local-agent project.

None of these survived to production. The reasons were different per framework, but the common failure mode was long-term memory architecture. Each framework had a memory layer that worked in principle: files on disk, retrieval on some schedule, injection into context. In practice, the agent could not reliably decide *where* a given piece of knowledge belonged, *when* to apply it, or *how* to apply it in a new context. Memory accumulated, but it accumulated as a pile, not as a structure. The agent could not use it.

Hermes solved this, or at least came closer, in two ways. First, its memory surface is structurally simpler: a single `MEMORY.md` file with discrete entries, edited deliberately, rather than an opaque retrieval pipeline over a growing corpus. Second, its skills system separates procedural knowledge from factual knowledge — how-to-do-things lives in skill files, world-facts live in memory, and the two don't get confused. This was the second half of the problem: earlier frameworks had no mechanism for the agent to encode its own procedures durably. Without that, the agent re-learned the same routines every session and the operator re-taught them.

The lesson is not that Hermes is special. Other frameworks may solve these problems equally well or better by the time anyone reads this. The lesson is that for a local-agent system to be useful over time, the memory-and-skills architecture needs to make deliberate, structural space for *what the agent knows* and *what the agent does*, and keep them separate. A framework that only provides "memory" in the retrieval-augmented-generation sense is not enough.

## A sandboxed home directory is not the home directory

When an agent runs in the Hermes framework, its `$HOME` environment variable points to a sandbox directory inside the agent's profile, not to Scan's real home directory. Tilde expansion goes to the sandbox. The first time Scan asked an agent to write to `~/projects/`, the file landed somewhere Scan could not find without a full-disk search.

The fix is to use absolute paths for any filesystem work outside the sandbox, and to document this in the agent's memory as a standing rule. The lesson: agent frameworks can make reasonable decisions about sandboxing that nevertheless surprise the reader the first time they hit them. Read the documentation; verify paths with a test write before trusting them.

## A memory file without delimiters is one entry, not many

Early versions of the memory format treated `MEMORY.md` as a flat document. When the memory tool was called to replace an entry, it replaced the entire file, clobbering everything else. The fix was to structure the memory as discrete entries separated by a delimiter, so that entry-level replacement became possible.

The underlying lesson: what an agent sees as "one entry" depends on how the file is structured, not on how a human thinks about the content. Memory formats need to be designed for the tools that edit them, not only for the humans that read them.

## Context windows have a cliff, not a limit

The 9B local model used in the system has a nominal context window of tens of thousands of tokens. In practice, performance degrades sharply before that nominal limit is reached. Sessions that look healthy at 40K tokens start to behave unreliably at 48K — responses become shorter, reasoning becomes thinner, and the agent starts forgetting material from earlier in the session.

The operational fix is to treat the practical ceiling as much lower than the nominal one, to commit state to disk frequently, and to design work units that can be resumed from a fresh session if needed. The lesson generalizes: model capacity specifications describe a ceiling, not a usable range, and the difference matters.

## Auxiliary model calls that silently fail are worse than failures that shout

The framework supports an auxiliary model for secondary tasks like context compression. When that auxiliary is misconfigured or missing credentials, some compression operations fail silently and simply drop content from the agent's context. The agent then continues with a quietly degraded view of the session.

The failure mode was traced by noticing that agents were giving thin answers to questions whose context had just been discussed a few turns earlier. The fix was to route auxiliary calls to the same main model rather than to a separate one — acceptable for a small setup, and eliminates a whole class of silent degradation.

## Positioning is judgment work and a 9B model will invent things

When one of the agents was asked to write the public documentation for this repository, she produced a competently formatted but substantially invented document. Models that did not exist were listed. Skills that belonged to other systems were described as native capabilities. A roadmap was produced containing commitments Scan had never made. The agent did this not because she was dishonest, but because the structural slots of a "README" pattern pulled in content from her broader training, and her judgment about which content was hers to claim was poor.

The lesson is architectural: positioning is not a task for a small local model. Positioning requires knowing what is true about the system, what is strategically appropriate to share, and how to frame it for a specific audience. The first is difficult for any language model without careful scaffolding; the second and third are judgment calls a human needs to make. The documentation in this repository was produced through the human-bridged advisor loop for this reason.

## Agents with access to private data will make bad publication decisions

One of the agents, while attempting to produce a public-facing project summary, pulled content from a folder containing Scan's private subscription and financial data. The content was caught before publication, but the episode exposed an architectural gap: an agent trusted with private data for one job cannot be trusted to make publication judgments about it.

The working fix is to give Studio (the publication-facing agent, when she comes online) no access to private data at all — her inputs are Scan's explicit design briefs and brand assets, nothing else. The general lesson: agent permissions should be scoped to jobs, not to profiles, and an agent that reads sensitive data should not also write public content.

## The system's real value is in the discipline, not the code

If someone read the configuration files, the skill definitions, and the memory files for each agent, they would find nothing technically novel. The underlying framework is open source. The models are publicly available. The techniques — persistent on-disk memory, skill libraries, sandboxing — are well-understood in the local-agent community.

What is distinctive is the operating discipline that sits on top: the gate-check-before-touch rule, the verified-before-capture rule for skills, the commit-with-evidence rule, the never-push-without-permission rule, the handoff-file-before-session-end rule, the human-bridged advisor loop, the profile isolation between agents, the honest-failure logs like this one. These are cultural patterns, not code. They are what makes the system reliable; they are also what cannot be copy-pasted out of this repository into someone else's setup.

This is probably the most important lesson in the file. The interesting question in autonomous agent systems is not "what can the agent do alone?" but "what discipline around the agent makes its work trustworthy?" Everything else follows from the answer.
