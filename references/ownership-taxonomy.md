# Ownership Taxonomy

Who actually owns the company, and therefore who can actually sell it. Read this
before `ownership-classification` or `owner-identification` runs.

Most bad target lists are bad because ownership was guessed once, early, and
every downstream step inherited the guess. Effort spent on a company that
structurally cannot sell to you is wasted twice: once on the work, and again on
the false pipeline entry.

The `ownership_type` column in `targets.csv` takes exactly the values below.

---

## The evidence hierarchy

Classify from the strongest evidence available, and record which tier you used
in `ownership_evidence`.

| Tier | Source | Strength |
|---|---|---|
| 1 | Statutory ownership register (UK PSC, EU beneficial ownership registers) | Definitive |
| 2 | Registry officer and shareholder filings; annual returns | Strong |
| 3 | Acquisition or recapitalization press release; sponsor portfolio page | Strong for exclusion |
| 4 | The company's own current statements about its ownership | Moderate |
| 5 | Owner's own public profile stating ownership or founding | Moderate |
| 6 | Trade press or local press describing ownership | Weak, needs a second source |
| — | Website tone, branding age, "family owned" marketing copy | **Not evidence** |

Two independent tier-4-or-weaker sources do not add up to a tier-2 fact. They
add up to a `Not found` with notes, if they disagree.

`Not found` on 10 to 20 percent of a list is a normal, healthy outcome. It is
not a failure of the research.

---

## founder-owned

The person who started the business still owns it and usually still runs it.

- **Who can sell:** the founder. One decision maker, sometimes with a spouse or a
  minority partner in the background
- **Who to contact:** the founder directly. Titles: Owner, Founder, President,
  CEO, or just their name on the contact page
- **Process dynamics:** no banker, no process, no board. The sale is a personal
  decision tangled up with identity, employees, and legacy. Timelines are set by
  life events, not fund cycles
- **What to record:** founding date with a registry source, and whether the
  founder still appears in current filings or on the current site
- **Actionable:** yes. This is the core target for most mandates here

## family-owned

Ownership has passed to, or is shared across, a family. Often second or third
generation.

- **Who can sell:** it depends, and finding out *is* the research task. There may
  be one patriarch or matriarch with control, or five siblings with equal stakes
  and unequal interest
- **Who to contact:** the family member who runs the business day to day, even if
  they are not the largest holder. They are the gateway to the others
- **Process dynamics:** slower than founder-owned. Internal alignment has to
  happen before any external conversation gets serious
- **Succession is the signal.** A second generation visibly in the business, or
  visibly absent from it, is the most useful thing research can establish here
- **What to record:** generation number if stated, which family members appear in
  filings, and which run operations
- **Actionable:** yes, with patience

### Telling founder-owned and family-owned apart

It matters, because it changes who you talk to and how long it takes. Useful
tells, all requiring a source:

- Registry filings listing multiple officers with the same surname → family
- A single officer since formation, still serving → founder
- "Our story" or history pages naming a second generation → family
- The founding date is 40+ years ago and the named president is clearly not the
  founder → family, or professionally managed; verify which
- Shared surname alone is not proof. Verify against filings

## partner-owned

Two or more unrelated partners. Common in professional services, agencies,
practices, and trades.

- **Who can sell:** all of them, together. A partnership agreement usually
  governs and you will not see it
- **Who to contact:** the managing partner first. Assume the others read over
  their shoulder
- **Process dynamics:** partial exits and partner buyouts are common asks. Expect
  internal disagreements you cannot see from outside
- **Actionable:** yes, but score the added complexity honestly

## PE-backed (platform)

A sponsor already owns it as a platform investment.

- **Who can sell:** the sponsor, on the sponsor's timeline, almost always through
  a banked process
- **Who to contact:** nobody, for proprietary origination. When the sponsor
  sells, you are one bidder in an auction — the opposite of the point
- **What it is useful for:** market intelligence. A platform in your sector tells
  you which thesis a competitor is running and which add-ons they will chase
- **Actionable:** no. Default `Not a Fit`

## PE-backed (add-on)

Already acquired by a sponsor's platform as a bolt-on.

- **Who can sell:** the platform's sponsor. The founder you found on LinkedIn may
  have no equity left at all
- **Who to contact:** nobody. The company sits inside someone else's thesis
- **The trap:** add-ons keep their old name, old website, and old "family owned
  since 1987" copy for years after the sale. Check the footer, the press
  releases, and the sponsor's portfolio page before classifying
- **Actionable:** no

## VC-backed

Venture investors on the cap table, usually with a preference stack.

- **Who can sell:** founders plus a board the founders do not control. The
  preference stack decides whether your price clears anything for anyone
- **Who to contact:** the founder, but only if the mandate genuinely covers
  venture-backed companies. Most buyout mandates do not
- **Actionable:** rarely. Fit only if the mandate profile says so explicitly

## corporate-owned

A subsidiary, division, or business unit of a larger company.

- **Who can sell:** the parent's corporate development function, never the unit's
  general manager, however enthusiastic the GM sounds
- **Who to contact:** corp dev or the CFO at the parent. The GM is useful for
  understanding the business, not for buying it
- **Process dynamics:** carve-outs are real deals but slow, political, and heavy
  on transition services
- **Actionable:** sometimes. Only if the mandate includes carve-outs

## ESOP

Owned wholly or partly by an employee stock ownership plan.

- **Who can sell:** the trustee, under fiduciary duties, at not less than fair
  market value, through a formal process. ERISA governs in the US
- **Who to contact:** the CEO to open a conversation, understanding that the
  trustee decides and a fairness process follows
- **Actionable:** yes for the patient. Do not expect founder-owned dynamics or
  founder-owned speed

## franchisee

Operates under someone else's brand and franchise agreement.

- **Who can sell:** the franchisee, subject to franchisor consent and often a
  right of first refusal you will not see until late
- **Who to contact:** the franchisee owner, after reading the franchisor's
  transfer policy if it is published
- **The trap:** franchise locations look like independent local businesses in
  every Tier 2 source. The brand name is the tell. Classify before enriching
- **Actionable:** only if the mandate is explicitly a franchise roll-up

## public

Listed on an exchange.

- **Actionable:** no, for this playbook. Public targets bring disclosure regimes,
  MNPI handling, and takeover rules this repo does not cover. Mark `Not a Fit`
  with the reason recorded

## Not found

Ownership could not be established from tier 1 to 5 evidence.

- **What it means:** exactly that, and nothing more. It is not "probably
  founder-owned"
- **Consequence:** the row cannot be `Strong Fit`. Flag it for manual review and
  note what you checked

---

## The distinction that breaks most lists

> A company that **is** an independent business can sell itself to you.
> A company that **was** independent and is now a sponsor's add-on cannot, no
> matter what its website still says.

Stale websites are the norm in this market, not the exception. Ownership is a
fact to verify, never a vibe to infer from design quality or copy age.

---

## Decision maker titles, roughly in order

1. Owner / Founder / President
2. CEO / Managing Director — verify they hold equity, not just the title
3. Managing Partner (partner-owned)
4. The family member running operations (family-owned)
5. CFO — a useful entry at larger targets, never the decision maker

Below that you are talking to somebody who can mention you at lunch but cannot
sell you a company. Sometimes that is a deliberate warm-path move. It should
never be an accident of whichever email you happened to find.
