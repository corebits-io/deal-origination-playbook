# The Deal Origination Playbook — Setup Guide

> A free giveaway. Five agents and seven skills that run PE deal origination
> from your terminal: market mapping, company discovery, ownership
> classification, mandate scoring, signal reading, and verified owner contacts.
>
> Follow this guide end to end and you will have it running on your own machine
> in about fifteen minutes. No database, no API keys, no signups.

**Read [PLAYBOOK.md](./PLAYBOOK.md) first if you have not.** It is the method
this package runs. The setup makes more sense once you have read it.

---

## What this actually is

**The five agents** are the chain. You talk to them like people.

| Agent | What it does |
|---|---|
| `market-mapper` | Maps a sector: segments, size distribution, who is consolidating, the typical owner, where companies here are findable, and where not to look. |
| `company-finder` | Enumerates the population from public sources, then establishes who owns each company from filings and registers — including the sponsor screen that catches add-ons. |
| `fit-scorer` | Builds a rubric from your mandate, gets it approved, scores every row identically, then audits itself. |
| `signal-tracker` | Reads succession, ownership-change, operating, and stress signals — quoted, sourced, dated — and writes a one-page brief per target. |
| `contact-builder` | Finds the person who can actually sell, and a route that reaches them. Never a guessed email. |

**The seven skills** are what the agents actually run. You can call them
directly too.

`market-map` · `company-discovery` · `ownership-classification` ·
`mandate-fit-scoring` · `owner-identification` · `business-research` ·
`coverage-tracking`

Everything runs through conversation. Your data stays in local files on your
machine.

**Where it stops:** a scored target list, a signal record, a verified contact
route, and a brief per target. It writes no outreach and sends nothing. That is
deliberate — see the FAQ.

---

## What you need

