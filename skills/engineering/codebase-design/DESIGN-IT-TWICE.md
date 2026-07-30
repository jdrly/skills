# Design It Twice

When the user wants to explore alternative interfaces for a chosen deepening candidate, use this parallel sub-agent pattern. Based on "Design It Twice" (Ousterhout) — your first idea is unlikely to be the best.

Uses the vocabulary in [SKILL.md](SKILL.md) — **module**, **interface**, **seam**, **adapter**, **leverage**.

## Process

### 1. Frame the problem space

Before spawning sub-agents, write a user-facing explanation of the problem space for the chosen candidate:

- The constraints any new interface would need to satisfy
- The dependencies it would rely on, and which category they fall into (see [DEEPENING.md](DEEPENING.md))
- A rough illustrative code sketch to ground the constraints — not a proposal, just a way to make the constraints concrete

Show this to the user, then immediately proceed to Step 2. The user reads and thinks while the sub-agents work in parallel.

### 2. Spawn sub-agents

First attempt to spawn three independent subagents in parallel. Each must produce a **radically different** interface for the deepened module. If slots are temporarily occupied by other workers, wait for them to free up and retry. The sequential fallback is permitted only when no collaboration/subagent capability is exposed, nesting is denied, or capacity remains unavailable after active workers finish; in that case run three separate non-isolated design passes and state why fallback was used. An optional fourth design may be added when capacity permits.

Prompt each subagent with one clean-context text brief (file paths, coupling details, dependency category from [DEEPENING.md](DEEPENING.md), what sits behind the seam). Use one supported text-input field per spawn. Make each brief a leaf design task that asks the worker to design directly without spawning another agent; keep `$codebase-design` and orchestration instructions out of it, and omit platform-specific agent type, model, reasoning-effort, and full-history-fork requests. The brief is independent of the user-facing problem-space explanation in Step 1. Give each agent a different design constraint:

- Design A: "Minimize the interface — aim for 1–3 entry points max. Maximise leverage per entry point."
- Design B: "Maximise flexibility — support many use cases and extension."
- Design C: "Optimise for the most common caller — make the default case trivial."
- Design D (if applicable): "Design around ports & adapters for cross-seam dependencies."

Include both [SKILL.md](SKILL.md) vocabulary and CONTEXT.md vocabulary in the brief so each sub-agent names things consistently with the architecture language and the project's domain language.

Each sub-agent outputs:

1. Interface (types, methods, params — plus invariants, ordering, error modes)
2. Usage example showing how callers use it
3. What the implementation hides behind the seam
4. Dependency strategy and adapters (see [DEEPENING.md](DEEPENING.md))
5. Trade-offs — where leverage is high, where it's thin

### 3. Present and compare

Present designs sequentially so the user can absorb each one, then compare them in prose. Contrast by **depth** (leverage at the interface), **locality** (where change concentrates), and **seam placement**.

After comparing, give your own recommendation: which design you think is strongest and why. If elements from different designs would combine well, propose a hybrid. Be opinionated — the user wants a strong read, not a menu.
