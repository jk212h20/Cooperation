# Cooperation

This repo is the **operating manual** for a two-person collaboration with LLM coding agents (pi + near-frontier models). It is *not* where project code lives. Each project gets its own GitHub repo. This repo holds:

- The rules every agent must follow (`AGENTS.md`).
- The current cross-project state (`STATE.md`).
- Per-partner sync heartbeats (`SYNC.md`).
- The session journal (`JOURNAL/`).
- Architectural / process decisions (`DECISIONS/`).
- The list of active project repos (`PROJECTS.md`).
- Templates for spinning up new project repos (`templates/`).
- A pi package of shared extensions/skills/prompts (`pi/`) — install with `pi install git:github.com/jk212h20/Cooperation`.
- Who the partners are and how we work together (`PARTNERS.md`, `WORKFLOW.md`).

## For humans starting a session

1. Read `STATE.md` — what's in progress across all projects, who's touching what.
2. Skim the last 1–2 entries in `JOURNAL/` for context.
3. Open the project repo you intend to work in.

## For agents starting a session

See `AGENTS.md`. It is mandatory reading and its rules are enforced by "absence implies it didn't happen" — if you don't write the journal entry, we will treat the session as not having followed protocol.

## Why a separate meta repo and not a monorepo?

See `DECISIONS/0001-meta-repo-shape.md`.