| Thing | Cost | Required? |
|---|---|---|
| [Claude Code](https://www.anthropic.com/claude-code) | Claude subscription or API usage | **Yes** |
| A folder on your computer | Free | **Yes** |
| Your LinkedIn connections export | Free | Strongly recommended |
| Everything else | — | No |

That is the whole list. There is deliberately no database, no MCP server, and
no API key to configure. Optional upgrades are at the bottom, for when you
outgrow files.

---

# Part 1 — Install Claude Code

Claude Code is Anthropic's official terminal app for Claude. It runs everything
here.

Follow the official instructions at
**[anthropic.com/claude-code](https://www.anthropic.com/claude-code)**. macOS,
Windows, and Linux are all supported.

Then check it works:

```bash
claude
```

You should get a welcome screen and a prompt. Type `/login` and authenticate if
you have not already. Exit with Ctrl+C twice.

---

# Part 2 — Install the package

Two steps: clone the repo, then copy the pieces where Claude Code looks for
them.

### macOS / Linux

```bash
git clone https://github.com/corebits-io/deal-origination-playbook.git
mkdir -p ~/.claude/skills ~/.claude/agents
cp -r deal-origination-playbook/skills/* ~/.claude/skills/
cp -r deal-origination-playbook/agents/* ~/.claude/agents/
```

### Windows (PowerShell)

```powershell
git clone https://github.com/corebits-io/deal-origination-playbook.git
New-Item -ItemType Directory -Force "$HOME\.claude\skills", "$HOME\.claude\agents"
Copy-Item -Recurse -Force "deal-origination-playbook\skills\*" "$HOME\.claude\skills\"
Copy-Item -Recurse -Force "deal-origination-playbook\agents\*" "$HOME\.claude\agents\"
```

### Keep the repo

Do not delete the cloned folder. The skills read the `references/` files from
it, and you will copy the `templates/` in a moment.

### Verify

Start Claude Code and run:

```
/skills
```

You should see all seven: `market-map`, `company-discovery`,
`ownership-classification`, `mandate-fit-scoring`, `owner-identification`,
`business-research`, `coverage-tracking`.

Then:

```
/agents
```

You should see all five.

If either list is short, see Troubleshooting below.

---

# Part 3 — Set up your origination workspace

This is where your actual data lives. Keep it separate from the cloned repo.

```bash
mkdir -p ~/my-origination/briefs
cd ~/my-origination
cp ~/deal-origination-playbook/templates/mandate-profile.md .
cp ~/deal-origination-playbook/templates/targets.csv .
cp ~/deal-origination-playbook/templates/coverage-log.md .
```

Windows:

```powershell
New-Item -ItemType Directory -Force "$HOME\my-origination\briefs"
Set-Location "$HOME\my-origination"
Copy-Item "$HOME\deal-origination-playbook\templates\mandate-profile.md" .
Copy-Item "$HOME\deal-origination-playbook\templates\targets.csv" .
Copy-Item "$HOME\deal-origination-playbook\templates\coverage-log.md" .
```

> **Never put this folder in a public repository.** It will contain company
> names, owner contact details, and later, notes from private conversations —
> possibly under NDA. Owner names and work emails are personal data and are
> regulated in most jurisdictions.

Delete the example row from `targets.csv` before you start. It is there to show
you what a correctly filled row looks like.

---

# Part 4 — Fill out your mandate profile

**This is the most important step in the whole guide.** Do not skip it and do
not rush it.

`mandate-profile.md` is the file every skill reads. It is where the system
learns what you buy, what size, where, which ownership types are actionable,
what you will never touch, and who counts as a competitor.

Open it and fill it out honestly. Ten minutes here saves hours later.

**Three rules while filling it out:**

1. If something does not apply, write `N/A`
2. If you do not know yet, write `TBD` — the agents will ask rather than invent
3. **Answer section 9 properly.** If you are a fee-based intermediary rather
   than a principal buyer, the agents will stop and tell you to talk to counsel
   about broker-dealer registration before researching anybody. That gate is
   there on purpose

If you would rather do this conversationally, start Claude Code in the folder
and say:

```
help me fill out my mandate profile
```

Sections 4 and 8 will improve after your first market map. That is expected —
come back and update them.

---

# Part 5 — Your first run

Start Claude Code from your origination folder:

```bash
cd ~/my-origination
claude
```

### 1. Map the market first

```
map the market for [your sector] in [your geography]
```

You get segments, size distribution, the sponsors already consolidating the
space, the typical owner, where these companies are findable — and where not to
look. Three to six hours of reading, condensed into a page.

**Read the verdict at the top.** Sometimes it is "do not source this sector,"
and that answer just saved you three weeks.

Then let it add the sponsor list to your mandate profile:

```
add the sponsors you found to my exclusions
```

### 2. Find the companies

```
find companies matching my mandate using the map
```

The finder confirms your brief, shows you a source plan, then works through
several angles. It stops and shows you samples along the way. Aim for 100 to 300
genuinely qualified companies, not thousands.

### 3. Establish who owns them

```
classify ownership for the list
```

This runs the sponsor screen on every row. Expect it to catch companies still
marketing themselves as family owned that were acquired years ago — that is the
point of the step, and it is the most common miss in origination.

### 4. Score them

```
score the list against my mandate
```

You will be shown the rubric before anything is scored. **Read it.** The
exclusion list and the sponsor screen are the two things that most commonly need
correcting, and correcting them here saves a rebuild.

Then read the audit at the end. It checks Strong Fit signals at their source URLs
and hunts for false negatives among the exclusions.

### 5. Research the keep pile

```
research my Strong Fit targets and write briefs
```

Ten to twenty at a time. You get a one-page brief per company, ending with an
explicit list of what is not known.

Then come back to scoring:

```
re-score the rows that now have signals
```

### 6. Find the owners

```
find the owners and contact routes for these companies
```

Export your LinkedIn connections first if you want warm paths checked:
**LinkedIn → Settings & Privacy → Data Privacy → Get a copy of your data →
Connections**. It arrives by email in a few minutes. Save `Connections.csv` into
your origination folder.

A warm introduction to an owner outperforms any cold approach you will ever
make. Always check before going cold.

### 7. Check your coverage

```
how much of this market have we actually covered?
```

The honest answer, by segment, by region, and by source — plus the gaps, the
things previous runs capped or truncated, and what needs re-scoring.

Run this at the end of every session. It takes two minutes and it is what makes
the next session start in the right place.

---

# Working with the agents directly

You can call an agent by name for a bigger job:

```
use the market-mapper agent to map commercial fire and life safety
in the Southeast US
```

```
use the company-finder agent to work the two state licence rosters
we have not touched yet
```

```
use the signal-tracker agent to brief the five companies with
ownership changes filed this year
```

The agents run the skills. Either route works. Talk normally and the right one
gets picked up.

---

# The safety rails

Built in on purpose, and not configurable.

**Every write has an approval gate.** You see counts, breakdowns, and full
sample rows before anything is written to your files.

**No fabrication.** `Not found` is the correct answer for anything unverified.
Every claim carries a source URL and a date. Revenue and EBITDA estimates are
labeled as estimates with the basis stated — a confident wrong number in a first
conversation is unrecoverable.

**Ownership is evidence, not vibes.** Classified from statutory registers,
filings, press releases, and the company's own statements. Never from branding,
design quality, or "family owned since 1987" marketing copy.

**No guessed email addresses.** Ever. Published or verified only. Pattern
guessing destroys sending domains.

**Public professional sources only.** No pretexting, no personal-life data, no
bulk harvesting of sites whose terms prohibit it. A succession signal is
something an owner said in public, not something inferred about their family.

**Nothing is sent.** There is no outreach capability in this package at all.

**The intermediary gate.** If your mandate profile says you are a fee-based
intermediary rather than a principal buyer, the agents stop and tell you to
clear it with counsel first.

None of this is legal advice.

---

# Troubleshooting

### `/skills` does not show the seven skills

Check they landed in the right place:

```bash
ls ~/.claude/skills/
```

You should see seven folders, each containing a `SKILL.md`. If you see a single
`deal-origination-playbook` folder instead, the copy command copied the parent
rather than the contents. Re-run it with the `/*` on the end.

Restart Claude Code after fixing.

### `/agents` does not show the five agents

```bash
ls ~/.claude/agents/
```

You should see five `.md` files. Same fix as above.

### "It cannot find my references files"

The skills read `references/` from the cloned repo. If you moved or deleted it,
tell Claude where it is, or re-clone.

### It keeps saying "Not found" instead of giving me data

That is the system working. It will not invent an email address, a revenue
figure, or an owner's intention to sell. A blank field is recoverable. A
confident wrong one gets you a bounce, a bad first meeting, or a credibility
problem in a market where owners talk to each other.

### It refuses to guess an email address

By design, and it will not be talked round. See the sending-domain note in
`skills/owner-identification/SKILL.md`.

### It classified a company as "Not found" ownership and I think it is family owned

Then it could not find tier 1 to 5 evidence, and neither did it invent any. Look
at what it says it checked — usually the state registry or Companies House will
settle it in two minutes by hand. Tell it what you found and it will record your
source.

### It stopped and asked about broker-dealer registration

Section 9 of your mandate profile says fee-based intermediary, or is blank. If
you are buying as a principal, say so in the profile. If you are not, that gate
is doing its job.

### It is slow

Real research is slow. A properly mapped sector plus a 200-company classified
list takes a few sessions, not one prompt. Speed here comes directly out of
accuracy, and an inaccurate target list wastes the scarcest thing you have:
credible first impressions with owners.

### Windows path problems

Use forward slashes or quoted paths, and tell Claude your paths explicitly. If
something looks wrong, say `my origination folder is at
C:\Users\me\my-origination` and it will adapt.

---

# FAQ

### Do I need to pay for anything beyond Claude Code?

No. The whole thing runs on Claude Code and local files. Optional paid tools are
listed below, and they buy you speed, not accuracy.

### Why is there no outreach in this?

Because origination and outreach are different disciplines with different
failure modes, and mixing them tempts you to write to a list you have not
properly qualified. Get the list right first. Outreach is a separate
discipline, and is deliberately out of scope here.

### Is my deal data safe?

It stays in local files on your machine. Nothing is uploaded anywhere except
your conversation with Claude. Keep your origination folder out of any public
repository.

### Can I use this outside the US?

The method applies anywhere, and the registry sources are genuinely better in
some jurisdictions — UK Companies House and the EU beneficial ownership
registers give you ownership data US filings mostly do not. The compliance notes
in `references/research-ethics.md` cover US, UK, EU, and Canadian rules at a high
level. Every jurisdiction differs. Talk to local counsel.

### How many companies should I work?

100 to 300 well-qualified companies for a focused mandate. A list of 5,000
unqualified rows is worse than 150 good ones — it buries the dozen real
succession conversations in noise and burns your name in a market where owners
know each other.

### What if I already have a list?

Drop your CSV in the workspace and say `score this list against my mandate`. It
will map your columns, tell you what it mapped, and run the rubric. Anything it
cannot map becomes `Not found` rather than an inference.

### I am a search funder / independent sponsor without committed capital. Does this still work?

Yes — set your buyer type and capital position honestly in section 1. Nothing
here sends messages, but the briefs are what you take into first conversations,
and they will describe you accurately rather than implying a fund you do not
have.

### Can I change the rules?

Yes. Everything is a markdown file. Edit `references/scoring-rules.md` to fit
your market, or `references/sourcing-sources.md` to add sources you know. The
ethics rules in `references/research-ethics.md` are the ones to think hard about
before loosening.

### Why does it keep telling me to run the market map first?

Because a list built before the market is mapped is a list for a market you have
not defined. You can skip it. You will usually rebuild the list.

---

# When you outgrow files

You will not need any of this on day one. Add it when volume actually demands
it.

| Tool | What it adds | When |
|---|---|---|
| [Serper](https://serper.dev) / [Exa](https://exa.ai) | Programmatic search at volume | Past ~500 companies |
| Registry APIs (Companies House, state bulk data) | Structured ownership at scale | Past a few hundred classifications |
| [Hunter](https://hunter.io) / [Prospeo](https://prospeo.io) | Email discovery and verification | Before any bulk send |
| ZeroBounce / NeverBounce | Deliverability verification | Before any bulk send |
| [Neon](https://neon.tech) Postgres | Real database | Past a few thousand rows |
| A real CRM | Team collaboration | When more than one person works the pipeline |

If you move to a database or CRM, keep the CSVs as your source of truth and
export from them. Two-way sync between files and a CRM goes wrong quietly.

---

# What's next

Map one sector properly. Build a small, well-classified, well-scored list.
Research the owners before you write a word to them. Then go and have twenty
real conversations.

The single highest-leverage habit in the whole playbook is running
`coverage-tracking` at the end of every session. It is the difference between a
systematic process and a pile of sessions that felt productive.

Good hunting.

---

*This guide covers version 1.0. Source:
[github.com/corebits-io/deal-origination-playbook](https://github.com/corebits-io/deal-origination-playbook)*
