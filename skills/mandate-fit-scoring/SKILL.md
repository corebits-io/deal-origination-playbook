---
name: mandate-fit-scoring
description: "Score every company on the target list against the investment mandate using a written rubric the user approves first, applied identically to every row, then audited for false negatives and missed sponsor conflicts. Produces Strong Fit / Fit / Near Miss / Not a Fit with a reason string per row. Triggers on: score the list, score against my thesis, rank targets, qualify targets, fit scoring, which targets fit, rescore, score this CSV, prioritise the target list, qualify my list."
---

# Mandate Fit Scoring

Turns a list of companies into a list of decisions. One bucket per company, one
reason string per bucket, the same rubric applied to every row.

**Read first:**
- `references/scoring-rules.md` — the buckets, the hard rules, the audit
- `references/ownership-taxonomy.md` — which types are actionable
- `references/signals-and-evidence.md` — because fit and signal are scored
  separately

---

## Step 0 — Load and scope

1. Read `mandate-profile.md`. **If it does not exist:** stop and create it from
   `templates/mandate-profile.md`. Scoring without it invents a mandate
2. Read the market map, for the segment language and the sponsor list
3. Read `targets.csv`
4. Scope: rows with `status` = `classified`, or any row whose `fit_score` is blank

**If `ownership_type` is blank across many rows:** stop and run
`ownership-classification` first. Ownership gates scoring per hard rule 7, and
scoring without it produces a list you have to re-score.

### Scoring an imported list

If the user has their own CSV, map their columns to the schema in
`templates/targets.csv` first and show them the mapping. Anything you cannot map
becomes `Not found`, never an inference from an adjacent column.

---

## Step 1 — Build the rubric in writing

Before scoring anything, write the rubric out from the mandate profile. Every
criterion gets a name, a source in the profile, a test, and a bucket effect.

```
RUBRIC — [sector] — built [date] from mandate-profile.md [date]

HARD EXCLUSIONS (any one → Not a Fit, record excluded_by)
  H1  ownership_type in {PE-backed (platform), PE-backed (add-on), public}
  H2  ownership_type not in mandate section 7 in-scope list
  H3  company appears in mandate section 8 exclusions or portfolio conflicts
  H4  company owned by a sponsor named in the market map
  H5  segment explicitly out of mandate (section 4)
  H6  geography outside mandate section 5, where a constraint is stated

SIZE BOX (from section 3)
  S1  verified revenue inside range               → in box
  S2  verified revenue outside range              → Not a Fit
  S3  labeled estimate outside range              → Near Miss
  S4  revenue Not found                           → not a failure; see hard rule 5

MUST-HAVES (section 4)
  M1  [must-have]  → absent and verified: Near Miss
  M2  [must-have]  → absent and verified: Near Miss

STRONG FIT REQUIRES (all three)
  F1  in box and clear on every hard exclusion
  F2  ownership_type actionable and NOT Not found
  F3  a sourced, quotable signal — signal_strength high or medium
```

### 🚧 HARD GATE — rubric approval

Show the rubric in full. Ask specifically about:

- The exclusion list and the sponsor screen — the two most commonly wrong
- Whether `Not found` revenue should really be non-fatal (it should; explain why
  if they push back)
- The Strong Fit bar

Do not score a single row before the user approves the rubric. If they change it
mid-run, hard rule 8 applies: every previously scored row is stale and the whole
list re-runs.

---

## Step 2 — Score every row, identically

Order of operations, per row:

1. **Hard exclusions first.** Any hit → `Not a Fit`, write `excluded_by` with the
   rule ID. Stop
2. **Ownership gate.** Unactionable → `Not a Fit`. `Not found` → cannot be Strong
   Fit, continue
3. **Size box** per S1 to S4
4. **Must-haves** per M rules
5. **Signal check** — read `signal_strength`. If signals have not been read yet,
   the row cannot be `Strong Fit` yet. Mark it `Fit` and flag it for re-scoring
   after `business-research`
6. **Assign the bucket.** Write `fit_reason` naming the specific rule or criterion

**When genuinely torn between Fit and Near Miss, choose Fit.** Per
`references/scoring-rules.md` — the expensive error is excluding a real target on
thin information.

**Never move a row to make the distribution look better.**

---

## Step 3 — Write back

Fill `fit_score`, `fit_reason`, `excluded_by`, and set `status` to `scored`.

Never overwrite a sourced field with an inference while scoring. Scoring reads;
it writes only these three columns and `status`.

### 🚧 HARD GATE — before writing

Show:
- Row count about to be updated
- Distribution across the four buckets
- `excluded_by` breakdown — which rules fired, how often
- **Ten sample rows in full**: three Strong Fit, three Fit, two Near Miss, two Not
  a Fit
- Any row where you had to make a genuine judgment call, listed explicitly

Get approval. Then write.

---

## Step 4 — The four-part audit (mandatory)

Run it every time, including when the numbers look fine. Twenty minutes.

1. **Sample the Strong Fits.** Pull the 10 highest-confidence rows. Open the
   `signal_source` URL and verify the quoted signal actually appears there. Report
   any that do not — that is a fabrication caught, and it is the most important
   thing this audit does
2. **Audit the Not a Fits for false negatives.** Pull 20 at random. If any look
   obviously good, the filter is too tight. Report them by name
3. **Re-run the sponsor and competitor screen against the keep pile.** Anything
   that hits was missed upstream. Fix and note it
4. **Sanity check the distribution** against the healthy ranges in
   `references/scoring-rules.md`. 80 percent Strong Fit means the rubric is
   flattering the user. 5 percent surviving means the sourcing or the rubric is
   wrong. Either way, stop and reread the mandate

Report the audit results whether or not they are clean. An audit that is never
reported is an audit that never ran.

---

## Step 5 — Report

```
Scoring complete — 145 rows scored under rubric [date]

Strong Fit      14   (10%)
Fit             52   (36%)
Near Miss       41   (28%)
Not a Fit       38   (26%)

Exclusions fired:
  H1 sponsor-owned          19
  H2 ownership out of scope   9   (7 franchisee, 2 corporate)
  H3 portfolio conflict       3
  H4 named sponsor            4
  H5 segment out of mandate   3
  H6 geography                0   (no constraint set)

Size box:
  Verified in box            22
  Estimate in box            31
  Revenue Not found          79   ← not scored as failures
  Verified out of box        13

Strong Fit blocked by:
  Ownership Not found        11   → manual review would unlock these
  No signal read yet         23   → re-score after business-research

AUDIT
  1. Strong Fit signals verified at source:   10 of 10  ✓
  2. Not a Fit false negatives:               1 of 20 sampled
       - [Company] — marked Near Miss on segment, is actually in the
         contract-recurring segment. Moved to Fit. Rule M1 wording tightened
  3. Sponsor re-screen on keep pile:          1 new hit → moved to Not a Fit
  4. Distribution:                            within healthy range

Next: business-research on the 14 Strong Fit and 52 Fit rows, then re-score.
```

---

## Notes

- **The rubric is the deliverable as much as the scores are.** Save it in the
  workspace as `rubric-[sector]-[date].md` so a score can be argued with later
- **Fit and signal are separate questions.** Never let a strong signal drag an
  out-of-mandate company into Fit, and never let a missing signal push an
  in-mandate company down. Hard rule 9
- **Near Miss is a keep, not a reject.** Mandates widen and companies grow.
  Re-scoring a kept row costs nothing
- **Re-score after every mandate change.** Offer to do it whenever the user edits
  the mandate profile
- **Never score during discovery.** The rubric exists so that scoring is
  inspectable, and an inline judgment call is not
