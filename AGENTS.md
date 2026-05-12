# Agent Rules — Cooperation

You are an LLM coding agent working inside a two-person collaboration. These rules are **mandatory**. They are written so that **absence implies non-compliance**: if there is no journal entry for your session, we will conclude the session did not happen under these rules, not that you "forgot." Treat each rule as a checklist item you must produce evidence of having followed.

The numbering is stable. When humans cite "A4" they mean rule A4 in this file.

---

## A0: Read these files before doing anything else

At the start of **every** session, in this order:

1. This file (`AGENTS.md`) in full.
2. `STATE.md` in the Cooperation repo — the cross-project snapshot.
3. The last entry in `JOURNAL/` (the most recent dated file).
4. If working in a project repo, that repo's own `AGENTS.md` (which points back here) and its `STATE.md` if present.
5. `~/ActiveProjects/AGENTS.md` — the user's personal cross-project rules (especially R1 "don't block on long compute" and R2 "pushed ≠ deployed"). Those rules apply here too.

If any of these files are missing or stale (last journal entry older than 7 days), say so explicitly in your first message and ask before proceeding.

---

## A1: Identify yourself and the human at the top of every session

In your first substantive message, state:
- Which human you understand yourself to be working with (by name, from `PARTNERS.md`).
- Which project repo you are in (or "meta repo" if working in Cooperation itself).
- What you read from STATE.md and the latest journal entry that's relevant.

This is so the *other* partner, reading later, knows what context you had.

---

## A2: Write a journal entry. Always. This is the load-bearing rule.

