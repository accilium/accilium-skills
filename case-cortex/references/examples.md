# Case Cortex — worked examples

Pull this file in when the user asks for examples or you're unsure how
a specific entry should look. All examples use fictional cases.

---

## Example 1 — Minimal-mode start

**Context:** user says: *"I want to start tracking my work on the
acquisition we're considering, but I don't want to commit to a heavy
structure yet."*

The skill offers minimal mode. After confirming the case slug
(`{target-acquisition}`) and the runtime supports persistent files,
the skill creates:

```
{target-acquisition}/
  CLAUDE.md
  cortex.yaml
  README.md
  notes.md
```

`notes.md` opens with:

```markdown
# {Target Acquisition} — Notes

> This is a minimal-mode Cortex. One growing notes file. The skill
> will offer to migrate to the full four-layer structure when this
> file gets long enough or when you start ingesting multiple sources.

## What this is

{Why you started this Cortex; what you're trying to figure out.}

## Open questions

- {first question}
- {second question}

## Notes

### {YYYY-MM-DD}

{First entry.}
```

Two weeks later, the user has 600 lines of notes and wants to ingest
a teaser document from the seller. The skill detects both signals
(line count, first source to ingest) and offers migration to full
mode. The user accepts; the skill creates the four-layer scaffolding,
splits the notes into the appropriate layers (open questions →
`02-working-memory/open-questions.md`, dated entries →
`02-working-memory/log/`), and proceeds with Workflow 3 (Ingest) on
the teaser document.

---

## Example 2 — Wizard-mode seeding for a strategic-review case

**Context:** user is starting a new case for a fictional client called
"{Client Co}" — a strategic review of their portfolio. They chose
`consulting` flavor.

### Dialog excerpt

> **Skill:** Let's start with Layer 1, file by file. First,
> `identity.md`. A few questions:
>
> 1. Case name — I'll use `{client-co-strategic-review}` as the slug
>    unless you'd rather something else.
> 2. Case type — strategic review, transformation, due diligence,
>    something else?
> 3. One-paragraph purpose?
> 4. Start date? (I'll default to today if unspecified)
> 5. Current status — pre-kickoff, active, on hold, wrapping up?
> 6. How will you know this case succeeded?
>
> **User:** Slug is fine. Strategic review. Purpose: help {Client Co}
> decide whether to exit a particular line of business. Start today.
> Pre-kickoff. Success = board-ready recommendation by end of Q3
> with clear scenario modeling.

### Resulting `identity.md`

```markdown
# Identity

## Case

- **Name:** {Client Co} Strategic Review
- **Slug:** client-co-strategic-review
- **Type:** Strategic review
- **Status:** Pre-kickoff
- **Started:** {YYYY-MM-DD}

## Purpose

Help {Client Co} decide whether to exit a particular line of
business. Deliver a board-ready recommendation with scenario modeling
by end of Q3.

## Success criteria

- Board receives a decision-ready recommendation by {date}
- Recommendation is backed by at least three quantified scenarios
- Scenarios cover market, regulatory, and operational dimensions

## Change Log

- {YYYY-MM-DD} — Initial seeding via wizard.
```

The wizard then walks through each named stakeholder the user
mentions, creating one entity page per person and per organisation
under `01-canonical/entities/`. It does not lump them into a single
`entities.md` file.

---

## Example 3 — One-shot seeding from a pasted intake memo

**Context:** user is a forensic investigator. They picked
`investigation` flavor and pasted a 2-page intake memo about a
fictional case code-named "{Codename}".

### User input (abridged)

> *"Investigation initiated by GC on {YYYY-MM-DD}. Subject: possible
> misrepresentation in Q4 revenue recognition at subsidiary {Subsidiary}.
> Key persons of interest: CFO {Person A} (subsidiary), controller
> {Person B}. External auditor was {Audit Firm}. Initial scope:
> revenue transactions over a threshold in Q4. Data sources available:
> GL dumps, email archives (subject to legal hold as of {date}),
> customer contracts. GC has imposed a preliminary confidentiality
> ring. Budget: {amount}. Deadline: preliminary report by {date}."*

### Resulting fan-out

The skill routes this as Ingest (Workflow 3) on the intake memo.
Output:

- `entities/{subsidiary-slug}.md` — the subsidiary under review
  (entity_type: legal-entity)
- `entities/{person-a-slug}.md` — CFO of subsidiary
  (entity_type: person)
- `entities/{person-b-slug}.md` — controller (entity_type: person)
- `entities/{audit-firm-slug}.md` — external auditor
  (entity_type: organization)
- `entities/general-counsel.md` — internal stakeholder
  (entity_type: person, identity TODO)
- `concepts/legal-hold.md` — the legal-hold mechanism applied to
  email archives
- `concepts/confidentiality-ring.md` — the access-control regime
  imposed by GC
- `concepts/revenue-recognition.md` — the accounting concept under
  review
- `concepts/transaction-threshold.md` — the scope mechanism (over a
  certain amount in Q4)
- `sources/{date}_intake-memo.md` — the source summary

`scope.md` and `context.md` get index links pointing into the new
entity and concept pages. `synthesis.md` opens with "no synthesis
yet — case just initialised; first ingest pending substantive
sources." `index.md` lists everything under topical clusters.

Where the brief was clear, facts are written as facts. Where it
wasn't (specific signing partner at the audit firm, names of the
paralegal), `TODO:` markers flag the gap on the relevant entity page.

