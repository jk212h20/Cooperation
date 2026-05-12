# Cooperation Pi Package

This directory is a [pi package](https://shittycodingagent.ai) that both partners install so we share the same agent extensions, skills, prompt templates, and themes.

## Install

After cloning Cooperation (or even without cloning), each partner runs:

```bash
pi install git:github.com/jk212h20/Cooperation
```

Pi clones the whole repo and reads the root `package.json`, which points at the resource directories inside `pi/`. Re-run `pi update` to pull the latest.

If you want to test local edits before pushing:

```bash
pi install /Users/<you>/ActiveProjects/Cooperation
```

## What goes in here (synced across partners)

- **`extensions/`** — TypeScript/JS extensions both partners want available. Generic, project-agnostic tools.
- **`skills/`** — `SKILL.md` files or skill folders that encode shared know-how (e.g. "how we deploy to Railway", "how to write a journal entry").
- **`prompts/`** — shared prompt templates (e.g. session-start prompt that loads STATE + journal).
- **`themes/`** — UI themes if we ever care.

## What does NOT go in here (stays personal)

- `~/.pi/agent/settings.json` — your model preferences, default provider, enabled models. Personal.
- `~/.pi/agent/auth.json` — API keys. **Never** sync.
- `~/.pi/agent/models.json` — your local model list.
- `~/.pi/agent/sessions/` — your transcripts.

Rule of thumb: if it's about *what tools/skills are available*, it belongs here. If it's about *which model you like* or *your credentials*, it stays in `~/.pi/agent/`.

## Adding a new extension/skill/prompt

1. Drop it in the right subdirectory (`extensions/`, `skills/`, `prompts/`, `themes/`).
2. Note it in `JOURNAL/YYYY-MM-DD.md` so the partner sees it on next session.
3. Commit + push. Partner runs `pi update` next session.
4. If it's load-bearing for the workflow, add a line to `AGENTS.md` so agents know to use it.

## Conventions

- Extensions and skills here should be **project-agnostic**. Project-specific tooling lives in the project repo's own `.pi/` directory.
- Don't add anything that requires personal credentials baked in. If a skill needs an API key, the skill must read it from env or a Keychain/1Password lookup, not from a committed file.
