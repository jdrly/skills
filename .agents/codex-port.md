# Codex port

The `codex` branch is the maintained Codex adaptation of
[`mattpocock/skills`](https://github.com/mattpocock/skills). Its initial upstream
base is `2ab958093e83e0ec752e6c1c5932da465bf23e0c`.

## Ownership boundary

Upstream owns:

- the base skill purpose, flow, and product behavior;
- skill frontmatter;
- every official `agents/openai.yaml`;
- promoted-skill inventory and human-facing docs.

Do not fork the published docs merely to replace harness syntax or orchestration
terms. Re-sync them only when the skill's product behavior changes; keep
Codex-only deltas in this file and the operational skill instructions.

This branch owns these explicit deltas:

- `$skill-name` invocation syntax in operational instructions;
- Codex instruction discovery through `AGENTS.override.md` and `AGENTS.md`;
- bounded, clean-context leaf subagents without Claude-specific agent types;
- parallel dispatch with explicit capacity and sequential fallbacks;
- parent-owned verification, repository writes, branch changes, and external side
  effects when subagents share a workspace;
- the accepted-ADR authority model: proposed or explicitly open contracts are
  never guessed into implementation or tests, while deprecated and superseded
  ADRs remain history.

The `$implement` skill tracks upstream behavior. Its only branch adaptation is
Codex `$skill-name` invocation syntax.

Do not introduce an unlisted product-behavior delta without documenting it here.

## Source of truth

Upstream `main` is the source for future behavior changes. The checked-out
`codex` branch is the source for Codex adaptations. The installed
`~/.agents/skills` tree is a deployment target only; after the initial import,
never merge changes back from it.

When upstream and the Codex layer conflict:

1. Preserve the current upstream behavior and official metadata.
2. Re-express the documented Codex and local-policy deltas.
3. Remove duplicated instructions when another skill is the single source of
   truth.
4. Keep user-visible completion criteria checkable.

## Sync procedure

1. Fetch `upstream/main` and merge it into `codex`.
2. Review upstream changes before resolving conflicts.
3. Keep upstream `agents/openai.yaml` files unchanged.
4. Reconcile only the explicit deltas listed above.
5. Validate frontmatter, metadata policy, references, conflict markers, and
   whitespace.
6. Commit and push `codex`.
7. Update installed skills only as a separate, explicitly approved deployment.