---

## Example 4 — Ingest fan-out on a workbook (the fan-out pattern)

**Context:** user is building a Cortex for a fictional consulting
firm's economic model. They point the skill at a multi-sheet
workbook (`{firm}-eco-model-FY{year}.xlsx`) and ask: *"Read this
into the cortex."*

This is Workflow 3 — Ingest. The expected output is a fan-out into
many entity and concept pages, not a single summary.

### Phase 1 — Pointer staged

The skill adds an entry to `04-pointers/systems.yaml`:

```yaml
- id: eco-model-workbook-fy{year}
  system: sharepoint
  kind: document
  url: https://{org}.sharepoint.com/.../{firm}-eco-model-FY{year}.xlsx
  description: Primary financial model workbook covering all operating entities.
  confidentiality: confidential
  last_verified: {YYYY-MM-DD}
```

### Phase 2 — Enumeration

The skill reads the workbook and produces an enumeration list,
splitting entities and concepts:

> I read the workbook and identified 3 entity candidates and 20
> concept candidates. Before I write the pages, please confirm or
> trim:
>
> **Entities** (→ `01-canonical/entities/`)
>
> 1. `{firm}-uk` — UK operating entity (legal entity)
> 2. `{firm}-nl` — Dutch operating entity (legal entity)
> 3. `{firm}-es` — Spanish operating entity (legal entity)
>
> **Concepts** (→ `01-canonical/concepts/`)
>
> 1. `revenue` — top-line driver
> 2. `contribution-margin-1` — first profitability checkpoint
> 3. `contribution-margin-2` — second profitability checkpoint
> 4. `ebit` — earnings before interest and tax
> 5. `ebt` — earnings before tax
> 6. `bill-rate` — hourly/daily sell rate per role
> 7. `utilisation` — target vs. actual utilisation per role
> 8. `pyramid` — role mix convention
> 9. `senior-role` — senior role definition
> 10. `manager-role` — manager role definition
> 11. `staff-role` — staff role definition
> 12. `target-bonus` — target bonus per role
> 13. `payroll-overhead-factor` — payroll overhead factor per entity
> 14. `bonus-split` — individual vs. company component of the bonus
> 15. `profit-share-pool` — partner profit-share mechanism
> 16. `equity-buy-in` — partner equity buy-in mechanism
> 17. `valuation-approach` — how ownership stakes are valued
> 18. `corporate-tax-rate` — per-entity tax assumptions
> 19. `dividend-policy` — flagged as open in source
> 20. `time-basis` — working-days / hours-per-year convention
>
> Out of scope, missing, or merge candidates?

User confirms. Skill proceeds.

### Phase 3 — Pages written

3 entity pages and 20 concept pages, each ~5–10 sentences of
description plus related links and any open questions. Example
shape (`contribution-margin-1.md`):

