---
name: coverage-tracking
description: "Track what of the mapped market has actually been covered and what has not — by segment, geography, and source — plus pipeline counts, honest shortfalls, and the rescore queue. Answers 'have we really covered this market or does it just feel like it?' Triggers on: coverage, how much of the market have we covered, what have we not searched, sourcing status, where are the gaps, coverage log, what's left to source, origination status, weekly sourcing summary, what needs rescoring."
---

# Coverage Tracking

Gives the origination effort a memory. Without it, the same three directories get
worked four times and half the map never gets touched — and it all feels like
progress.

**Read first:**
- `references/market-map-method.md` — the map is what coverage is measured against
- `references/sourcing-sources.md` — the source types being tracked

---

## Step 0 — Load

1. The market map for the sector — segments, population estimates, discovery
   surface
2. `coverage-log.md` in the workspace, creating it from
   `templates/coverage-log.md` if absent
3. `targets.csv`

**If there is no market map:** coverage cannot be measured, because there is no
denominator. Say that plainly and offer to run `market-map`. Do not invent a
population estimate to fill the gap.

---

## Step 1 — Compute what can be computed

From `targets.csv`, count and never estimate:

- Rows per segment
- Rows per region
- Rows per `status`: `identified`, `classified`, `scored`, `briefed`
- Rows per `fit_score` bucket
- Rows per `ownership_type` in the keep pile
- Rows per `email_status` and `owner_route`
- Rows per source

From the map, take the population estimates. **Label them as estimates with the
map's stated method every time you use them.** A coverage percentage against an
estimated denominator is direction, not measurement, and presenting it as
measurement is the exact failure this skill exists to prevent.

---

## Step 2 — Establish source status

For every source in the map's discovery surface, one status:

| Status | Meaning |
|---|---|
| `not started` | Never worked |
| `in progress` | Partially worked, more available |
| `worked` | Worked through once, yield recorded |
| `exhausted` | Nothing new left in it |
| `blocked` | Technically inaccessible |
| `terms prohibit` | Terms of use prohibit collection. **Never retried** |

`terms prohibit` is permanent and carries a reason and a date, so nobody
re-attempts a source that should not be worked. See
`references/research-ethics.md`.

Any source in the map with no status is `not started` — surface it as a gap, not
as coverage.

---

## Step 3 — Name the gaps

The section that stops silent truncation from reading as coverage. For each gap:
what it is, why it exists, what leaving it costs, and a priority.

Gap types to check for explicitly, every time:

- **Segments** in the mandate that are `not started` or under 30 percent
- **Regions** in scope with few or no rows
- **Sources** on the map never worked
- **Rows stuck at a status** — identified but never classified, scored but never
  briefed
- **Anything capped, sampled, or truncated** in a previous run, and where
- **`Not found` clusters** — a segment where ownership could not be established
  for most rows usually means the wrong source was used, not that the data does
  not exist

---

## Step 4 — Build the rescore and refresh queue

What is stale, why, and when it is due:

| What | Staleness rule |
|---|---|
| Near Miss rows | Whenever the mandate changes, especially the size floor |
| Sponsor screen on the keep pile | Every 60 to 90 days — add-on announcements land constantly |
| Signals over 18 months old | Recency bands in `references/signals-and-evidence.md` |
| Contact data | Before any second cycle |
| Market map section 3 | Every 60 to 90 days; the rest, 6 to 12 months |
| Rows blocked from Strong Fit by a missing signal | After every research batch |

---

## Step 5 — Update the log and report

Write `coverage-log.md` with all sections updated and a dated session-log row.

### 🚧 HARD GATE — before writing

Show the computed counts, the source status table, and the gap list. Get approval.
Then write. Never delete a previous session-log row — the history is the value.

```
Coverage — Commercial fire & life safety, Southeast US
Updated 2026-08-17

SEGMENT COVERAGE (against map estimates, method in market-map)
  Commercial contract-recurring   ~180 of ~240 est.   75%   worked
  Commercial project               ~40 of ~400 est.   10%   partial
  Residential                      out of scope
  Mixed                            ~22 of ~90 est.    24%   partial

SOURCE STATUS (9 sources on the map)
  worked            4
  in progress       1
  not started       3   ← the real gap
  terms prohibit    1   (logged 2026-08-02, never retry)

PIPELINE
  Identified 164 → Classified 139 → Scored 145 → Briefed 14
  Strong Fit 14 · Fit 52 · Near Miss 41 · Not a Fit 38
  Keep pile ownership: founder 61, family 38, partner 12, Not found 25
  Reachable now: 30 by email, 22 manual route only

GAPS, ranked
  1. Three Tier 1 sources never worked (2 licence rosters, 1 certification
     registry) — est. 60-100 companies, the highest-yield remaining work
  2. Commercial project segment at 10% — decide whether it is in mandate at all
     before spending more here
  3. 25 rows with ownership Not found — all from Tier 2 sources only; the state
     registry was not checked for these
  4. Georgia and Alabama: 6 rows between them vs. ~70 est. population

CAPPED OR TRUNCATED IN PREVIOUS RUNS
  - Map density sweep stopped at 3 of 7 metros (2026-08-10) — not coverage

RESCORE / REFRESH QUEUE
  - 23 rows blocked from Strong Fit by missing signal → due now
  - Sponsor re-screen on the 66-row keep pile → due 2026-10-15
  - Market map section 3 → due 2026-10-15

THE COVERAGE SENTENCE
  "We have enumerated ~180 of an estimated 240 companies in the commercial
  contract-recurring segment in the Southeast, from 5 of 9 sources on the map,
  and the biggest untouched gap is the two state licence rosters."
```

---

## Notes

- **Never present an estimated coverage percentage as a measurement.** State the
  method or do not state the number
- **A gap you did not name is a gap the user thinks does not exist.** This skill's
  whole job is to make shortfalls visible
- **`terms prohibit` is permanent.** Record it once, honour it forever
- **The coverage sentence is the test.** If you cannot fill it in from the log, the
  log is out of date — and "it feels like we've covered it" is exactly the belief
  this file exists to disprove
- **Run this at the end of every session.** It takes two minutes and it is what
  makes the next session start in the right place
