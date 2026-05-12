# ADR 0001 — Meta repo for rules, separate repos per project

**Date:** 2026-05-12
**Status:** Accepted
**Deciders:** Nick (partner TBD)

## Context

Two-person collaboration with LLM coding agents (pi + near-frontier models) expected to span multiple projects. Need a durable home for shared conventions, journal, and decisions, plus a way to scope per-project code, history, CI, and visibility (public vs. private).

## Options considered

1. **Single repo, projects as subdirectories.** Pros: one place to grep, one rulebook colocated with code. Cons: shared issues/PRs/visibility; messy history; tight coupling of unrelated work.
2. **Separate repos per project + this meta "Cooperation" repo.** Pros: clean per-project history, independent CI, independent visibility, scales to N projects. Cons: agents in project X don't automatically see the meta repo — must be told.
3. **Monorepo with git submodules.** Submodules are a footgun, especially under agent automation. Rejected.

## Decision

Option 2. The Cooperation repo is the **operating manual** (rules, journal, decisions, templates, project index). Each project lives in its own GitHub repo and includes an `AGENTS.md` that references back to the Cooperation repo's rules.

## Consequences

- New-project setup has a small one-time cost (copy templates, add to `PROJECTS.md`). Mitigated by `templates/`.
- Agents must be pointed at the Cooperation repo from each project's `AGENTS.md`. Enforced by rule A0.
- The Cooperation repo must be kept on disk alongside project repos; convention is `~/ActiveProjects/Cooperation/` next to each `~/ActiveProjects/<project>/`.
- If we ever want to make the meta repo public (to share the workflow), the journal may contain things we don't want public. Revisit visibility before publishing; consider splitting `JOURNAL/` and `STATE.md` into a private sibling repo at that point.

## Revisit if

- We end up with >5 projects and the meta repo feels stale → consider automating STATE/PROJECTS updates.
- Partner uses a different agent that can't follow the cross-repo convention cleanly.