```markdown
---
kind: concept
first_seen: {YYYY-MM-DD}
sources:
  - 04-pointers/systems.yaml#eco-model-workbook-fy{year}
aliases:
  - CM1
  - First Contribution Margin
confidentiality: confidential
---

# Contribution Margin 1

## Definition

Contribution Margin 1 (CM1) is operating margin after deducting
variable cost of revenue from revenue. In the eco-model workbook,
CM1 = Revenue − Delivery People Cost − External Delivery Cost.

## Description

CM1 is the first profitability checkpoint in the firm's P&L cascade.
It isolates the margin earned on consultant time before any
infrastructure, overhead, or management cost is allocated. Because
people cost dominates the deduction, utilisation and bill rate are
the two levers that move CM1 most. CM1 is calculated per legal
entity and consolidated for the operating group; it feeds CM2 and
ultimately EBIT.

## Related concepts and entities

- [Revenue](./revenue.md) — the input
- [Bill Rate](./bill-rate.md) — primary lever
- [Utilisation](./utilisation.md) — primary lever
- [CM2](./contribution-margin-2.md) — next stage in the cascade
- [{firm}-uk](../entities/{firm}-uk.md) — calculated for this entity

## Open questions

- Confirm whether the workbook lines "External Delivery Cost" and
  "Partner Delivery" refer to the same cost block.

## Synthesis

> Synthesis: CM1 vs. CM2 split is unusually informative because it
> isolates consultant economics from the overhead-management
> question. Most operational levers (pyramid, bill rate,
> utilisation) move CM1 only.

## Change Log

- {YYYY-MM-DD} — Initial page from ingest of eco-model-workbook-fy{year}.
```

### Phase 4 — Skeleton files updated as indexes

`context.md` gains a one-paragraph cascade map with links into the
relevant concept pages. The rich content stays in `concepts/`.

### Phase 4.5 — Spine updated

`index.md` gains:

```markdown
## Entities

### Legal entities

- [{firm}-uk](./entities/{firm}-uk.md) — UK operating entity
- [{firm}-nl](./entities/{firm}-nl.md) — Dutch operating entity
- [{firm}-es](./entities/{firm}-es.md) — Spanish operating entity

## Concepts

### P&L cascade

- [Revenue](./concepts/revenue.md) — top-line driver
- [Contribution Margin 1](./concepts/contribution-margin-1.md) — first profitability checkpoint
- [Contribution Margin 2](./concepts/contribution-margin-2.md) — second profitability checkpoint
- [EBIT](./concepts/ebit.md) — earnings before interest and tax
- [EBT](./concepts/ebt.md) — earnings before tax

### Compensation mechanics

- [Bill Rate](./concepts/bill-rate.md)
- [Utilisation](./concepts/utilisation.md)
- [Pyramid](./concepts/pyramid.md)
- [Target Bonus](./concepts/target-bonus.md)
- [Bonus Split](./concepts/bonus-split.md)
- [Profit Share Pool](./concepts/profit-share-pool.md)

### Ownership model

- [Equity Buy-In](./concepts/equity-buy-in.md)
- [Valuation Approach](./concepts/valuation-approach.md)
- [Dividend Policy](./concepts/dividend-policy.md) — flagged as open

### Conventions

- [Corporate Tax Rate](./concepts/corporate-tax-rate.md)
- [Time Basis](./concepts/time-basis.md)
- [Payroll Overhead Factor](./concepts/payroll-overhead-factor.md)
```

`synthesis.md` is updated with current direction (workbook structure
absorbed; cascade is the dominant frame; bill rate × utilisation is
the lever the case will likely focus on) and 8 new open questions.

### Phase 5 — Open questions logged

`open-questions.md` mirrors the source-flagged opens (dividend
policy, valuation method).

### Phase 6 — Ingest log entry

`02-working-memory/log/{YYYY-MM-DD}-ingested-eco-model-workbook.md`
records the full fan-out: 3 entity pages, 20 concept pages, 4
skeleton files updated, spine updates, 8 new open questions, honest
state.

### Phase 7 — Optional structural briefing

Because the workbook is structurally complex (3 scenario views × 5
fiscal years), the skill also writes
`03-derived/briefing/{YYYY-MM-DD}-eco-model-workbook-structure.md`
— a *map of the workbook*, not a summary of its content.

### Phase 8 — Reported back

