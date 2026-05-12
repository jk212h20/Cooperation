# STATE — Cross-Project Snapshot

> This file represents **now**. It is not append-only. The journal is the history; this is the photo.
> Last updated: 2026-05-12 13:25 PT by Nick + pi/sonnet-4.5

## Active work

_None — Cooperation meta repo bootstrapped, awaiting first real project and partner onboarding._

## Project repos (see `PROJECTS.md` for the full index)

_None yet._

## Open questions for partners

- Partner name, GitHub handle, initials, agent stack, timezone → fill `PARTNERS.md`.
- Default Railway team/project naming convention.
- Which of Nick's local extensions in `~/.pi/agent/extensions/` should be promoted to the shared Cooperation pi package? Candidates: `railway-status.ts`, `handoff.ts`, `background-bash.ts`, `git-checkpoint.ts`, `auto-commit-on-exit.ts`. Need a per-extension audit for personal config / hard-coded paths first.

## Open infra items

- **Cooperation repo is now PUBLIC.** Decision: process docs + templates + journal are not sensitive today. If the journal ever needs to contain sensitive context, split it off into a private sibling repo (ADR-0001 "Revisit if" already flags this).
- **Branch protection on `main` is ENFORCED** (as of 2026-05-12 13:25 PT): PRs required (0 approving reviews so solo self-merge is allowed per A4.3), force-pushes blocked, deletion blocked. **From the next commit onward, A4.1 binds: no direct pushes to main.**
- **`gitleaks` pre-commit hook** not installed yet. Will wire up when first project repo is created (rule A5.5). Higher priority now that the repo is public.
- **Pi package install verified** for Nick's machine: `pi install git:github.com/jk212h20/Cooperation` clones the repo and discovers skills `cooperation-session-start` and `cooperation-session-end`. **Skills will become available after pi is reloaded** — Nick to reload at his discretion.

## Background processes running

_None._

## Recent deploys

_None — meta repo, nothing to deploy._

## Recent pushes

- `76b7918` — Move pi package manifest to repo root so `pi install git:` works
- `0be888f` — Add SYNC.md heartbeats (rule A0.5) and shared pi package
- `ff17a6f` — Initial scaffold
