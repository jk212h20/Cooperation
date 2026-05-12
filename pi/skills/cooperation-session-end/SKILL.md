---
name: cooperation-session-end
description: Use when wrapping up a coding session in any repo participating in the Cooperation workflow. Writes the journal entry, updates STATE.md, runs the A0–A12 checklist. Required by rules A2, A3, A9.
---

# Cooperation Session End

When the user signals the session is ending (or you are about to stop being responsive), do this **before** your final message.

## Step 1 — Write the journal entry

Append to `~/ActiveProjects/Cooperation/JOURNAL/YYYY-MM-DD.md` (today's date, local time). Create the file if it doesn't exist. Use this schema exactly:

```
## <HH:MM> — <human name> + <agent label e.g. pi/sonnet-4.5>

**Project:** <repo name or "meta">
**Goal:** <one sentence>

**Did:**
- bullet
- bullet

**Did not / deferred:**
- bullet (with reason)

**Open questions / for partner:**
- bullet

**Next:**
- bullet

**Commits / PRs:** <repo>@<sha> (link if pushed), or "no commits"
**Deploy status:** "not deployed" | "pushed <sha>, deploy unverified" | "deployed <sha> at <HH:MM>, verified via <method>"
```

The journal is **append-only**. Never edit a prior day's entry — append a `Correction:` section in today's entry instead.

## Step 2 — Update STATE.md

If anything about in-flight work changed:
- New thing started → add it to "Active work".
- Thing finished → remove it from "Active work", possibly add a line under "Recent deploys".
- New open question for partner → add to "Open questions for partners".
- Background process still running → note under "Background processes running" with PID and log path.

STATE.md represents *now*. Edit it in place.

## Step 3 — Commit and push

```bash
cd ~/ActiveProjects/Cooperation
git add JOURNAL/ STATE.md SYNC.md
git commit -m "Journal <YYYY-MM-DD>: <one-line summary>

Co-authored-by: pi-agent (<model-id>) <agent@cooperation.local>"
git push
```

If working in a project repo, also push that repo's branch and confirm the PR is open per rule A4.

## Step 4 — Run the A0–A12 checklist in your final message

Paste this exactly and mark each item:

```
[ ] A0 read: AGENTS.md, STATE.md, latest journal, SYNC.md, ~/ActiveProjects/AGENTS.md
[ ] A1 identified human + project at session start
[ ] A2 journal entry written at JOURNAL/YYYY-MM-DD.md
[ ] A3 STATE.md reflects current reality
[ ] A4 branch + PR (or noted self-merge)
[ ] A5 no secrets in tracked files
[ ] A6 no long synchronous waits; background PIDs logged
[ ] A7 deploy status stated honestly
[ ] A9 definition-of-done items accounted for (done or explicitly deferred)
```

If any item is `[ ]` instead of `[x]`, explain why in one line beneath the checklist. **Absence implies non-compliance** — an unchecked item with no explanation will be treated as having been skipped.