> Ingested the eco-model workbook. Created 3 entity pages and 20
> concept pages, wrote source summary at
> `01-canonical/sources/{YYYY-MM-DD}_eco-model-workbook-fy{year}.md`,
> updated all four skeleton files, updated index and synthesis,
> added 8 open questions, logged the ingest. Top entities:
> {firm}-uk, {firm}-nl. Top concepts: CM1, Bill Rate, Pyramid.
> Want me to walk through any?

### What this example demonstrates

- One source → many pages (23, not 1).
- Skeleton files become an index, not a duplicate of the richness.
- Entity pages and concept pages are split: legal entities get
  `entities/`; mechanisms get `concepts/`.
- Concept pages have rich Descriptions, marked Synthesis, and
  cross-links.
- Provenance is end-to-end: pointer → frontmatter `sources` →
  ingest log.
- The structural briefing is a map of the workbook, not a substitute
  for fan-out.

---

## Example 5 — A typical week of maintenance entries

### Monday, {YYYY-MM-DD}

User: *"Add to the cortex that we had a kickoff with the {Client
Co} CFO today. Agreed on scope. Next meeting in two weeks."*

Skill creates `02-working-memory/log/{YYYY-MM-DD}-client-co-kickoff.md`:

```markdown
# Client Co kickoff meeting

**Date:** {YYYY-MM-DD}
**Participants:** {user}, {Client Co} CFO {name TBD}

## What happened

Kickoff call with {Client Co} CFO. Confirmed scope and timeline.
Agreed on 2-week cadence for working sessions.

## Decisions taken

- Scope confirmed as outlined in `identity.md`.
- Next working session: {YYYY-MM-DD}.

## Open questions raised

- Which {Client Co} business units are in-scope for scenario modeling?

## Next steps

- Send kickoff summary to CFO — {user} — {due date}
- Schedule working session — {user} — {due date}
```

The skill also appends the open question to `open-questions.md` and
adds a Change Log entry on `identity.md`.

### Wednesday, {YYYY-MM-DD+2}

User: *"Open question resolved — scope is the three core BUs only."*

Skill edits `open-questions.md`:

```markdown
## Resolved

- **Which {Client Co} business units are in-scope?** — [resolved
  {YYYY-MM-DD+2}: only the three core BUs are in-scope; the rest
  are excluded.]
```

Skill also updates `scope.md` (Layer 1) to reflect the resolved
scope and adds a Change Log entry. Because `scope.md` changed
materially, the skill scans Layer 3. Empty so far — no flags
needed.

### Friday, {YYYY-MM-DD+4}

User: *"Decision made: we're going with Approach A."*

Skill appends to `decisions.md`:

```markdown
## {YYYY-MM-DD+4} — Use Approach A

**Context:** Approach A vs. Approach B was open since {YYYY-MM-DD-7}.
**Decision:** Approach A.
**Rationale:** {cost / quality / timeline reasoning, with concrete
numbers}.
**Superseded by:** —
**Related log:** [→ log/{YYYY-MM-DD+4}-approach-decision.md]
```

---

## Example 6 — Derived artifact generation with provenance

**Context:** Cortex for {Client Co} is 3 weeks in. User asks:
*"Generate a briefing for the scenario modeling workshop next week."*

The skill:

1. Reads `identity.md`, `scope.md`, `context.md`, and the relevant
   subset of `entities/` and `concepts/` from Layer 1.
2. Reads `decisions.md` and recent log entries from Layer 2.
3. Computes content hashes of every input it consulted.
4. Writes `03-derived/briefings/{YYYY-MM-DD}-scenario-modeling-briefing.md`:

