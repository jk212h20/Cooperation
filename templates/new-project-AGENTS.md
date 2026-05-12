# Agent Rules — <PROJECT NAME>

**Meta repo:** `~/ActiveProjects/Cooperation/` — this project inherits all rules in `Cooperation/AGENTS.md` (rules A0–A12). Read those first. The rules below are project-specific additions and overrides.

**Cross-link `CLAUDE.md` → `AGENTS.md`** so Claude Code reads the same file:
```bash
ln -s AGENTS.md CLAUDE.md
```

## Project front matter

- **Name:** <project>
- **GitHub:** <org/repo>
- **Deploy target:** <e.g. Railway project "foo", service "web"> | <none>
- **Primary language / stack:** <e.g. Python 3.12 + FastAPI + Postgres>
- **Owners:** Nick, <partner>
- **Created:** <YYYY-MM-DD>

## Project-specific

### How to run locally
```bash
# fill in
```

### How to run tests
```bash
# fill in
```

### Secrets
Every variable in `.env.example` is required. Real values live in:
- Local dev: <Keychain item name> | <1Password vault/item> | <ask partner>
- Deploy: Railway project `<name>`, service `<name>`, env vars tab.

Never commit a real `.env`. See Cooperation rule A5.

### Deploy verification (per Cooperation rule A7)
After pushing to `main`:
```bash
railway status   # or whatever this project uses
```
Confirm deployed SHA matches `git rev-parse HEAD` before claiming "live."

### Don't-touch (project-specific additions to A8)
- <e.g. `prisma/migrations/` once applied to prod>
- <e.g. `public/vendor/`>

### Definition of done (project-specific additions to A9)
- <e.g. integration test suite passes against staging Railway env>

## Journal location

All sessions touching this repo write their entry in **`Cooperation/JOURNAL/YYYY-MM-DD.md`**, not here. This repo does not have its own journal — there's one canonical journal across all projects.
