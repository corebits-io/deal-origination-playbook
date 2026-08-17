---
name: market-map
description: "Map a sector before sourcing in it — segments by how businesses actually run, size distribution, fragmentation and which sponsors are consolidating, the typical owner, where companies in this sector are findable, and where not to look. Produces a sourced one-to-two-page map, not a target list. Triggers on: map the market, market map, map a sector, size the market, who is consolidating, is this sector fragmented, understand the sector, where do I find companies in, sector overview before sourcing."
---

# Market Map

Maps a sector so the next four steps are cheap and auditable. The output is a
decision document that tells the user where **not** to look.

**Read first:**
- `references/market-map-method.md` — the six sections and how each is built
- `references/sourcing-sources.md` — source types, for section 5
- `references/research-ethics.md` — terms of use, personal data, the lines

This skill produces **no company list**. Names you stumble across go in a scratch
list at the end, and `company-discovery` enumerates properly once the map is
approved.

---

## Step 0 — Load the mandate

Read `mandate-profile.md` from the user's workspace.

**If it does not exist:** copy `templates/mandate-profile.md` into the workspace
and walk the user through sections 2 to 7 at minimum before mapping. A map built
without a mandate maps somebody else's sector.

### 🚧 HARD GATE — intermediary check

Check section 9 of the mandate profile:

- **Principal buyer:** proceed
- **Fee-based intermediary:** STOP. Tell the user plainly that this can trigger
  broker-dealer registration questions in the US and that counsel should clear
  the model first. Proceed only after they confirm it is cleared. Per
  `references/research-ethics.md`, this is not legal advice — it is the first
  question counsel will ask
- **`TBD` or blank:** stop and ask

---

## Step 1 — Confirm scope

Restate back, from the mandate:

- The sector to map, and the geography
- The size box, so section 2 can be judged against it
- Deal type and ownership types in scope
- Known exclusions

Ask one question if the sector is broad: **map the whole sector, or one segment
of it?** Mapping "industrial services" is three maps. Mapping "commercial fire
and life safety in the Southeast" is one.

Wait for confirmation.

---

## Step 2 — Read, do not search-and-summarize

Work in roughly this order, and cite everything:

1. Association publications, member magazines, annual reports
2. Trade press: consolidation coverage, state-of-the-industry pieces
3. Sponsor portfolio pages and add-on press releases
4. The largest players' own sites — segment language, service mix, footprint
5. Public company filings for any listed comparable; the risk factors section is
   unusually honest about sector dynamics
6. Licensing and certification registries, for counts

**Rules while reading:**

- **Never write a sector fact from memory.** If it is not on a page you read in
  this session, it is `Not found`
- **Count things where counting is possible.** A licence roster count with a
  stated method beats "highly fragmented" every time
- **Label every estimate with its method** in the same sentence
- **Name sponsors and cite the portfolio page.** "The sector is consolidating"
  with no names is not a finding
- **Segment by how businesses earn**, not by industry classification

Check in after the reading pass, before writing, with what you found and what you
could not establish.

---

## Step 3 — Write the map

Use `templates/market-map.md`. All six sections:

1. **Segments** — three to six, operating-based, each with a one-line profile and
   an in-mandate flag
2. **Size distribution** — counts by band, method stated, and an explicit answer
   to whether the mandate size box intersects where the mass sits
3. **Fragmentation and consolidation** — largest players and their ownership;
   named sponsors with platforms here; the add-on profile they buy; an estimated
   sponsor-owned share
4. **The typical owner** — generation, background, and two or three sourced public
   quotes. Professional sources only, no generalizations about age or health
5. **Discovery surface** — actual sources with URLs, ranked for this sector, with
   a terms-of-use note per source
6. **Where not to look** — segments, size bands, sponsor clusters, franchise
   networks, geographies

Plus the summary at the top with a one-line verdict: `Source this sector`,
`Source a segment only`, or `Do not source`.

### 🚧 HARD GATE — before writing the file

Show the user:

- The summary and the verdict
- The segment table
- The sponsor list
- The three best sourcing angles
- The **"where not to look"** section in full
- Everything you could not establish, as open questions

Get approval. Then write.

---

## Step 4 — Feed the map forward

Two hand-offs, both explicit:

1. **Sponsor list → mandate profile section 8.** Offer to add the named sponsors
   to the exclusions section. `mandate-fit-scoring` screens against it
2. **Segments → mandate profile section 4.** If the map revealed better segment
   language than the mandate had, offer to update it

Ask before editing the mandate profile. It is the user's file.

---

## Step 5 — Report

```
Market map complete — Commercial fire & life safety, Southeast US

Verdict: Source a segment only

Segments identified:        4  (2 in mandate)
Size bands counted:         4  (method: state licence roster + association list)
Est. population in mandate: ~310 companies
Sponsors named:             6  (11 platforms, 40+ add-ons since 2022)
Est. sponsor-owned share:   ~25% of the in-mandate population
Owner quotes sourced:       3
Discovery sources found:    9  (2 prohibit automated collection — manual only)

Best three angles:
  1. State fire protection licence rosters (mandatory, dated, complete)
  2. NFSA/AFSA chapter member directories
  3. Trade show exhibitor lists, 2022-2026

Where not to look:
  - Residential-only operators (out of mandate)
  - Sub-$5M revenue band (~60% of population, below the size floor)
  - The 11 known sponsor platforms and their announced add-ons

Could not establish:
  - Margin norms in the inspection-recurring segment (no public source found)
  - Whether the two largest independents are family or partner-owned

Next: run company-discovery against angles 1-3.
```

**Report what you could not establish.** A map with no open questions has almost
certainly filled gaps with plausible sector generalities.

---

## Notes

- **A map is not a list.** If you find yourself writing company names into the
  map, stop. Note them in a scratch list and move on
- **The test of a good map is what it excludes.** If every company in the sector
  sounds like a target, the map has not done its job
- **Three to six hours of reading is normal.** A map produced in ten minutes is a
  summary of what the model already believed about the sector, which is exactly
  the failure mode this step exists to prevent
- **Re-read the consolidation section before every new sourcing cycle.** It goes
  stale fastest
- **One map per sector per geography.** Do not merge two sectors into one map to
  save time; the segment boundaries stop meaning anything
