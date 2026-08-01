# Codex port

The `codex` branch is the maintained Codex adaptation of
[`mattpocock/skills`](https://github.com/mattpocock/skills). Its initial upstream
base is `2ab958093e83e0ec752e6c1c5932da465bf23e0c`.

## Ownership boundary

Upstream owns:

- the base skill purpose, flow, and product behavior;
- skill frontmatter;
- official `agents/openai.yaml` metadata, except a documented compatibility
  correction where it contradicts the skill's declared invocation behavior;
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
  effects when subagents share a workspace.

All planning, ticketing, implementation, review, TDD, and domain-model behavior
comes from upstream. Codex adaptations change only harness syntax, instruction
discovery, subagent orchestration, and the minimum metadata needed to expose the
same invocation policy.

At the user's request, the complete upstream `release/v1.2` stack at
`bfdaef8e989a5c81160e74bc5043bd434da49cac` is integrated before it lands on
`main`. This includes round-by-round grilling, the shareable HTML logic
prototype, `to-questionnaire` graduation, and the breaking
`writing-great-skills` → `writing-for-agents` replacement. `$grill-me` and
`$grill-with-docs` inherit the single `$grilling` primitive; the former
standalone `batch-grill-me` copy stays removed.

The v1.2 `writing-for-agents` metadata arrived with the old display name and
implicit invocation disabled, contradicting its new name, frontmatter, and
changeset. This branch corrects that metadata so Codex discovers the skill as
model-invoked, and keeps its mechanics reference dual-harness.

Do not introduce an unlisted product-behavior delta without documenting it here.

## Source of truth

Upstream `main` is the source for future behavior changes. The checked-out
`codex` branch is the source for Codex adaptations. The installed
`~/.agents/skills` tree is a deployment target only; after the initial import,
never merge changes back from it.

When upstream and the Codex layer conflict:

1. Preserve the current upstream behavior and official metadata, except a
   compatibility contradiction documented above.
2. Re-express only the documented Codex harness deltas.
3. Remove duplicated instructions when another skill is the single source of
   truth.
4. Keep user-visible completion criteria checkable.

## Sync procedure

1. Fetch `upstream/main` and merge it into `codex`; merge a release branch only
   when explicitly requested and record its pinned commit above.
2. Review upstream changes before resolving conflicts.
3. Keep upstream `agents/openai.yaml` files unchanged unless a documented Codex
   compatibility correction is required.
4. Reconcile only the explicit deltas listed above.
5. Validate frontmatter, metadata policy, references, conflict markers, and
   whitespace.
6. Commit and push `codex`.
7. Update installed skills only as a separate, explicitly approved deployment.
