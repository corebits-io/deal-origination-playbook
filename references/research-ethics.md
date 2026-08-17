# Research Ethics and Compliance

The lines this playbook does not cross, and the rules that apply to origination
research whether or not anybody is watching.

**None of this is legal advice.** It is a summary of the questions to ask, and
the ones your counsel will ask first. Jurisdictions differ, and the differences
matter.

---

## 🚧 The intermediary question

Before any research begins, establish which you are:

- **Principal buyer** — buying for your own fund, search, holdco, or balance
  sheet. Proceed
- **Fee-based intermediary** — paid to introduce deals to other buyers. **Stop.**
  In the US, effecting securities transactions for compensation can trigger
  broker-dealer registration requirements, and the analysis turns on facts about
  your model, not on what you call yourself. Get it cleared with counsel before
  you research or contact anybody
- **Unclear** — treat as the second case until it is resolved

This is the first question counsel will ask, and it is recorded in section 9 of
the mandate profile for exactly that reason.

---

## Sources: what is fine and what is not

### Fine

- Reading public websites, directories, registries, and filings
- Reading published interviews, press coverage, and award profiles
- Reading professional profiles and company pages
- Reading public licensing and certification rosters
- Manual research at human pace, page by page
- Recording what you read, with a citation

### Not fine

- **Bulk or automated extraction from sites whose terms prohibit it.** Many
  directories and platforms do. Technical possibility is not permission, and
  platform terms are enforced
- **Pretexting.** Calling reception posing as a customer, supplier, job
  applicant, student, or journalist to extract information. This is the most
  common line crossed in origination and it is not recoverable when discovered
- **Circumventing access controls.** Paywalls, login walls, rate limits, robots
  directives
- **Buying scraped personal data.** "Verified owner emails" from a vendor who
  cannot tell you the source or the lawful basis
- **Personal-life research.** Health, family circumstances, finances, home
  address, personal social accounts, personal phone numbers
- **Contacting employees for information under the cover of buying interest.** A
  target's staff are not a research source

### The test

> Would you be comfortable if the owner read a full log of how you researched
> them, on the first call?

If not, stop. In small sectors, they often effectively do.

---

## Personal data

Owner names, titles, work emails, and professional profiles are personal data in
most jurisdictions, and processing them carries obligations.

**Practical rules:**

1. **Keep it in the workspace, out of any repository.** The `.gitignore` in this
   repo blocks the workspace patterns and CSVs by default. Keep it that way
2. **Collect the minimum.** Business contact routes and role information. Nothing
   about the person outside their professional role
3. **Record provenance.** For every contact, where it came from and when. If you
   cannot answer "where did you get this," you should not hold it
4. **Honour objections immediately and permanently.** If someone asks not to be
   contacted or asks what you hold, act on it and keep the suppression record
   forever
5. **Delete what you are not using.** `Not a Fit` rows do not need enriched
   personal data. Do not enrich them in the first place

**By jurisdiction, at a very high level:**

| Jurisdiction | Notes |
|---|---|
| **EU / EEA** | GDPR applies to business contact data. You need a lawful basis (usually legitimate interests, documented), transparency, and you must handle access and objection requests |
| **UK** | UK GDPR plus PECR. Similar to the EU. Corporate subscriber rules differ from individual subscribers |
| **US** | Federal rules govern commercial email content and opt-out (CAN-SPAM). State privacy laws (CCPA/CPRA and successors) create access and deletion rights that can cover business contacts |
| **Canada** | PIPEDA for data, CASL for electronic messages. CASL is consent-based and strict, with real penalties |
| **Elsewhere** | Assume something applies and check |

Nothing in this repo sends messages, so the messaging rules above bite at the
next stage rather than this one. The data rules bite immediately, from the first
row you record.

---

## Public companies and MNPI

This playbook is for private company origination. If a target turns out to be
public, or a subsidiary of a public company:

- Mark it `Not a Fit` per `references/ownership-taxonomy.md`
- Do not accumulate non-public information about it
- Disclosure regimes, insider dealing rules, and takeover codes apply, and none
  of them are covered here

If a private target is a supplier or customer of a public company, be careful
about what you learn and from whom.

---

## Confidentiality in both directions

- **Anything an owner tells you in a first conversation is theirs, not yours.**
  Do not use it to source competitors in the same segment
- **Do not reveal that a company is talking to you**, including implicitly to
  other owners in the sector. Sectors are small
- **Your own portfolio conflicts are your problem to manage.** Never research or
  approach a direct competitor of a portfolio company under the cover of buying
  interest. It is a real legal risk, not just a reputational one
- **NDA-covered material stays out of shared files and out of any repository**

---

## Honesty in what you claim

The moment you contact anybody, everything you have said about yourself becomes
checkable. It applies to research too, since researchers are frequently asked
who they are and why they are asking.

- Never imply committed capital you do not have
- Never imply a mandate, sector track record, or transaction history you cannot
  evidence
- Never imply an offer, a valuation, or a process that does not exist
- Never manufacture familiarity or a shared connection

An owner who discovers an overstatement mid-process is a dead deal, and in a
small sector, a burned market. The mandate profile records what you are cleared
to say for exactly this reason.

---

## Anti-fabrication is an ethics rule, not just a quality rule

Every fabricated field in a target list eventually becomes something said out
loud to a real person about their own company. A guessed revenue figure becomes a
wrong number in a first meeting. A guessed owner name becomes a letter addressed
to somebody who left in 2019. A pattern-guessed email becomes a bounce and a
damaged sending domain.

`Not found` is always the better answer. See `references/scoring-rules.md`.

---

## If in doubt

Ask three questions:

1. Would the owner be comfortable seeing how I got this?
2. Can I evidence every claim I am about to make or record?
3. Would my counsel be comfortable with the method, not just the outcome?

Three yeses, proceed. Anything else, stop and ask a human.
