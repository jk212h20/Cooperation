# <PROJECT NAME>

<one-line description>

## Status

<early / active / paused / archived> — see `Cooperation/STATE.md` for cross-project context and `Cooperation/JOURNAL/` for recent activity.

## Setup

```bash
git clone <repo url>
cd <project>
cp .env.example .env
# fill in .env from the source noted in AGENTS.md
<install command>
```

## Run

```bash
<run command>
```

## Test

```bash
<test command>
```

## Deployment

- **Target:** <Railway project "name", service "name"> | <none>
- **Auto-deploy:** <yes from main / no / manual>
- **Verify a deploy:**
  ```bash
  railway status
  # compare deployed SHA to: git rev-parse HEAD
  ```
- **Secrets location:** Railway env vars (see project's Variables tab). Local dev secrets per `AGENTS.md`.

## Collaborators

See `Cooperation/PARTNERS.md`.

## Agent rules

This repo follows the rules in `Cooperation/AGENTS.md` plus the project-specific additions in this repo's `AGENTS.md`. **All sessions must produce a journal entry in `Cooperation/JOURNAL/`.**
