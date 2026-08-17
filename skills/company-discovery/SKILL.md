---
name: company-discovery
description: "Enumerate private companies that match an acquisition mandate, from public sources — association directories, trade show exhibitor lists, registries, licence rosters, certification registries, review platforms, job boards, sponsor portfolio pages. Records a source for every row and never fabricates a field. Triggers on: find companies, find acquisition targets, build a target list, source companies, company discovery, enumerate the market, find businesses to acquire, who could we buy, expand the target list, find off-market companies."
---

# Company Discovery

Enumerates the mapped population. The quality of this step sets the ceiling on
everything downstream, so it is slow and it is sourced.

**Read first:**
- `references/sourcing-sources.md` — where private companies are findable
- `references/ownership-taxonomy.md` — what you are looking for, and the traps
- `references/scoring-rules.md` — the anti-fabrication rules
- `references/research-ethics.md` — terms of use, personal data

---

## Step 0 — Load the mandate and the map

1. Read `mandate-profile.md`. **If it does not exist:** stop and create it from
   `templates/mandate-profile.md`. A list built without a mandate is a list for
   somebody else's fund
2. Read the market map for this sector. **If there is none:** offer to run
   `market-map` first. Say plainly why: without a map you do not know the segment
   boundaries, the discovery surface, or which sponsors to screen against, and
   the list will have to be rebuilt

### 🚧 HARD GATE — intermediary check

Section 9 of the mandate profile. Principal buyer: proceed. Fee-based
intermediary: STOP, per `references/research-ethics.md`. `TBD` or blank: ask.

---

## Step 1 — Confirm the brief

Restate back, from the mandate and the map:

- Sectors and **segments** in scope, in the map's segment language
- The size box: revenue, EBITDA, check/EV
- Geography, or `No constraint`
- Ownership types that are actionable
- Explicit exclusions, portfolio conflicts, and **who counts as a competitor**
  (ask directly if this is vague — a competing sponsor's platform and a conflict
  with your own portfolio are different things and both matter)
- The named sponsors from the map, for the screen

Ask for a target list size. Recommend **100 to 300** for a first run. If the user
asks for thousands, say plainly why that is worse, then do what they decide.

Wait for confirmation.

---

## Step 2 — Plan the search, then show the plan

Build the plan from the map's discovery surface, weighted to Tier 1 in
`references/sourcing-sources.md`.

A plan for ~200 companies looks roughly like:

| Angle | Method | Rough yield |
|---|---|---|
| Association directories | Member lists, 2 to 4 bodies, plus regional chapters | 40 to 80 |
| Trade show exhibitors | Exhibitor lists, 2 to 3 events, several years | 30 to 60 |
| Registries and licences | State registries, Companies House, licence rosters | 20 to 50 |
| Certification registries | ISO / sector accreditations | 10 to 30 |
| Review platforms and maps | Density sweep per metro for local services | 20 to 50 |
| Local press lists | Business journal fastest-growing and family lists | 10 to 30 |
| Job boards | Active hiring as an operating signal | 10 to 30 |
| Sponsor portfolio pages | Who is gone; the independents around them | 10 to 20 |

**Run several angles.** Each is blind to what the others surface. Good private
companies are frequently visible in exactly one place.

Check each source's terms before working it, and record any source whose terms
prohibit collection in the coverage log rather than working it.

Show the plan. Get a nod. Then go.

---

## Step 3 — Research

One angle at a time. For each candidate, capture only what you can see:

- Company name, domain, HQ location
- Sector and **segment**, in the map's language
- Year founded and employee count, if published
- Where you found it

**Rules while researching:**

1. **`Not found` is correct and expected.** Use it constantly. Never fill a gap
   with a plausible guess
2. **Never infer revenue or EBITDA from headcount** and present it as fact. If you
   estimate, label it and state the basis in the same field
3. **A thin website is normal for a good private company.** Not a negative signal.
   Do not skip a company for looking small online
4. **Quote, do not summarize.** If you cannot quote it, you do not have it
5. **Every row carries its source URL.** No exceptions
6. **Check the domain before merging near-identical names.** Similar names are
   usually different companies
7. **Dead or parked site:** record that as the finding. Do not describe the
   company from memory
8. **Respect robots and terms.** Read pages. Do not bulk harvest sites that
   prohibit it

### The franchise and brand screen

Before a row is kept, check whether the name is a franchise brand. Franchise
locations look exactly like independent local businesses in every Tier 2 source.
Mark them and let `ownership-classification` handle the classification.

### Deduplicate as you go

Match on **domain**, not name. Keep the row with the better source. Record where
the duplicate came from — appearing in three independent sources is itself a mild
positive signal, and it belongs in `notes`.

---

## Step 4 — Write `targets.csv`

Append to the workspace `targets.csv`, creating it from `templates/targets.csv` if
absent.

At this stage you fill: `company`, `domain`, `hq_location`, `sector`, `segment`,
`year_founded`, `employee_count`, `source`, `date_added`. Set `status` to
`identified`.

Fill `est_revenue` and `est_ebitda` only if published, or as a labeled estimate
with the basis stated. Otherwise `Not found`.

**Leave blank for the next steps:**
- `ownership_type`, `ownership_evidence` → `ownership-classification`
- `fit_score`, `fit_reason`, `excluded_by` → `mandate-fit-scoring`
- `signal`, `signal_source`, `evidence_date`, `signal_strength` → `business-research`
- All owner and contact fields → `owner-identification`

Everything unknown is the literal string `Not found`. Never blank, never a guess.

### 🚧 HARD GATE — before writing

Show the user:
- How many rows you are about to add
- How many are new vs. duplicates of existing rows
- The breakdown by segment
- How many are suspected franchise or branded-network locations
- **Five sample rows in full**, so quality can be inspected
- Any angle that produced little or nothing, and why

Get approval. Then write.

---

## Step 5 — Report honestly

```
Discovery run complete

Added:            164 new companies
Duplicates:       19 (already in list)
Total list size:  164

By segment:
  Commercial contract-recurring    88
  Commercial project                41
  Mixed                             22
  Unclear                           13

Evidence quality:
  Founding year sourced            121
  Employee count published          64
  Revenue published                  7
  Revenue Not found                141   (16 labeled estimates)

Flags:
  Suspected franchise locations       9  → ownership-classification
  Dead or parked domain               4

Angles run:      6 of 8
Not run:         Import/export records (sector is services), job boards (deferred)
Weakest angle:   Local press lists (6 rows — city has no book-of-lists feature)
Blocked:         [Directory X] — terms prohibit collection, logged, not worked

Next: ownership-classification on all 164.
```

**Report what did not work.** A silent shortfall reads as full coverage, and that
is the one failure the user cannot detect on their own. If you capped or truncated
anything, say exactly where.

---

## Notes

- **Stop and check in every 50 rows** on a large run. Show a sample. Correcting
  the brief at row 50 is much cheaper than at row 300
- **Volume is not the goal.** 150 well-sourced rows beat 1,500 scraped ones on
  every metric that matters
- **If yield is low, the brief is probably too narrow.** Come back with what you
  are seeing rather than padding the list to hit a number
- **Never score or classify ownership here.** Both have their own skill and their
  own rules, and doing them inline skips the evidence hierarchy and the rubric
- **Update the coverage log** at the end of every run, per `coverage-tracking`
