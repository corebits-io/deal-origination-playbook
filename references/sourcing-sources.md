# Where to Actually Find Private Companies

Sources for `company-discovery`, ordered by signal per hour spent. The good news
about private company sourcing: the best sources are free, public, and ignored,
because everybody else bought the same stale database.

**Before you use any of these:** read the site's terms of use. Many directories
prohibit bulk extraction, and several platforms restrict automated collection
regardless of what is technically possible. Manual research and reading are
almost always fine. Automated harvesting frequently is not. See
`references/research-ethics.md`.

---

## Tier 1 — free, public, high signal

Start here. Companies appear in these sources because they operate, not because
they market. That is exactly the population a proprietary process wants.

### Industry association member directories
Nearly every sector has a trade body, and most publish member lists with
location, specialty, and sometimes year joined. Membership is itself a signal:
these are established operators who pay dues and show up.

Search: `[sector] association members directory`, `[sector] contractors
association [state]`, `[trade body] find a member`.

Regional and state chapters of national associations are often richer than the
national list and far less picked over.

### Trade show exhibitor lists
Public, current, and self-selected for companies healthy enough to buy a booth.
Past years are usually still online, which gives you a longitudinal read: a
company exhibiting five years running is durable.

Search: `[sector] trade show exhibitor list`, `[conference name] exhibitors`,
plus the year.

### Government registries
Mandatory and structured, which makes them the most trustworthy source here.

- **US state Secretary of State registries** — entity name, formation date,
  registered agent, and officers in some states. Formation date fills
  `year_founded` with a real source
- **UK Companies House** — filings, directors with appointment dates, and actual
  ownership through the PSC (persons with significant control) register. The
  closest thing to a free ownership database that exists
- **Other national registries** — Ireland's CRO, Canada's provincial
  registries, and most EU commercial registers publish comparable detail
- **Import/export manifest records** — reveals who actually ships product,
  useful for manufacturing and distribution theses

### Licensing boards
Licensed trades come with public rosters, license issue dates, and disciplinary
records: contractors, electricians, plumbers, HVAC, pharmacies, home care
agencies, funeral homes, staffing agencies in some states. License issue date is
a hard tenure fact with a citable source.

### Certification registries
ISO 9001, AS9100, NADCAP, SOC 2, sector-specific accreditations. A certification
proves the company operates to a standard, and the renewal date gives you an
`evidence_date` for free.

### Sponsor portfolio and add-on pages
Read competing sponsors' portfolio pages and add-on announcements. This tells
you which companies are already gone, which platforms are consolidating your
sector, and what profile they buy. Feed it into the map and into the sponsor
screen in `references/scoring-rules.md`.

---

## Tier 2 — public, noisier, still free

- **Review platforms and map density sweeps** — Google Maps, Yelp, and
  sector-specific review sites. Review count and oldest review date are rough
  proxies for scale and tenure in local services. A map density sweep is the
  fastest way to enumerate every operator of a given type in a metro
- **Job boards** — a company hiring technicians, drivers, or account managers is
  operating and probably growing. Title-and-region searches surface companies no
  directory lists
- **Local business journals** — "fastest growing," "family business awards," and
  "book of lists" features are pre-researched target lists with owner names
  attached
- **Local press and award profiles** — anniversary stories ("celebrating 40
  years") and chamber awards frequently quote the owner on succession directly
- **Supplier and distributor locators** — manufacturers publish
  authorized-dealer and installer finders that enumerate an entire regional
  operator base
- **Procurement and contract award records** — public sector award notices name
  private suppliers, with contract values

---

## Tier 3 — disciplined generic search

The fallback when a sector has no directory culture. Lower yield per hour, still
productive with tight queries.

```
"[sector]" "family owned" OR "founded in 19" [region]
"[sector] company" "[city]" -jobs -franchise
"celebrating * years" "[sector]" [state]
"[sector]" "second generation" OR "third generation"
site:linkedin.com/company "[sector]" "[region]"
"[sector]" "about us" "since 19" OR "since 20"
```

**Ownership screening — run on every candidate before it enters `targets.csv`:**
```
"[company]" acquisition OR acquired OR "portfolio company"
"[company]" "private equity" OR sponsor OR recapitalization
"[company]" "has been acquired by" OR "joins"
```

**Finding the owner:**
```
"[company]" owner OR founder OR president
"[company]" [state] secretary of state
site:linkedin.com "[company]" owner OR president
```

---

## Worked examples

### Commercial HVAC services (local services thesis)
Tier 1: state mechanical contractor license rosters; trade association chapter
directories; manufacturer dealer-locator pages. Tier 2: map density sweep per
metro sorted by review count and oldest review; job postings for service
technicians. **Screen hard** — the sector is heavily consolidated, so run every
candidate against known platform portfolio pages before scoring. Expect a high
add-on hit rate.

### Vertical SaaS (software thesis)
Tier 1: exhibitor lists for the *end customer's* trade shows, because software
vendors exhibit where their buyers are; integration marketplaces and partner
directories of the dominant platform in that vertical. Tier 2: job boards for
implementation and customer-success roles, which signal real revenue; category
review platforms. Screen: check funding history carefully. Bootstrapped vertical
SaaS rarely announces anything, so absence of funding news is weak evidence, not
proof — mark `Not found` and verify.

### Specialty manufacturing
Tier 1: import/export manifest records for the product category; ISO and AS9100
certification registries; association member lists; manufacturing extension
partnership client stories. Tier 2: trade publication "top shops" lists; job
postings for machinists and quality engineers. Certifications with renewal dates
are the cleanest evidence available in this sector.

### Regulated healthcare services
Tier 1: state licensure rosters and CMS-type provider enumeration files;
accreditation body member lists. Tier 2: local press on ownership changes.
Screen: physician-owned entities, MSO structures, and payer concentration all
change who can sell — classify carefully per
`references/ownership-taxonomy.md`.

---

## Sources to avoid

- **Bought lists of "off-market businesses for sale."** Recycled, stale, and
  contacted by every buyer who paid the same vendor. If a list is for sale to
  you, it is not proprietary
- **Scraped third-party social exports.** Terms problems, data protection
  problems, and quality problems in one purchase
- **Broker listing aggregators presented as proprietary.** Listed businesses are
  fine to look at, but they are marketed deals in a process. Track them
  separately if at all
- **Anyone selling "verified owner emails."** Verified by whom, when, and under
  what right to process the data? The answer is never good

---

## A realistic first pass

For one thesis in one sector: **100 to 300 genuinely qualified companies**, built
over a few days, deduped on domain, every row sourced.

That is enough to run a real origination program and learn which angle works,
and small enough to establish ownership properly and brief each company before
anyone speaks to it.

A list of 2,000 unscreened rows is worse than 150 good ones. It buries the
handful of real succession conversations inside add-ons, franchisees, and
companies that cannot sell — and quality of the list sets the ceiling on
everything downstream.