Every session produces exactly one journal entry at `JOURNAL/YYYY-MM-DD.md` in the Cooperation repo (append to today's file if it exists, create it if not). The entry must include:

```
## <HH:MM local> — <human name> + <agent label, e.g. "pi/sonnet-4.5">

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
**Deploy status:** "not deployed" | "pushed, deploy unverified" | "deployed <sha> at <time>"
```

Rules about the journal:
- **A2.1** Write the entry **before** ending the session, not "later." Later doesn't happen.
- **A2.2** If you made no progress, write that. An empty session is still a session.
- **A2.3** Never edit or rewrite a prior day's entry. Append a correction with today's date and a `Correction:` heading instead. The journal is append-only.
- **A2.4** If you skip the journal entry, the human is entitled to assume you did nothing useful and revert your work. Don't make them have to.

---

## A3: Update STATE.md when in-flight work changes

`STATE.md` is the always-current snapshot of what's open across all projects. Update it whenever:
- You start work on something not already listed.
- You finish or abandon something listed.
- A blocker or open question emerges that the partner needs to see *without* reading the journal.

STATE.md is **not** append-only — it represents *now*. The journal is the history; STATE is the photo.

---

## A4: Branching and PRs

- **A4.1** `main` is protected. Never commit directly to `main` in any project repo. Use a branch named `<initials>/<short-slug>` (e.g. `nm/add-railway-healthcheck`).
- **A4.2** Open a PR for every change, even tiny ones. The PR description must reference the journal entry: `Journal: Cooperation/JOURNAL/2026-05-12.md` (and the section heading).
- **A4.3** If the partner is the reviewer and not available, you may self-merge after CI passes, but the journal entry must say "self-merged, awaiting post-hoc review by <partner>."
- **A4.4** Agent-authored commits use a `Co-authored-by:` trailer naming the agent and model, e.g.:
  ```
  Co-authored-by: pi-agent (claude-sonnet-4.5) <agent@cooperation.local>
  ```
  This makes blame auditable later.

---

## A5: Secrets — never in the repo, ever

- **A5.1** Every project has a committed `.env.example` listing every required variable with a placeholder *and* a comment saying where the real value lives (e.g. `# Railway env var, project "foo"` or `# macOS Keychain item "openai-personal"`).
- **A5.2** Real `.env` files are gitignored. Never `git add` one. If you find one tracked, stop and tell the human.
- **A5.3** Never write a value matching obvious secret patterns (`sk-...`, `ghp_...`, `AKIA...`, JWTs, anything 32+ char base64-ish next to the word "key"/"token"/"secret") into any tracked file, including journal entries. If you need to refer to a secret, refer to its *location*.
- **A5.4** Deploy-time secrets for Railway-watched repos live in the Railway project's env vars. Record *which* Railway project/service in the project repo's README under "Deployment".
- **A5.5** Pre-commit hook with `gitleaks` is the backstop, not the primary defense. You are the primary defense.

---

## A6: Don't block the conversation on long compute (mirrors `~/ActiveProjects/AGENTS.md` R1)

Anything expected to exceed ~30 seconds runs detached:

```bash
nohup <command> > /tmp/<task>.log 2>&1 &
echo "pid: $!"
```

Then return to the conversation. Poll later in short tool calls. Do **not** sit in a synchronous wait. The journal entry must note any background processes still running at session end, with their PIDs and log paths, so the partner can find them.

---

## A7: "Pushed" is not "deployed" (mirrors `~/ActiveProjects/AGENTS.md` R2)

When stating that work is live, verify against the deployed system, not against `git log`. For Railway projects:

```bash
git push
railway status        # or: railway deployment list | head -3
# Compare deployed SHA to: git rev-parse HEAD
```

In the journal, the "Deploy status" line must be one of:
- `not deployed` — no push or no auto-deploy expected
- `pushed <sha>, deploy unverified` — pushed but you didn't check Railway
- `deployed <sha> at <HH:MM>, verified via <method>` — you checked

Never claim "live" / "shipped" / "in prod" without the third form.

---

## A8: Don't-touch zones

Without explicit human instruction, do not modify:
- Lockfiles (`package-lock.json`, `uv.lock`, `Cargo.lock`, `poetry.lock`) — only as a side effect of an intentional dependency change.
- Generated files (anything under `dist/`, `build/`, `*.generated.*`, files with a "DO NOT EDIT" header).
- Vendored third-party code.
- Migrations that have already been applied in production.
- Another agent's open branch.

If you think one of these *needs* to change, raise it as an Open Question in the journal and stop.

---

## A9: Definition of done

A task is "done" only when **all** of:
1. Code change exists on a branch.
2. Tests for the change exist and pass locally.
3. Linter/formatter pass (project's configured one; don't introduce new ones unilaterally).
4. PR is open with a description linking the journal entry.
5. STATE.md updated.
6. Journal entry written.
7. If the change should be deployed: deploy is verified per A7.

If you stop short of any of these, the task is "in progress," not "done." Say so plainly.

---

## A10: When in doubt, ask in the journal, don't guess

If you encounter a decision the human didn't specify and it's not obvious from existing code, **don't guess and proceed silently**. Add it to "Open questions / for partner" in the journal and either:
- Pick the lowest-risk reversible option and note that you did so, or
- Stop and surface it before going further.

The partner reading the journal later should never be surprised by a non-trivial decision they didn't see.

---

## A11: Decision records for non-trivial choices

For anything that will be hard to reverse (framework choice, schema shape, deploy target, auth model, API contract), write a short ADR in `DECISIONS/NNNN-slug.md` using `templates/ADR_TEMPLATE.md`. Number monotonically. Reference it from the journal entry.

---

## A12: Multi-agent etiquette (you are not the only agent)

The other partner's agent may be working concurrently. To avoid stomping:

- **A12.1** Before starting work, `git fetch --all` and read STATE.md. If STATE.md says the other partner is touching the same file/area, post an Open Question and pick something else or coordinate.
- **A12.2** Long-running branches: rebase on `main` daily; if there's a conflict in a file the other agent owns per STATE, do not resolve unilaterally.
- **A12.3** Never force-push a branch that isn't yours.

---

## Quick checklist (paste into your final message of a session)

```
[ ] A0 read: AGENTS.md, STATE.md, latest journal, ~/ActiveProjects/AGENTS.md
[ ] A1 identified human + project at session start
[ ] A2 journal entry written at JOURNAL/YYYY-MM-DD.md
[ ] A3 STATE.md reflects current reality
[ ] A4 branch + PR (or noted self-merge)
[ ] A5 no secrets in tracked files
[ ] A6 no long synchronous waits; background PIDs logged
[ ] A7 deploy status stated honestly
[ ] A9 definition-of-done items accounted for (done or explicitly deferred)
```
