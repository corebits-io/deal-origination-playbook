---
name: business-research
description: "Research each target company properly before anyone speaks to it — what the business does, scale evidence, tenure and history, succession and ownership-change signals quoted and dated, what the owner appears to care about, and an explicit list of what is not known. Produces a one-page target brief per company. Triggers on: research this company, research the owners, target brief, brief me on, pre-call research, succession signals, deal brief, prepare for the call, what do we know about this company, read the signals."
---

# Business Research

Produces the one page you take into a first conversation: what this company is,
what the evidence says, what the signal is, and — the part that matters most —
what you do not know.

**Read first:**
- `references/signals-and-evidence.md` — signal classes, the evidence standard,
  what is noise, the line you do not cross
- `references/ownership-taxonomy.md` — ownership context and succession dynamics
- `references/research-ethics.md` — public professional sources only
- `references/scoring-rules.md` — anti-fabrication rules

---

## Step 0 — Load and scope

1. Read `mandate-profile.md` — section 2 for the thesis, section 10 for what the
   user is cleared to say about themselves
2. Read the market map — the brief must describe the company in the map's segment
   language
3. Read `targets.csv`
4. Filter to `fit_score` = `Strong Fit` or `Fit`

**Never brief a `Not a Fit` or `Near Miss` row.** If the user asks for one
specifically, do it and say why the row is not in the keep pile.

Ask how many to brief. **Recommend 10 to 20 at a time.** A brief is 30 to 60
minutes of real research, and a rushed brief is worse than none — it produces a
confident first conversation built on inference.

---

## Step 1 — Research the business

Sources, in order of value:

1. The company's own site — services, segments, locations, history, team
2. Registry filings — formation, officers, changes, addresses
3. Licence and certification rosters — dated proof of operating standard
4. Association listings and committee roles
5. Trade press and local press — anniversary pieces, award profiles, expansion
   coverage
6. Job postings — what they are hiring tells you what they are doing
7. Review platforms — volume and age, for scale and tenure proxies
8. Procurement and contract award records, where public

**What to establish:**

| Field | Standard |
|---|---|
| What it does | In the map's segment language, no unsourced adjectives |
| Scale | Published figure, or labeled estimate with basis, or `Not found` |
| Ownership | Already classified — verify it still holds, note if it changed |
| Tenure and history | Dated events with sources |
| Locations | Opened, closed, or acquired, with dates |
| Structural changes | Name changes, new entities, holdco insertions |

**Rules:**

1. **Quote, do not paraphrase**, anything you will treat as a signal
2. **Never infer financials from headcount** and present them as fact
3. **A dated website is not a finding about the business.** See the non-signal
   table in `references/signals-and-evidence.md`
4. **Record what you checked and found nothing in.** That belongs in the brief
5. **Date everything.** `evidence_date` on every claim that has one

---

## Step 2 — Read the signals

Work the four classes in `references/signals-and-evidence.md`:

- **A. Succession** — tenure with no visible successor, retirement language, a
  step back to Chairman, a second generation visibly present or visibly absent,
  association roles handed over
- **B. Ownership change** — officer changes, PSC updates, new registered agent, a
  holdco inserted, share transfers, name changes
- **C. Operating change** — new facility, certification added, hiring burst, large
  contract, capability added
- **D. Stress** — licence lapse, closure, overdue filings, litigation of record

**For each signal found:** the exact quote or filed fact, the URL, and the date.
All three, or it is `Not found`.

**Score `signal_strength`** per the table in
`references/signals-and-evidence.md` — `high`, `medium`, `low`, or `Not found`.

### 🚧 HARD GATE — the inference line

Before recording any signal, check it against this list. If it comes from any of
these, **do not record it and do not mention it**:

- An inference about anybody's health, age, or family circumstances
- A personal social media account
- Anything obtained by pretexting — posing as a customer, supplier, applicant, or
  journalist
- Family members who are not in the business
- A photograph read for age or infirmity

A signal is something a person **said or filed in public, in a professional
context**. Beyond the ethics, inferred personal signals are usually wrong, and
acting on one in a first conversation is unrecoverable.

Also check independence: three articles quoting one press release are **one**
signal, not three. Record it once and cite the primary source.

---

## Step 3 — Write the brief

Use `templates/target-brief.md`, one file per company, into `briefs/` in the
workspace. Every section, including:

- **Three specifics only someone who read about them would know.** Not flattery,
  not generic sector observations. Concrete facts about this company
- **Questions to ask** — the real ones this research raised and could not answer.
  Not a discovery checklist
- **What we do not know** — explicit, itemized, and never filled in with an
  inference at the last minute

> The last section is the point of the whole document. A brief that hides its gaps
> produces a confident conversation built on an invention, and owners in small
> sectors remember that.

Keep the brief to one page of substance. Length is not thoroughness; a brief
nobody reads before the call has failed.

---

## Step 4 — Write back to `targets.csv`

Fill `signal`, `signal_source`, `evidence_date`, `signal_strength`, and set
`brief_status` = `briefed` and `status` = `briefed`.

Update `est_revenue` / `est_ebitda` **only** with a published figure or a labeled
estimate with the basis stated inline.

If research contradicted the earlier classification — sponsor ownership found,
family rather than founder, a different segment — say so loudly and flag the row
back to `ownership-classification` or `mandate-fit-scoring`. Do not quietly
overwrite a scored row.

### 🚧 HARD GATE — before writing

Show:
- Which companies you briefed
- **One complete brief in full**, so the user can judge the standard
- The signal found for each, with strength, quoted
- Every company where you found no signal at all
- Every contradiction with the existing row
- Anything you checked and could not establish

Get approval. Then write.

---

## Step 5 — Report

```
Business research complete — 14 companies briefed

Signals found:
  high        4   (2 owner-stated succession, 2 filed ownership change)
  medium      6   (long tenure + no visible successor, both sourced)
  low         2   (operating change only)
  Not found   2   ← approach on mandate fit and merit, no angle

By class:
  A succession        7
  B ownership change  3
  C operating         5
  D stress            1   (overdue filings — diligence note, not an angle)

Evidence recency:
  Under 12 months     8
  1-3 years           4
  Over 3 years        0   ← none presented as current intent

Rejected as non-signals:      11
  (dated websites 4, no profile 3, small headcount 2, sector consolidation 2)
Rejected on the inference line: 2
  (an inferred retirement age, a personal social post — neither recorded)

Contradictions found:
  [Company A] — holdco inserted 2025, likely sponsor deal → back to classification
  [Company B] — second generation runs ops → family-owned, not founder-owned

Scale evidence:
  Revenue published    2
  Labeled estimate     6
  Not found            6

Re-score recommended: 10 rows now have a sourced signal and may reach Strong Fit.
```

---

## Notes

- **Fit and signal are different questions.** This skill answers the second. Never
  let a strong signal argue a company into the mandate
- **`Not found` on signal is fine.** It means you go on mandate fit and general
  merit rather than a specific angle. It does not lower `fit_score`
- **Recency bands matter.** A 2018 quote about retiring soon is a 2018 fact — and
  if it happened, the company may be somebody's add-on now. Check
- **Re-score after a research batch.** Rows blocked from Strong Fit only by a
  missing signal can now be reassessed
- **Briefs go stale.** Re-check before any second cycle
- **Never commit briefs.** They hold personal data and later conversation notes.
  The `.gitignore` covers the workspace patterns; keep it that way
- **This is where the playbook stops.** No outreach copy, no sequences, nothing
  sent. If the user wants that, point them at
  `corebits-io/deal-origination-system`
