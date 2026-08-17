---
name: ownership-classification
description: "Establish who actually owns each company on the target list — founder-owned, family-owned, partner-owned, sponsor-backed, franchisee, ESOP, corporate — from registries, filings, and the company's own statements, never from branding. Runs the sponsor screen that catches add-ons still using founder-era marketing. Triggers on: who owns this company, classify ownership, is this family owned, is this founder owned, is this PE backed, sponsor screen, check ownership, identify family businesses, is this company already owned."
---

# Ownership Classification

Establishes who owns each company, because that decides who can sell it and how
long it will take.

This is the step that most target lists skip, and the guess it leaves behind
propagates into every later step. A company that cannot sell to you is a wasted
approach and a false pipeline entry.

**Read first:**
- `references/ownership-taxonomy.md` — the types, the evidence hierarchy, the traps
- `references/scoring-rules.md` — anti-fabrication rules
- `references/research-ethics.md` — public professional sources only

---

## Step 0 — Load and scope

1. Read `mandate-profile.md` — section 7 for ownership types in scope, section 8
   for exclusions and the known sponsor list
2. Read `targets.csv`
3. Filter to rows with `status` = `identified` and `ownership_type` blank or
   `Not found`

Report how many rows are in scope. On a large list, offer to work in batches of 50
so the user can inspect early quality.

---

## Step 1 — Work the evidence hierarchy, top down

For each company, stop at the strongest tier you can reach and record which tier
you used in `ownership_evidence`.

| Tier | Where to look |
|---|---|
| 1 | UK PSC register, EU beneficial ownership registers, equivalent statutory registers |
| 2 | Registry officer and shareholder filings, annual returns, registered agent records |
| 3 | Acquisition or recap press releases, sponsor portfolio pages |
| 4 | The company's own current statements about its ownership |
| 5 | The owner's own public professional profile stating ownership or founding |
| 6 | Trade or local press describing ownership — weak, needs a second source |

**Never tier:** website tone, branding age, "family owned since 1987" copy, design
quality, or the absence of a sponsor mention.

Two independent tier-6 sources do not equal a tier-2 fact. If they disagree, the
answer is `Not found` with both recorded in `notes`.

---

## Step 2 — Run the sponsor screen on every row

Mandatory, before any classification is written. The company's own website will
not tell you.

```
"[company]" acquisition OR acquired OR "portfolio company"
"[company]" "private equity" OR sponsor OR recapitalization
"[company]" "has been acquired by" OR "joins" OR "partners with"
```

Then check the named sponsors from the market map and mandate section 8 against
their portfolio and add-on pages directly.

**What to look for beyond a press release:**

- A holding company newly inserted above the operating entity in filings
- A registered agent that serves a sponsor's other portfolio companies
- Board appointments with private equity firm affiliations
- A footer copyright naming a parent entity that is not the trading name
- Careers or benefits pages referencing a group or family of companies

Record the screen result for every row, including the clear ones. "Screened,
clear, [date]" is a finding.

> Add-ons keep founder-era branding for years and score highest on naive
> family-owned matching. This screen is the highest-value thing in the skill.

---

## Step 3 — Separate founder-owned from family-owned

It changes who you talk to and how long the process takes, so do not collapse
them. Useful tells, each requiring a source:

| Tell | Points to |
|---|---|
| Single officer since formation, still serving | founder-owned |
| Multiple officers sharing a surname in filings | family-owned |
| "Our story" page naming a second generation | family-owned |
| Founded 40+ years ago, named president is not the founder | family-owned or professionally managed — verify which |
| Officer appointment dates clustered a generation apart | family-owned |
| A named founder plus unrelated minority officers | founder-owned with partners |

**Shared surname alone is not proof.** Verify against filings.

Where it is family-owned, record in `notes` which family members appear in filings
and which appear to run operations. `owner-identification` needs both.

---

## Step 4 — Classify, or do not

Write exactly one value from `references/ownership-taxonomy.md` into
`ownership_type`, plus the evidence tier and source in `ownership_evidence`.

**`Not found` rules:**

- Use it whenever tiers 1 to 5 gave you nothing
- It is expected on 10 to 20 percent of a list
- It does **not** mean "probably founder-owned"
- A `Not found` row cannot become `Strong Fit` later. Note what you checked so
  somebody can finish the job by hand

### 🚧 HARD GATE — before writing

Show the user:
- Rows about to be updated
- Breakdown by `ownership_type`
- Breakdown by evidence tier used
- **Every row where the sponsor screen fired** — these are exclusions and they
  matter most
- **Ten sample rows in full**, including at least two `Not found`
- Any row where the website says one thing and the filings say another

Get approval. Then write. Set `status` to `classified`.

---

## Step 5 — Report

```
Ownership classification complete — 164 rows in scope

Classified:            139  (85%)
Not found:              25  (15%)  ← normal, listed with what was checked

By type:
  founder-owned          61
  family-owned           38
  partner-owned          12
  PE-backed (add-on)     14   ← sponsor screen caught these
  PE-backed (platform)    5
  franchisee              7
  corporate-owned         2
  Not found              25

Evidence tiers used:
  Tier 1 (statutory register)    18
  Tier 2 (registry filings)      71
  Tier 3 (press / portfolio)     19
  Tier 4 (company statements)    24
  Tier 5 (owner profile)          7
  Tier 6 + second source          0

Sponsor screen:
  Run on:        164 of 164
  Fired:          19  → Not a Fit at scoring
  Of which still marketing as "family owned":  11   ← the whole point of the screen

Website contradicted filings:  6  (all 6 were add-ons)

Next: mandate-fit-scoring on the 145 non-excluded rows.
```

---

## Notes

- **Never classify from the website's tone.** The most common failure in the whole
  playbook, and it fails in the direction that wastes the most effort
- **A franchise brand name is the tell.** Check the name against franchisor
  location finders before classifying a local services business as independent
- **Registry data is dated.** An officer list from a 2019 filing describes 2019.
  Record the filing date in `ownership_evidence`
- **An owner who has died or exited** shows up as a registry change, not on the
  website. Check the date on any single-officer record older than a few years
- **Do not enrich contacts here.** That is `owner-identification`, and it only
  runs on rows that survive scoring
- **Personal data discipline applies from this step on.** Officer names are
  personal data. Keep them in the gitignored workspace
