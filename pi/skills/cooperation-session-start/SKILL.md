---
name: cooperation-session-start
description: Use at the start of every session in any repo that participates in the Cooperation workflow. Loads STATE, the latest journal entry, SYNC.md, and the rules. Required by rule A0 in Cooperation/AGENTS.md.
---

# Cooperation Session Start

When the user starts a coding session in any repo under `~/ActiveProjects/` that is part of the Cooperation workflow (i.e. either the `Cooperation` meta repo itself, or a project repo whose `AGENTS.md` references Cooperation), do this **before** taking any other action:

## Step 1 — Read the rules and state

Read these files in order. If any is missing, stop and tell the user.

1. `~/ActiveProjects/Cooperation/AGENTS.md` — the canonical rules A0–A12.
2. `~/ActiveProjects/Cooperation/STATE.md` — current cross-project snapshot.
3. `~/ActiveProjects/Cooperation/SYNC.md` — when the other partner's agent last pulled. Note any staleness.
4. The most recent file in `~/ActiveProjects/Cooperation/JOURNAL/` (sort by name; they're `YYYY-MM-DD.md`).
5. If working in a project repo: that repo's `AGENTS.md` and `STATE.md` if present.
6. `~/ActiveProjects/AGENTS.md` — Nick's personal cross-project rules (R1 long-compute, R2 deploy verification).

## Step 2 — Refresh the repo

```bash
cd ~/ActiveProjects/Cooperation && git fetch --all && git status
```

If `git status` shows the local branch is behind origin, `git pull` before doing anything else.

## Step 3 — Update SYNC.md

Append (don't overwrite) a line to `~/ActiveProjects/Cooperation/SYNC.md` under the right partner's section:

```
- <YYYY-MM-DD HH:MM local> — fetched origin, HEAD at <short sha>, working in <project>
```

Commit this in the same commit as the session's first real change, or in a standalone commit if the session ends up doing nothing else.

## Step 4 — Announce in chat

In your first substantive message, state:
- Which human you're working with (from `PARTNERS.md`).
- Which project repo you're in.
- What you read from STATE.md, the latest journal, and SYNC.md (in particular: when did the *other* partner last sync, and is that recent enough that we should assume their work is reflected in STATE).
- If the other partner pulled within the last hour, mention that — there's a higher risk of concurrent work.

## Step 5 — Proceed with the user's request, under rules A0–A12

Especially:
- A2: write a journal entry before ending the session.
- A3: update STATE.md when in-flight work changes.
- A6: detach long compute.
- A7: verify deploys before claiming "live."
