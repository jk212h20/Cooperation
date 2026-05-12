# Workflow

This is the human-facing version of the rules. The strict version agents must follow is `AGENTS.md`.

## Repo shape

- This `Cooperation` repo: rules, journal, decisions, project index, templates. **No project code lives here.**
- Each project: its own GitHub repo. Drop `templates/new-project-AGENTS.md` in as that repo's `AGENTS.md`, fill in the front matter, and link back to this repo.
- Decision rationale: `DECISIONS/0001-meta-repo-shape.md`.

## Starting a new project repo

1. Create the GitHub repo (private by default; flip to public deliberately).
2. `git clone` it next to `Cooperation/` (i.e. `~/ActiveProjects/<project>`).
3. Copy in the templates:
   ```bash
   cp Cooperation/templates/new-project-AGENTS.md   <project>/AGENTS.md
   cp Cooperation/templates/new-project-README.md   <project>/README.md
   cp Cooperation/templates/PR_TEMPLATE.md          <project>/.github/PULL_REQUEST_TEMPLATE.md
   cp Cooperation/templates/gitignore               <project>/.gitignore
   ln -s AGENTS.md                                   <project>/CLAUDE.md   # for Claude Code compatibility
   ```
4. Fill in the front-matter placeholders in `AGENTS.md` and `README.md`.
5. Add a row to `Cooperation/PROJECTS.md`.
6. Configure Railway (if deploying): create the project, set env vars, point it at the GitHub repo. Record the Railway project name in the project's README.
7. Open a journal entry in `Cooperation/JOURNAL/` noting the new project.

## Shared pi config

Both partners install the Cooperation pi package so we share extensions, skills, prompts, and themes:

```bash
pi install git:github.com/jk212h20/Cooperation
pi update   # later, to refresh
```

The package lives in `pi/` in this repo. Personal pi config (model preferences, auth) stays in `~/.pi/agent/` and is not synced. See `pi/README.md`.

## Daily flow

- **Session start:** `cd Cooperation && git pull && cat STATE.md && ls JOURNAL/ | tail -3`.
- **Pick work:** from STATE.md or the project's issues/STATE.
- **Work in a branch:** `<initials>/<slug>`.
- **PR + review.**
- **Session end:** journal entry, STATE.md updated, push.

## Sync between partners

The repo *is* the async channel. If you need realtime, use whatever's in `PARTNERS.md`. Anything decided realtime must be written down — either in the journal or as an ADR if it's load-bearing.

## What if we disagree?

Either partner can open an ADR with two options listed. The other partner edits in their preference and reasoning. Resolution gets a final "Decision:" section. The ADR is the record; the chat thread is not.
