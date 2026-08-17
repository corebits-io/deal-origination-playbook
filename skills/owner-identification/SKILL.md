---
name: owner-identification
description: "Find the person who can actually sell each target company and a verified route to them — name, role, whether they hold equity, LinkedIn, and an email that is published or verified, never guessed. Marks confidence honestly and prefers warm paths. Triggers on: find the owner, who do I contact, find contacts, verify emails, get owner emails, find the decision maker, contact details, owner contact, who can sell this company, build the contact list."
---

# Owner Identification

Finds the person who can actually sell the company, and a route that reaches
them.

A perfect target list pointed at a plant manager is a wasted campaign. So is a
technically plausible email address that bounces and damages your sending domain.

**Read first:**
- `references/ownership-taxonomy.md` — who can sell, by ownership type
- `references/research-ethics.md` — personal data, no pretexting, no personal-life
  research

---

## Step 0 — Load and scope

1. Read `mandate-profile.md` for geography and jurisdictions (section 9)
2. Read `targets.csv`
3. Filter to `fit_score` = `Strong Fit` or `Fit` only

**Never enrich `Not a Fit` or `Near Miss` rows.** It builds personal data you will
not use, which is both wasted effort and an unnecessary data protection exposure.
Per `references/research-ethics.md`, collect the minimum.

Report how many rows are in scope and ask whether to do all of them or start with
`Strong Fit`.

---

## Step 1 — Identify the right person, before looking for any address

Order matters. An email for the wrong person is worth less than nothing. Use
`ownership_type` and `references/ownership-taxonomy.md`:

1. Owner / Founder / President — founder-owned
2. The family member running operations — family-owned, even if not the largest
   holder. They are the gateway to the rest
3. Managing partner — partner-owned
4. CEO — **only** where the CEO also holds equity. Verify, do not assume from the
   title
5. Trustee-facing CEO — ESOP, understanding the trustee decides
6. Parent corp dev or CFO — corporate-owned. Never the unit's GM
7. Sponsor deal team — PE-backed rows, which should not be in scope at all. If one
   is here, flag it back to scoring

**A hired CEO cannot sell a family business.** Writing to one wastes the first
touch and often delivers your name to the owner with a gatekeeper's framing.

**Where to look, in order:**

1. The company's own site — about, team, history, contact pages
2. Registry filings — officers and registered agents are public and reliable, and
   they carry dates
3. Statutory ownership registers where they exist (UK PSC and equivalents)
4. Licence rosters — often name the licence holder personally
5. Professional profiles
6. Association member listings and committee rosters
7. Local press and award coverage

Second-generation names on a history page are a succession signal. Note them for
`business-research`.

**One contact per company by default.** Small companies talk. Approaching the
owner and the owner's son in the same week reads as a mail merge to both.

### 🚧 HARD GATE — equity check on any CEO or MD

Before recording a CEO or Managing Director as the decision maker, establish that
they hold equity, from a filing or their own public statement. If you cannot,
record the finding as `owner_title` = `CEO (equity not confirmed)` and note that
the actual owner was not identified. Do not present a hired executive as the
person who can sell.

---

## Step 2 — Get a route

In order of what actually works.

### Warm path
If a shared advisor, banker, accountant, association peer, or existing contact
exists, stop here. Record it in `warm_path` and set `owner_route` = `warm intro`.
An introduction converts many times better than the best cold approach.

If the user has a connections export in the workspace, cross-reference it. If they
do not, mention it once: it is the highest-value optional input in the whole
system.

### Email
Only if you have a real one.

**Acceptable sources:**
- Published on the company's own site
- In a registry or licensing filing
- In a trade directory or association listing the owner controls
- Returned by a verification service with a confidence score

**Never acceptable:**
- Guessed from a pattern (`first@domain.com`) without verification
- Inferred because `info@` exists so the owner "probably" does too
- Copied from a purchased list without independent verification

> Pattern-guessing is the fastest way to destroy a sending domain. A high bounce
> rate on a young domain can end your ability to send email at all. One guessed
> address is not worth that. **This system never writes a guessed address.**

### Professional profile
Real but weaker for this audience. Many owners of excellent private companies have
a bare profile or none. Record the URL where it exists; absence is not a negative
signal.

### Published phone or contact form
A real route for offline owners, not a last resort — in some trades it is the best
route available. Record a phone number **only if the company published it**. Never
look up personal numbers.

### Posted letter
For owners with no digital footprint, the registered office address from the
registry is a legitimate, published business address. In some sectors a letter
outperforms everything else.

---

## Step 3 — Record confidence honestly

| `email_status` | Meaning |
|---|---|
| `verified` | Confirmed deliverable by a verification service |
| `published` | Found on the company's own site or an official filing |
| `Not found` | No email located. Honest and common |

There is no fourth value. If a row arrived from an imported list with a
pattern-derived address, mark it `Not found` and note the provenance — do not
launder it into `published`.

`owner_route` takes: `warm intro`, `email`, `phone`, `letter`, `form`,
`Not found`.

---

## Step 4 — Write back to `targets.csv`

Fill `owner_name`, `owner_title`, `owner_linkedin`, `owner_email`, `email_status`,
`owner_route`, `warm_path`. Set `status` to `contact-found`.

Add to `notes` where relevant:
- Contact form or published phone only
- Ownership unclear — could not confirm who can sell
- Sponsor ownership discovered during research → flag back to scoring
- Owner appears to have exited or died — check the filing date
- Multiple family holders, alignment unknown

### 🚧 HARD GATE — before writing

Show:
- Rows about to be updated
- Breakdown by `email_status` and `owner_route`
- **Ten sample rows in full**
- Every company where no owner could be identified at all
- Every row where ownership turned out different from what was scored

Get approval. Then write.

---

## Step 5 — Report

```
Owner identification complete — 66 rows in scope (14 Strong Fit, 52 Fit)

Owner identified:       54  (82%)
No owner found:         12  ← mostly registry-only entities, listed in notes

Route available:
  Warm path exists         5  → route as introductions first
  Email published         21
  Email verified           9
  Professional profile    33
  Phone published         17  (manual only)
  Registered office only   8  (letter route)
  Not found               11

Reachable by email now:    30  (verified + published)
Manual route only:         22  (phone, letter, or form)
Guessed addresses written:  0  ← by design

Flags:
  Actually sponsor-backed        2  → back to mandate-fit-scoring
  Hired CEO, no equity confirmed 6  (real owner found via filings for 4)
  Owner appears to have exited   2  → re-check ownership
  Ownership unclear              3  → needs a human read
```

---

## Notes

- **Never invent an email.** Not once, not for a Strong Fit, not because the
  pattern is obvious. `Not found` is the correct output
- **Verify before any bulk send.** Even published addresses go stale. That send
  happens outside this package
- **Professional footprint only.** No personal-life data, no home addresses, no
  pretexting calls to reception. See `references/research-ethics.md`
- **Treat everything here as personal data.** Regulated in most jurisdictions.
  Keep it in the gitignored workspace and record provenance for every contact
- **Re-check before a second cycle.** Owners retire, sell, and hand over. Contact
  data goes stale faster than target data
- **This skill finds routes. It does not use them.** There is no outreach in this
  package
