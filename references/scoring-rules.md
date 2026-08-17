# Scoring Rules

How to decide whether a company belongs on your target list. Read this before
`mandate-fit-scoring` runs.

These rules exist because naive scoring gets private companies wrong in a
specific, predictable direction: it rewards companies that market well and
punishes companies that operate well, which is exactly backwards for a buyer.

---

## The four buckets

Every company lands in exactly one. The `fit_score` column in `targets.csv`
takes exactly these values.

### Strong Fit
Inside the mandate box on every dimension you can verify, **and** carrying a
documented signal that makes it more than a category match: a succession signal,
an ownership-change signal, a strategic angle from the mandate profile, or
verified financial scale in range. The signal must be quotable with a source and
a date.

### Fit
Inside the box on the dimensions you can verify, nothing contradicting, no
specific signal beyond category membership. Still worth working.

### Near Miss
Fails one soft criterion, or a key criterion is `Not found` rather than failed.
Too small but growing, right sector wrong subsector, geography one state out.
Kept, because mandates widen and companies grow, and re-scoring a kept row is
free.

### Not a Fit
Fails a hard exclusion: unactionable ownership type, already sponsor-owned, a
competitor conflict, or explicitly outside the mandate. Record which rule fired
in `excluded_by`.

> **Default direction:** when genuinely torn between Fit and Near Miss, choose
> Fit. A slightly loose list costs you a few ignored approaches. A tight filter
> applied to thin information costs you the owner who would have taken the call.
> Be strict only where a hard rule below says to be strict.

---

## Hard rules

Non-negotiable. Each exists because it was gotten wrong first.

### 1. Sponsor-owned companies are Not a Fit

PE-backed (platform) and PE-backed (add-on) rows cannot sell to you off market.
Screen explicitly — press releases, sponsor portfolio pages, recapitalization
announcements — because the company's own website will not tell you.

This is the single most common miss, because add-ons keep their founder-era
branding for years and score highest on naive "family owned" matching.

### 2. Competitor conflicts are Not a Fit

Two shapes. A company already owned by a competing sponsor in your sector is
their deal, not yours. A company that competes directly with your existing
portfolio creates a conflict you must not research or contact under the cover of
buying interest. Check the exclusions section of the mandate profile and record
`excluded_by` when the rule fires.

### 3. A thin website is not a negative signal

Excellent private companies have websites from 2011, or none at all. They are
busy operating. Score on registry facts, licenses, tenure, reviews, hiring, and
certifications — never on design quality, copy polish, or whether the site
"feels" like a real business.

> This rule has the highest cost when broken. Surface-signal scoring inverts the
> result in this market: the best-run 30-year-old business in the sector often
> has the worst website, and the venture-funded competitor burning cash has the
> best one.

### 4. Never infer financials from headcount and present them as fact

Revenue per employee varies by an order of magnitude across sectors and by
several times within one. If you estimate, label it: `est_revenue` and
`est_ebitda` carry the basis inline ("estimate: 40 staff at sector-typical
revenue per head, unverified") or they carry `Not found`. An estimate presented
as a fact is a fabrication with extra steps.

### 5. Unknown is not failed

A `Not found` revenue is not a failed size test. Unknown is Near Miss territory
at worst, and usually just a flag for further research. Only a verified figure or
a well-based estimate can fail the size box.

### 6. Do not apply constraints the mandate did not set

If the mandate says a region, apply it. If it says no geographic constraint, do
not quietly apply one because a company is far from your office. Same for
subsector, deal type, and size floors.

### 7. Ownership type gates everything

`ownership_type` is scored first. If it is unactionable per
`references/ownership-taxonomy.md`, no other virtue rescues the row. If it is
`Not found`, the row cannot be `Strong Fit`, whatever else is true.

### 8. Every rubric change re-runs the whole list

If you tighten, loosen, or reword a criterion mid-run, every previously scored
row is stale. Re-run all of them under the new rubric. A list scored under two
rubrics is not a list, it is two lists interleaved, and the audit below cannot
catch what that hides.

### 9. Fit and signal are separate questions

Fit is "do we want this company." Signal is "might it move." Never let a strong
signal push an out-of-mandate company into Fit, and never let the absence of a
signal push an in-mandate company to Near Miss. `signal_strength` is its own
column for exactly this reason.

---

## Anti-fabrication rules

Scoring runs across many rows independently. Each row is an opportunity to invent
something plausible. These are mandatory in every research and scoring step.

1. **`Not found` is a valid, expected, and correct answer.** Say it often. An
   empty field is recoverable. A confident wrong field is not
2. **Never infer a fact from a related fact.** Not revenue from headcount, not
   ownership from branding, not an owner's age from a photo, not succession
   intent from years in business alone
3. **Every signal carries its source.** A URL, or a quoted phrase from a named
   page. If it cannot be quoted, it did not happen
4. **Do not merge companies with similar names.** Confirm the domain and the
   location match. Trades and local services reuse names constantly
5. **A press mention is not a fact about the company.** Being quoted in a sector
   article is not evidence of scale, ownership, or intent
6. **If the site is dead, parked, or blocked, record that.** Do not fall back on
   model memory to describe the company
7. **Recency matters.** Record `evidence_date` with every signal. A 2018 award
   profile describes a 2018 company

---

## Deterministic beats clever

Build the rubric in writing from the mandate profile before scoring anything, get
it approved, then apply it identically to every row.

A row-by-row judgment call has no memory of the other rows, so the same company
profile can land in different buckets depending on phrasing. A rule you can read,
argue with, and correct beats a smart guess you cannot inspect, every time.

Keep the reason string attached to every score so you can audit it later.

---

## Required output for every scored row

| Field | Rule |
|---|---|
| `fit_score` | `Strong Fit`, `Fit`, `Near Miss`, or `Not a Fit`. Never blank |
| `fit_reason` | One sentence naming the specific rule or criterion applied |
| `excluded_by` | Which hard rule fired, for every `Not a Fit`. Otherwise `N/A` |
| `signal_strength` | `high`, `medium`, `low`, or `Not found` — scored separately |
| `signal` | The quoted phrase behind the signal, or `Not found` |
| `signal_source` | URL the signal came from, or `Not found` |
| `evidence_date` | When the evidence was published or updated, or `Not found` |

A row without a `fit_reason` is not scored. It is a guess with a label on it.

---

## The four-part audit

After every scoring run, by hand:

1. **Sample the Strong Fits.** Pull the 10 highest-confidence rows and verify the
   quoted signal actually appears at the source URL
2. **Audit the Not a Fits for false negatives.** Pull 20 at random. If any are
   obviously good, the filter is too tight. This is the expensive failure and it
   is invisible unless you look
3. **Re-run the sponsor and competitor screen against the keep pile.** Search
   Strong Fit and Fit rows against known sponsor portfolios and the exclusion
   list. Anything that hits was missed by rule 1 or 2
4. **Sanity check the distribution.** If 80 percent of rows are Strong Fit, the
   rubric is flattering you. If 5 percent survive at all, either the sourcing or
   the rubric is wrong. Both mean stop and reread the mandate profile

Twenty minutes, every run. It is the only thing standing between you and a
confidently wrong list.

---

## A healthy distribution

For a well-mapped sector and a real mandate, roughly:

| Bucket | Share of the list |
|---|---|
| Strong Fit | 5–15% |
| Fit | 25–45% |
| Near Miss | 20–35% |
| Not a Fit | 20–40% |

Wide variance by sector. A consolidated sector produces far more `Not a Fit` on
the sponsor screen alone. Use this as a smell test, never as a quota — never
move a row to hit a shape.
