# The Deal Origination Playbook for Private Equity

Most firms see a fraction of the relevant deals in their own market. The rest
do not disappear — somebody else finds them first.

This is the playbook for finding the companies nobody is calling yet, plus the
Claude Code package that runs it: **five agents and seven skills** that map a
market, find the companies inside it, score them against your mandate, read
the ownership and succession signals, and get you a verified route to the
person who can actually sell.

Origination only. It stops where outreach starts, deliberately.

Built for PE funds, family offices, search funds, independent sponsors,
holdcos, and corporate development teams that want proprietary deal flow
without a ten-person origination desk.

Runs on [Claude Code](https://www.anthropic.com/claude-code) and local files.
No database, no API keys, no signups.

---

## 👉 Read this first: [PLAYBOOK.md](./PLAYBOOK.md)

The method itself, in six steps. Useful whether or not you ever install
anything.

## 👉 Then set it up: [SETUP.md](./SETUP.md)

Fifteen minutes from zero to a running system. Every step in plain English.

---

## Came from the "PLAYBOOK" post? — this is it

**What it does, in the order you will use it:**

1. **Map the market beyond the obvious databases** — segments, fragmentation,
   who is already consolidating, and where the companies in this sector are
   actually findable
2. **Find companies that fit the mandate** — from association directories,
   trade show exhibitor lists, registries, licensing boards, and a dozen other
   places bought lists never cover
3. **Identify founder and family-owned businesses** — classified from evidence,
   never inferred from a website that says "family owned since 1987"
4. **Score targets against the investment thesis** — a rubric you approve
   first, applied identically to every row, then audited
5. **Find and verify the actual owners** — the person who can say yes, with a
   route that works. Never a guessed email address
6. **Research each business before outreach** — a one-page brief per target so
   the first conversation sounds like you know the company

### The five agents

| Agent | What it does |
|---|---|
| `market-mapper` | Maps the sector: segments, fragmentation, owner profile, who is already buying |
| `company-finder` | Finds the companies and classifies who owns them, with a source per row |
| `fit-scorer` | Scores every target against a mandate rubric you approve first |
| `signal-tracker` | Succession, ownership-change, and operating signals — quoted and dated |
| `contact-builder` | The person who can sell, and a verified route to them |

Install, then run `/agents` to see all five.

### The seven skills

| Skill | What it does |
|---|---|
| `market-map` | Maps a sector before you source in it |
| `company-discovery` | Finds private companies matching the mandate |
| `ownership-classification` | Establishes who owns each company, from evidence |
| `mandate-fit-scoring` | Scores against an approved rubric, then audits itself |
| `owner-identification` | Finds and verifies the decision maker honestly |
| `business-research` | The one-page pre-outreach brief per target |
| `coverage-tracking` | What of the map you have actually covered, and what you have not |

Install, then run `/skills` to see all seven.

> Both lists are the same system. The agents run the skills.

**The chain:**

```
market-mapper → company-finder → fit-scorer → signal-tracker → contact-builder
```

Each step does one job and hands its output to the next. Every step has an
approval gate before it writes anything.

---

## Where this stops

It hands you a scored target list, a signal record, and a verified contact
route per company. It does not write outreach, sequence anything, or send
anything.

---

## Repo contents

- [`PLAYBOOK.md`](./PLAYBOOK.md) — the method, in six steps
- [`SETUP.md`](./SETUP.md) — the full setup guide
- [`skills/`](./skills/) — the seven skills Claude Code reads
- [`agents/`](./agents/) — the five subagents
- [`references/`](./references/) — market mapping method, sourcing sources,
  ownership taxonomy, scoring rules, signal and evidence standards, research
  ethics
- [`templates/`](./templates/) — mandate profile, market map, target list,
  target brief, coverage log

---

## Built-in safety rails

**No fabrication.** `Not found` is the correct answer for anything unverified.
Every claim carries a source and a date. Ownership is established from
registries, filings, and the company's own statements — never inferred from
branding. Revenue and EBITDA estimates are labeled as estimates with the basis
stated.

**Every write is gated.** You see counts, breakdowns, and full sample rows
before anything is written to your files.

**Public professional sources only.** No pretexting, no personal-life data, no
bulk harvesting of sites that prohibit it. A succession signal is something an
owner said in public, not something inferred about their family.

**Nothing is sent.** There is no outreach in this package at all. Nothing here
can email anybody.

---

## Important

This is not investment, legal, or tax advice. If you intermediate transactions
for success fees rather than buy as a principal, broker-dealer registration
rules may apply to you — talk to counsel. Data protection law (GDPR, PECR,
CCPA and others) applies to owner research and differs by jurisdiction.

---

## License

[MIT](./LICENSE) — do whatever you want with it.
