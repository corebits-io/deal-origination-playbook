# Market Map Method

How to map a sector before sourcing in it. Read this before `market-map` runs.

A market map is not a target list and it is not a research essay. It is a
one-to-two-page decision document that makes the next four steps cheaper and
tells you where **not** to look.

Everything in it carries a source. A map built from model memory is a
confident-sounding fiction, and every list built on top of it inherits the
fiction.

---

## The six sections

Every map has exactly these. If a section is genuinely unknowable from public
sources, the section says `Not found` and says what would answer it.

### 1. Segmentation — how the businesses actually run

Not SIC or NAICS codes. Segment by the operating characteristics that decide
whether two companies are comparable:

- Customer type: commercial / residential / industrial / public sector
- Revenue shape: contract-recurring / repeat-transactional / project
- Regulatory status: licensed trade / certified / unregulated
- Delivery model: self-performing / subcontracted / distribution / franchise
- Ownership pattern: owner-operated / professionally managed / branded network

Name three to six segments and write one line each on what a business in it
looks like. Then state plainly which segments the mandate covers and which it
does not.

> Industry classifications group companies by what they sell. Buyers care how
> they earn. Those two produce different segment boundaries, and the second one
> is the useful one.

### 2. Size distribution

Roughly how many companies sit in each size band, and where the mass is. Use
whatever is countable: association member counts, license roster counts, map
density sweeps, published sector statistics.

State the method and mark it as an estimate. "License roster shows 1,240 active
mechanical contractors in the state; a 40-company sample suggests roughly 70
percent are under 20 employees" is a usable finding. "The market is highly
fragmented" is not.

This section decides whether the mandate is transactable at all. A sector whose
mass sits below your size floor needs a roll-up thesis, a lower floor, or a
different sector.

### 3. Fragmentation and consolidation

- Who are the largest players, and are they sponsor-backed?
- Which sponsors hold platforms here? Name them and cite the portfolio page
- What add-on profile are those platforms buying — size, geography, segment?
- Roughly what share of the mapped population is already sponsor-owned?

This is the highest-value section and the one databases never give you. It tells
you which companies are already gone, which thesis your competitors are running,
and which of your future keyword matches will turn out to be add-ons.

Feed the sponsor list straight into the screen in `references/scoring-rules.md`.

### 4. The typical owner

From public professional sources only:

- First, second, or third generation, typically?
- Trade background or professional management?
- What have owners in this sector said publicly about succession, exits, and
  consolidation? Quote two or three
- What do they appear to care about — the team, the name, the customers,
  continuity of the trade?

Cite specific owners saying specific things. Do not generalize about ages,
health, or family circumstances. See `references/research-ethics.md`.

### 5. The discovery surface

Where companies in *this* sector are findable, ranked for this sector
specifically. Name actual sources, with URLs:

- Which associations, and do they publish a member directory?
- Which trade shows, and are exhibitor lists public?
- Which licenses or certifications are required, and is the roster public?
- Which registries carry useful ownership detail here?
- Which review or marketplace surfaces enumerate operators?

This section is what makes step 2 fast. Skipping it means discovering the same
sources three times.

### 6. Where not to look

The section that proves the map did its job. Explicitly out of scope:

- Segments outside the mandate, and why
- Size bands that cannot transact
- Sponsor-owned clusters
- Franchise networks, if the mandate is not a franchise roll-up
- Geographies excluded by the mandate

---

## How to build it

**Three to six hours of reading.** Sources, in rough order of value:

1. Association publications, member magazines, and annual reports — sector
   economics written by insiders for insiders
2. Trade press: consolidation coverage, "state of the industry" pieces
3. Sponsor portfolio pages and add-on press releases
4. The largest players' own sites — segment language, service mix, footprint
5. Public company filings where a listed comparable exists; the risk factors
   section is unusually honest about sector dynamics
6. Licensing and certification registries, for counts
7. One or two conversations with sector participants, if you can get them

**Then write it as a page** using `templates/market-map.md`, and circulate it.
If two people on your team would describe the sector differently after reading
it, the map is not finished.

---

## Quality tests

Before the map is used for anything:

| Test | Failure looks like |
|---|---|
| Does it exclude anything? | Every company in the sector sounds like a target |
| Is every claim sourced? | Confident sector "facts" with no URL |
| Are estimates labeled? | A precise-sounding count with no stated method |
| Does it name sponsors? | "The sector is consolidating" with no names |
| Are segments operating-based? | Segments that mirror an industry code list |
| Would it change a decision? | Reads as background rather than direction |

---

## Refresh cadence

A map is good for roughly six to twelve months. What goes stale first:

- The sponsor and platform list — add-on announcements land constantly
- The largest-player list, after any recap or merger
- Owner quotes, which date fast

Re-read the consolidation section before every new sourcing cycle. Everything
else can wait.

---

## What a map does not do

It does not name targets. The temptation to start listing companies while
mapping is strong and it corrupts both jobs: the map stops being a map, and the
list gets built before the criteria exist.

Note company names you stumble across in a scratch list, then run
`company-discovery` properly once the map is approved.
