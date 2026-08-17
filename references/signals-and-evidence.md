# Signals and Evidence

What counts as a signal that a company might actually transact, what counts as
evidence for it, and what is noise that list vendors sell as insight. Read this
before `business-research` runs, and before any signal is written to
`targets.csv`.

---

## Fit and signal are different questions

**Fit** answers *do we want this company.* It comes from the mandate.

**Signal** answers *might this company move, and roughly when.* It comes from
what the owner and the filings have said in public.

A list of perfectly-fitting companies with no signal read produces a lot of
polite silence. A list of strong signals outside the mandate produces meetings
you cannot act on. You need both, scored separately, which is why `fit_score`
and `signal_strength` are separate columns.

---

## Signal classes

### A. Succession signals

The most valuable class in this market, and the reason founder and family-owned
businesses are the core target.

- 20+ years in business with no visible successor in the leadership team
- Retirement language in an interview, award profile, or association bio
- The owner stepping back to Chairman or a similar role while a non-family GM
  runs daily operations
- A second generation visibly entering the business — new family-surname officers
  in filings, family members in leadership pages
- A second generation visibly *absent* — children in unrelated professions, per
  their own public profiles
- Long-held association board seats or officer roles handed over
- The owner has publicly discussed selling, exiting, or "what happens next"

### B. Ownership-change signals

Structural, filed, and dated. The most reliable class because the evidence is
statutory.

- Registry officer changes, resignations, or new appointments
- UK PSC register updates, or equivalent beneficial ownership changes
- A new registered agent, or a change of registered office
- A holding company newly inserted above the operating entity
- Share issuance or transfer filings
- Name change, or a `d/b/a` registration

> Note: an ownership-change signal can also disqualify. A new holdco above the
> operating company is often the first visible trace of a sponsor deal. Check
> before you treat it as an opening.

### C. Operating-change signals

The company is doing something, which makes a conversation timelier.

- A new facility, branch, or geographic expansion
- A certification added, or a licence category extended
- A hiring burst, particularly in management rather than line roles
- A large contract or public-sector award
- A capability or product line added
- Equipment or capacity investment mentioned in trade press

### D. Stress signals

Handle carefully. Real information, easy to misuse.

- Licence lapse or disciplinary action on a public roster
- A location closed or an expansion wound down
- Filings overdue at the registry
- Litigation of record

Stress is not a reason to approach an owner differently, and it is never
something to reference in a first conversation. Record it because it affects
diligence and value, not because it is leverage.

---

## Not signals

Things sold as insight that carry no information about whether a company will
transact:

| Non-signal | Why it is noise |
|---|---|
| A dated website | Good private companies have terrible websites. Frequently inversely correlated with quality |
| No LinkedIn presence | Normal for owners over 55 in most trades |
| Small stated headcount | Says nothing about revenue, margin, or quality |
| No press coverage | Most excellent private companies have none, ever |
| "Founded 1985" alone | Tenure is a fact, not an intention. It becomes a signal only with an absent successor or a stated plan |
| A generic email address | Says something about their IT, nothing about their plans |
| Being in a consolidating sector | Applies to every company in the sector equally |

---

## The evidence standard

Every signal written to `targets.csv` carries three things:

1. **`signal`** — the quoted phrase or the specific filed fact. Quote it, do not
   summarize it. If you cannot quote it, you do not have it
2. **`signal_source`** — the URL, or a precisely named document
3. **`evidence_date`** — when it was published, filed, or last updated

A signal without all three is `Not found`.

### Recency bands

| Age of evidence | Treatment |
|---|---|
| Under 12 months | Current |
| 1–3 years | Usable, note the age in the brief |
| Over 3 years | Historical context only. Never present as current intent |

A 2018 quote about retiring "in the next few years" is a 2018 fact. It may have
already happened, and if it did, the company is probably somebody's add-on now.
Check.

---

## Scoring signal strength

| `signal_strength` | Criteria |
|---|---|
| `high` | A class A or B signal, under 18 months old, quoted with a source. Owner-stated intent, or a filed ownership change |
| `medium` | A class A signal inferred from structure rather than statement (long tenure plus no visible successor, both sourced), or a class C signal under 12 months |
| `low` | Class C or D only, or a class A signal over 3 years old |
| `Not found` | No sourced signal. Common and correct |

`Not found` on signal strength does not lower `fit_score`. It means you approach
on mandate fit and general merit rather than on a specific angle.

---

## The line you do not cross

A signal is something a person **said or filed in public, in a professional
context**. It is not:

- An inference about anybody's health, age, or family circumstances
- Anything from a personal social media account
- Anything obtained by pretexting — calling reception as a fake customer,
  supplier, or job applicant
- Anything about family members who are not in the business
- A photograph read for age or infirmity

Beyond the ethics, inferred personal signals are usually wrong, and acting on one
in a first conversation with an owner is unrecoverable. Sectors are small and
owners talk to each other.

See `references/research-ethics.md`.

---

## Cross-referencing signals

Two independent weak signals pointing the same way are worth more than either
alone — but only if they are genuinely independent.

**Genuinely independent:** a registry officer change *and* an association bio
change. Different systems, different dates.

**Not independent:** three news articles that all quote the same press release.
That is one signal with three URLs. Record it once and cite the primary source.

---

## Where signals live

- `signal` / `signal_source` / `evidence_date` / `signal_strength` in
  `targets.csv` — one primary signal per row
- The full signal record, including secondary and historical signals, in the
  target brief from `templates/target-brief.md`
- Recheck before any second cycle. Owners retire, sell, and hand over. A signal
  read is stale faster than you think