```markdown
---
generated_at: {YYYY-MM-DDTHH:MM:SSZ}
generator: case-cortex skill
inputs:
  - path: 01-canonical/identity.md
    hash: sha256:a3f2b1c8e91d
    hash_mode: material-v1
  - path: 01-canonical/scope.md
    hash: sha256:7c2e44f0a92b
    hash_mode: material-v1
  - path: 01-canonical/context.md
    hash: sha256:f99c00abe521
    hash_mode: material-v1
  - path: 01-canonical/entities/{client-co}.md
    hash: sha256:1234567890ab
    hash_mode: material-v1
  - path: 02-working-memory/decisions.md
    hash: sha256:abcdef012345
    hash_mode: material-v1
  - path: 02-working-memory/log/{YYYY-MM-DD}-client-co-kickoff.md
    hash: sha256:fedcba987654
    hash_mode: material-v1
kind: briefing
case: client-co-strategic-review
confidentiality: internal
confidence: medium
notes: |
  Stakeholder data is partial — three named contacts still marked
  TODO. Resolve before this briefing is used in-meeting.
---

# Briefing — Scenario modeling workshop

## Purpose

Prepare the workshop team for scenario modeling on {Client Co}'s
business-line exit decision.

## Context

{summary drawing from identity and context}

## Scope

- In: three core BUs (per `scope.md`)
- Out: remaining BUs

[... rest of briefing ...]
```

5. Tells the user: *"Briefing written to
   `03-derived/briefings/{YYYY-MM-DD}-scenario-modeling-briefing.md`.
   4 pages, built from 6 Layer 1/2 inputs. Want me to summarize key
   points here?"*

The skill does not dump the full briefing into chat. The file is
the deliverable.

---

## Example 7 — Staleness detection and regeneration

**Context:** two weeks after the briefing was generated, the user
updates `scope.md` — scope expanded to include a fourth BU after all.

When the user makes the scope change, the skill:

1. Updates `scope.md`.
2. Adds a Change Log entry on `scope.md`.
3. Re-hashes `scope.md` and scans Layer 3 for artifacts that list
   `scope.md` as an input.
4. Finds the scenario modeling briefing; the stored hash for
   `scope.md` no longer matches. Opens the briefing. Adds at the top:

```markdown
> ⚠️ **Stale**: one or more inputs to this artifact changed on
> {YYYY-MM-DD}. Consider regenerating. Changed inputs:
> 01-canonical/scope.md.
```

5. Tells the user:

> Scope updated. I flagged 1 derived artifact as stale:
> `03-derived/briefings/{YYYY-MM-DD}-scenario-modeling-briefing.md`.
> Regenerate now, or leave it for later?

User says regenerate. Skill rebuilds the briefing with fresh inputs
and updated provenance hashes. The prior version moves to
`03-derived/_archive/briefings/`.

---

## Example 8 — A Cortex answering a question

Three weeks into the {Codename} investigation case. User asks: *"Who
was that controller at the subsidiary again?"*

The skill:

1. Reads `01-canonical/index.md` to find entity pages tagged with the
   subsidiary.
2. Loads `01-canonical/entities/{person-b-slug}.md`.
3. Responds: *"Per
   `01-canonical/entities/{person-b-slug}.md`, the controller at the
   subsidiary is {Person B}. Reports to CFO {Person A}."*

The skill does not guess, does not search the web, does not
re-derive. The Cortex is the source.

If the answer were not in the Cortex, the skill would say so
explicitly and offer to add it to `open-questions.md` for tracking.

---

## Example 9 — A lint report

After three months of work on the {Client Co} case, the user runs
Workflow 6: *"Lint the cortex. Anything stale?"*

The skill scans every layer and writes
`03-derived/lint/{YYYY-MM-DD}-lint-report.md`:

```markdown
---
generated_at: {YYYY-MM-DDTHH:MM:SSZ}
generator: case-cortex skill — Workflow 6 (Lint)
inputs:
  - {all Layer 1, 2, 3, 4 files scanned}
kind: lint-report
case: client-co-strategic-review
---

# Cortex Lint — client-co-strategic-review — {YYYY-MM-DD}

## Summary

1 blocker, 4 warnings, 6 nits. Cortex is broadly healthy but a
stale briefing and an open question that has silently become a
fact need attention.

## Blockers

1. **Layer 3 contradicts current Layer 1** —
   `03-derived/briefings/{YYYY-MM-DD-old}-scenario-modeling-briefing.md`
   asserts "the fourth BU is excluded from scope" but `scope.md`
   was updated {YYYY-MM-DD-newer} to include it. Briefing is
   already flagged Stale but has not been regenerated. Suggested
   fix: regenerate the briefing with current inputs.

## Warnings

1. **Empty Description on concept page** —
   `01-canonical/concepts/regulatory-context.md` has only a
   Definition. Suggested fix: re-read source pointer-id
   {pointer-id} and fill the Description.
2. **TODO older than 90 days** —
   `01-canonical/entities/{auditor-slug}.md` line 18 has
   `TODO: confirm signed-off auditor partner` from {date} ({N}
   days). Suggested fix: resolve or escalate.
3. **Open question has silently become a Layer 1 fact** —
   `concepts/dividend-policy.md` Definition states "{specific
   number}% of EBT distributed annually" but `open-questions.md`
   still lists this as open with no `[resolved]` marker.
   Suggested fix: add a resolution entry to `open-questions.md`
   or strip the assertion from the concept page.
4. **Cortex has not had a review pass in 96 days** — `cortex.yaml`
   `last_reviewed: {date}`. Suggested fix: do a review pass and
   update the field.

## Nits

1. **Concept page with no cross-links** —
   `concepts/budget-constraint.md` has empty Related concepts.
   Suggested fix: add 1–2 related links.
2. **Missing description on a Layer 4 pointer** —
   `04-pointers/external.yaml` entry `{pointer-id}` has no
   `description` field. Suggested fix: add a one-liner.
3. **Date format deviation** —
   `02-working-memory/log/{YYYY-MM-DD}-meeting.md` uses
   `12-Mar-2026` in the body. Suggested fix: convert to ISO.
4. **Orphan file** — `03-derived/working-notes/scratch.md` has no
   inbound links. Suggested fix: link from a log entry, archive,
   or delete.
5. **Skeleton file claim without provenance** —
   `context.md` line 18 asserts "{specific competitor} is the main
   competitor" without a pointer. Suggested fix: add pointer or
   downgrade to TODO.
6. **Concept page slug duplicates an alias** —
   `concepts/cm1.md` aliases include "Contribution Margin 1" but
   `concepts/contribution-margin-1.md` also exists. Suggested fix:
   merge under one canonical slug.

## Not checked

- Remote pointer HTTP-resolution (skipped by default; user can
  request network-lint to enable).
- Git-history append-only check on `decisions.md` (no git repo
  initialised in this Cortex; using content-hash comparison
  instead).
```

The skill tells the user:

> Lint found 1 blocker, 4 warnings, 6 nits. Top issue: the scenario
> modeling briefing contradicts current scope — needs regeneration.
> Want me to walk through fixes?

The lint report is itself a Layer 3 artifact. The next lint pass will
move this report to `03-derived/_archive/lint/` and write a fresh
report at the active path.

---

## Anti-examples — don't do these

### Don't invent facts about the world when sources are missing

**Bad:**

```markdown
- {Client Co} is headquartered in {a specific city}.
```

(No one said this. Don't write it.)

**Good:**

```markdown
- TODO: confirm {Client Co} headquarters location.
```

### Don't suppress synthesis on entity or concept pages

**Bad:** A concept page with a one-line Definition and an empty
Description, citing "never invent facts" as the reason.

**Good:** A concept page with a rich Description grounded in the
source, plus a `> Synthesis:` block where you name patterns the
source implies. Synthesis is allowed when marked as such.

### Don't edit Layer 2 decisions retroactively

**Bad:** user says "actually we changed our mind on the approach".
The skill edits the prior decision entry to say "Use Approach B".

**Good:** The skill appends a new decision entry dated today,
explaining the reversal, and adds `**Superseded by:** [→ {new
date} decision]` to the original entry.

### Don't skip provenance

**Bad:** Layer 3 briefing without frontmatter. Six weeks later, no
one knows which Cortex state it was built from.

**Good:** frontmatter with `inputs:` listing every Layer 1/2 file
read, with content hashes (or commit hashes when git is available).

### Don't dump the full artifact into chat

**Bad:** user asks for a briefing. The skill writes a 2000-word
briefing directly in the chat turn.

**Good:** The skill writes the briefing to `03-derived/...`, tells
the user where it is, and offers a short summary on request.

### Don't bump synthesis date stamps when nothing materially changed

**Bad:** Every Ingest, regardless of impact, edits `synthesis.md` to
update the date in frontmatter, leaving body unchanged.

**Good:** `synthesis.md` is touched only when the Ingest *materially*
shifted the view. Lint detects staleness via content hash, not mtime
— a date-only edit produces no signal and creates noise.
