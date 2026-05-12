# SYNC — Last-Seen Heartbeats

Each partner's agent appends one line per session-start to its section, recording when it last fetched/pulled origin. **Append-only.** The most recent line per partner tells the *other* partner's agent how stale STATE.md / JOURNAL might be relative to that partner's reality.

Format per line:
```
- YYYY-MM-DD HH:MM <tz> — fetched origin, HEAD <short-sha>, working in <repo>
```

If an agent sees the *other* partner's most recent SYNC entry is within the last ~hour, it should treat concurrent work as plausible and re-read STATE.md immediately before making any non-trivial change.

> Sessions are not expected to overlap — we coordinate first (per rule A12). SYNC is the receipt that proves the coordination happened, and the canary if it didn't.

---

## Nick (jk212h20)

- 2026-05-12 12:30 PT — initial scaffold, HEAD ff17a6f, working in Cooperation (meta)

## _partner_

_no entries yet_
- 2026-05-12 13:10 PT — fetched origin, HEAD 76b7918, working in Cooperation (meta)
