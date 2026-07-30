---
name: research
description: Investigate a question against high-trust primary sources and capture the findings as a Markdown file in the repo. Use when the user wants a topic researched, docs or API facts gathered, or reading legwork delegated to a research subagent.
---

First attempt to spawn one read-only research subagent that returns a cited Markdown report body to the parent. Give it a clean, bounded leaf-worker brief containing the research question and source paths; tell it to research directly without spawning another agent. Keep `$research` and orchestration instructions out of that brief, and omit platform-specific agent type, model, reasoning-effort, and full-history-fork requests. Continue only independent work while it runs; otherwise wait for its result. Current-thread fallback is permitted only when no collaboration/subagent capability is exposed or the spawn attempt returns a capacity or nesting error; state why fallback was used.

Its job:

1. Investigate the question against **primary sources** — official docs, source code, specs, first-party APIs — not a secondary write-up of them. Follow every claim back to the source that owns it.
2. Return the findings as one Markdown report body, citing each claim's source. Do not write repository files.

After the subagent returns, the parent verifies the citations and saves the report where the repo already keeps such notes. Match the existing convention; if there is none, put it somewhere sensible and say where.
