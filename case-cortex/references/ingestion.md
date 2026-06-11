# Case Cortex — Ingestion methodology (the fan-out primitive)

Read this file before the first Ingest in any session. It is the single
most important reference for avoiding the **thin-cortex failure mode**:
a Cortex with a sparse 4-file skeleton and all the richness buried in a
single disposable briefing. That failure mode is what you get when you
apply the skill timidly; what follows is how to apply it the way the
LLM-native wiki pattern intends.

---

## The rule, in one line

> **One source touches many pages.** A substantive source fans out into
> 10+ entity *and* concept pages combined, not a single summary.

Everything in this file is a consequence of that rule. The split
between entity pages (`01-canonical/entities/`) and concept pages
(`01-canonical/concepts/`) reflects a fundamental asymmetry — the same
source teaches things that *act* (entities) and things that *describe
how something works* (concepts), and they need different shapes.

---

## Why this matters (read once, internalise)

The Cortex's value compounds only if richness accumulates. Accumulation
requires *many pages* that can be *cross-referenced* and *updated
independently*. A single briefing per source doesn't accumulate — it
shadows the next briefing and gets superseded. Concept and entity pages
accumulate because each one is independently referenceable, independently
update-able, and independently cite-able from any number of derived
artifacts.

The failure mode this file exists to prevent:

> A model ingested a substantive source and produced: a 1-page glossary
> + a 1-page structural briefing + updates to 4 skeleton files. The
> same source, in a fan-out pass, produces 20+ pages. Same source,
> same model, different instructions, different artifacts. This file
> is the "different instructions."

---

## The operating procedure — step by step

### Phase 1 — Pre-read

Before opening the source:

1. **Stage the pointer.** Create or update a Layer 4 entry in
   `systems.yaml` or `external.yaml` for the source. Assign it an `id`.
   Every page derived from this source will cite that `id`. For a
   source that exists only in the conversation (a pasted brief,
   dictated text), there is no real locator — use
   `url: conversation:{YYYY-MM-DD}` and note in the `description`
   that the content is preserved in the Phase 3.5 source summary.
2. **Determine confidentiality.** Public, internal, restricted,
   confidential — propagate to every derived page.
3. **Clarify intent.** Is the user bringing this source in to (a) get
   everything in it into the Cortex, or (b) answer a narrow question
   from it? For (a), run the full fan-out; for (b), run Ingest but
   scope the enumeration to the user's question, and note the
   remainder as a TODO for a future full-ingest pass.

### Phase 2 — Read and enumerate

Read the source once, front to back, and produce **two enumeration
lists**: one for entities (named real-world things with identity that
*act*) and one for concepts (mechanisms that *describe how something
works*). Target **10+ entries combined from a substantive source**. If
you get 2–3, you have under-read.

Routing rules are in `SKILL.md` ("Entity vs. concept — the routing
primitive"). Apply them strictly during enumeration.

#### What goes into the entity list (`01-canonical/entities/`)

Things that have **identity** and *act* in the case:

- **Persons** — people who play a role (clients, counterparties,
  advisors, regulators, internal stakeholders).
- **Organisations** — firms, agencies, teams, suppliers, peer
  comparators.
- **Legal entities** — specific named legal entities by their full
  name. (A group of legal entities under common ownership: each gets
  its own page.)
- **Products / systems** — named software, named contracts, named
  datasets, named tenders, named programmes.
- **Regulators / jurisdictions** — when their identity matters (a
  specific regulatory body by name — not generic "the regulator").

#### What goes into the concept list (`01-canonical/concepts/`)

Things that *describe how something works*:

- **Mechanisms and calculations** — formulas, pricing rules,
  allocation methods, workflows, decision rules, rating or scoring
  scales.
- **Metrics and KPIs** — named measurable quantities with definitions.
- **Terms of art** — abbreviations, jargon, anything the source defines
  or uses with a specific in-case meaning.
- **Decision artifacts as concepts** — policies, standards, contract
  clauses, SLAs, tender criteria, regulatory obligations. (The clause
  is a concept; the firm that drafted it is an entity. Cross-link
  them.)
- **Regimes and regulations** — the *regime* is a concept; the
  *regulator* that issues it is an entity.
- **Relationships** — only if load-bearing (e.g. a structural pattern
  of interaction between entities is a concept; "two people emailing
  each other" is not).

#### Enumeration heuristics

- **Scan the table of contents, headings, sheet names, defined-terms
  lists, and legends.** These are pre-enumerated by the source's
  author.
- **Read tables column by column.** Every column header is a concept
  candidate.
- **Treat every abbreviation as a candidate.** If the source uses an
  abbreviation without ever spelling it out, that's still a concept
  page — its first job may be to capture "definition unknown / TODO".
- **Don't deduplicate too aggressively.** Two concepts that look
  related but have different mechanics or definitions deserve separate
  pages. Link them, don't collapse them.
- **Do deduplicate aliases.** If a concept has three names in the
  source, pick one as the canonical page slug and list the others in
  `aliases` frontmatter.

**Before writing any pages, show both enumeration lists to the user.**
Format:

> I read the source and enumerated {E} entity candidates and {C}
> concept candidates. Before I write the pages, here are the lists.
> Flag any that are out of scope, any that I missed, any that should
> merge, and any I routed wrongly between entity / concept:
>
> **Entities** (→ `01-canonical/entities/`)
> 1. {slug} — {one-line what-it-is}
> 2. {slug} — {one-line what-it-is}
> ...
>
> **Concepts** (→ `01-canonical/concepts/`)
> 1. {slug} — {one-line what-it-is}
> 2. {slug} — {one-line what-it-is}
> ...

This is cheap and prevents wasted writing, and it gives the user a
chance to flag mis-routed items before they live as files.

### Phase 3 — Write one page per entity and one page per concept

#### Phase 3a — Entity pages

For each confirmed entity, create or update
`01-canonical/entities/{slug}.md` using `templates/entity-template.md`.
If a page already exists, *update* it: append new identity facts,
extend the description, add a row under footprint for this source's
event, and append the source pointer to frontmatter `sources:`. Do not
replace existing content; entities accumulate identity across sources.
Add a Change Log entry.

Entity slugs are stable. Once a slug exists, every later source that
mentions the entity uses that slug. If the entity renames or acquires
a new alias, add it to `aliases:` rather than renaming the file.

Critical writing rules for entity pages:

- The identity-facts section is short and structured. Adjust by
  `entity_type`: people get role/title/team; organisations get legal
  form/seat/registration number; products get version/owner.
- The description is rich prose. Same richness expectation as concept
  pages — 3–10 sentences for any non-trivial entity.
- The role-in-case section is what distinguishes this page from a
  Wikipedia stub. What does this entity *do* in this case? What
  decisions do they own? What artefacts do they produce?
- The footprint accumulates over time. Every Ingest that references
  this entity should add a row.
- Cross-link to entities they deal with and concepts they apply.

#### Phase 3b — Concept pages

For each confirmed concept, create `01-canonical/concepts/{slug}.md`
using `templates/concept-template.md`. Write each page *as if* a new
reader landing on it has never seen the source.

Critical writing rules:

**The Description section is where the Cortex earns its richness.**
Aim for 3–10 sentences of actual description for any non-trivial
concept. Describe:

- What the concept is
- How it works (mechanism, formula, process)
- What depends on it / what it depends on
- When it applies and when it doesn't
- Edge cases or variants
- Why it matters in this case

If the source is thin on a concept but the concept is load-bearing,
write what you can and flag the gap as a TODO **within** the
Description — do not leave the Description empty. An empty Description
is a lint **warning**.

**Cross-link eagerly.** Every concept page should link to at least one
other concept or entity. Two links is better. Five is fine. The Cortex
gets its power from the graph — a concept page with no outgoing edges
is a node disconnected from the graph.

**Use the Synthesis block for interpretation.** If you notice a
pattern the source implies but doesn't state — a tension, a
redundancy, a gap, a likely next decision — name it in `## Synthesis`.
That section is explicitly *not* fact-ground; it's declared
interpretation. The rule "never invent facts" can get over-applied and
suppress this kind of useful synthesis. Mark it and write it.

**Cite provenance.** Every factual claim that came from the source
should be referencable to that source via the `sources:` frontmatter
and, where the claim is non-obvious, an inline pointer tag.

### Phase 3.5 — Write the per-source summary (mandatory)

After the entity and concept pages are written, write
`01-canonical/sources/{{YYYY-MM-DD}}_{{SOURCE_SLUG}}.md` using
`templates/source-summary-template.md`. This is the LLM's reading
notes on the source — narrative-shape, distinct from the fact-shape
entity and concept pages. TL;DR, parties involved, structural
breakdown, key facts, notable quotes, takeaways. The frontmatter
cites the Layer 4 pointer via `sources:`. The body lists every
entity page generated or updated under `## Generated entity pages`
and every concept page under `## Generated concept pages`.

Why this is mandatory: a future reader (human or LLM) needs to be able
to ask "what did this source actually say?" without re-reading the raw
source. The entity and concept pages answer "what does this source
teach?" — they do not answer "what is this source about?". Both
questions are common; both must be cheap to answer from the Cortex.

### Phase 4 — Update skeleton files as indexes

After the entity and concept fan-out, update the Layer 1 skeleton
files so they become a map into the entity and concept graph:

- `context.md` gets lines pointing into `concepts/` for any background
  concept and into `entities/` for any background organisation /
  regulator / jurisdiction that now has a dedicated page.
- `scope.md` gets lines pointing into `entities/` and `concepts/` for
  any in-scope element that now has a dedicated page.
- `identity.md` rarely needs cross-links, but add them if the case's
  identity references a specific KPI, mechanism, or named entity that
  now has a page.

Skeleton files stay **short and index-like**. Do not duplicate content
from the entity or concept pages into the skeleton files. Duplication
is drift waiting to happen — the two copies will eventually disagree.

Add a Change Log line on every skeleton file you edit.

### Phase 4.5 — Update the spine files

The spine files (`overview.md`, `synthesis.md`, `index.md`) are
first-class Layer 1 files and must be updated on every Ingest. This
is the mechanism that prevents the **meta-layer gap** — the failure
mode where concept pages get rich but synthesis and the index drift
behind reality.

For every Ingest:

- **`index.md`** — append every new entity page under the entities
  section's appropriate cluster, every new concept page under the
  concepts section's appropriate cluster, and the new source summary
  under sources. If a new item doesn't fit any existing cluster,
  propose a new cluster heading. The index is what the user navigates
  by; if it's stale, the Cortex is harder to use even when the
  underlying pages are fine. **Mandatory.**
- **`synthesis.md`** — update the relevant section if the Ingest
  *materially* shifted your view of the case. New sources often
  surface new open risks, parameter calibrations, or design patterns.
  If the Ingest did not shift your view, **do not** touch the file
  just to bump a date. Lint detects material staleness via content
  hash, not mtime — a date-only edit produces no signal and a
  no-change-needed Ingest should leave synthesis alone. **Update
  conditionally.**
- **`overview.md`** — touch only if the Ingest materially changed the
  case framing (new stakeholder cluster, redefined scope, new
  motivation). Always update the "where to start reading" pointer
  list if there are now new prominent concepts a new reader should be
  sent to. **Optional but expected for major Ingests.**

This phase is roughly 5–15 minutes of work after a substantive Ingest.
Skipping it is the single biggest predictor of a Cortex that becomes
unusable after 5–10 Ingests.

### Phase 5 — Record open questions

For every gap or ambiguity found during Ingest:

- **Entity-specific** questions → `## Open questions` section on the
  relevant entity page.
- **Concept-specific** questions → `## Open questions` section on the
  relevant concept page.
- **Case-level** questions → append to
  `02-working-memory/open-questions.md`.
- **Source-acknowledged** unresolved items → preserve with attribution
  (`(source flags this as open)`) on the relevant entity or concept
  page, *and* mirror to `open-questions.md`.

### Phase 6 — Log the ingest

Write `02-working-memory/log/{YYYY-MM-DD}-ingested-{source-slug}.md`:

```markdown
# Ingested {source name}

**Date:** {YYYY-MM-DD}
**Source:** [→ pointers/{file}.yaml#{pointer-id}]
**Confidentiality:** {public | internal | restricted | confidential}

## Enumeration

{E} entity candidates and {C} concept candidates identified.
{written / deferred / merged breakdown}.

## Entity pages created

- `entities/{slug-1}.md` — {one-line}
- `entities/{slug-2}.md` — {one-line}
- ...

## Entity pages updated

- `entities/{existing-slug}.md` — {what changed: new identity facts,
  new footprint row, new relationship}

## Concept pages created

- `concepts/{slug-1}.md` — {one-line}
- `concepts/{slug-2}.md` — {one-line}
- ...

## Concept pages updated

- `concepts/{existing-slug}.md` — {what changed}

## Source summary

- `01-canonical/sources/{YYYY-MM-DD}_{slug}.md` — created.

## Spine updates

- `index.md` — added entries under entities, concepts, sources.
- `synthesis.md` — {updated section X | unchanged}.
- `overview.md` — {touched / not touched}.

## Skeleton updates

- `context.md` — added index links for {list}
- `scope.md` — added index links for {list}
- ...

## Open questions raised

- {question 1}
- {question 2}

## Honest state

What is **locked in** from the source: {list}.
What was **inferred / synthesised**: {list, referring to Synthesis sections}.
What is **still TODO**: {list}.
```

This log entry is the only place the full shape of the ingest lives.
Future audit, lint, and "why does this concept page exist?" questions
trace back here.

### Phase 7 — Optional Layer 3 structural briefing

If the source is structurally complex (a multi-sheet workbook, a long
policy document, a detailed tender pack), and Phase 3.5's source
summary doesn't give a complete enough map of the source's
*organisation*, write a separate Layer 3 briefing at
`03-derived/briefing/{YYYY-MM-DD}-{source-slug}.md` that maps the
source's structure — what's in it, how it's arranged, where to look
for what.

Distinction from Phase 3.5:

- `01-canonical/sources/{date}_{slug}.md` — *what the source says*.
  Mandatory for every Ingest.
- `03-derived/briefing/{date}-{slug}.md` — *how the source is
  organised*. Optional. Only for genuinely complex sources where a
  reader benefits from a structural map distinct from the narrative
  summary.

Skip this step in most Ingests. The Phase 3.5 source summary handles
the common case.

### Phase 8 — Report back

Tell the user:

> Ingested {source}. Created {E} entity pages and {C} concept pages,
> wrote source summary `{path}`, updated spine ({index | synthesis |
> overview}), updated {M} skeleton files, {K} new open questions. Top
> entities: {1}, {2}; top concepts: {1}, {2}, {3}. {Optional:
> structural briefing at {path}.} Want me to walk through anything?

Do not dump entity or concept pages into chat. The file tree is the
deliverable.

### Phase 9 — Offer a lint pass

After any substantial Ingest (5+ entity or concept pages), offer to
run Workflow 6 (Lint) to catch under-ingestion, missing cross-links,
mis-routed pages (entity content under `concepts/` or vice versa),
and empty Descriptions early. This is cheap and keeps the Cortex
honest.

---

## Enumeration heuristics — worked example

A financial-controlling workbook for a multi-entity group has these
sheets: `Overview`, `Revenue`, `OpEx`, `People Cost`, `Pyramid`,
`Compensation`, `Ownership`, `Legend`.

A thin ingest might produce 2 concept pages (`Revenue` and `OpEx`)
plus a briefing. That's under-reading.

A proper enumeration reads each sheet and pulls out every defined
term, line item, mechanism, **and named entity**. Example partial
list, already split into the two routings:

**Entities** (→ `01-canonical/entities/`)

1. `{firm}-uk` — UK legal entity (legal form, registration, seat, role in case)
2. `{firm}-nl` — Dutch legal entity
3. `{firm}-es` — Spanish legal entity

**Concepts** (→ `01-canonical/concepts/`)

1. `revenue` — top-line driver
2. `contribution-margin-1` — first profitability checkpoint (defined on `Overview`)
3. `contribution-margin-2` — second profitability checkpoint
4. `ebit` — earnings before interest and tax
5. `ebt` — earnings before tax
6. `bill-rate` — hourly/daily sell rate per role
7. `utilisation` — target vs. actual utilisation per role
8. `pyramid` — role mix convention
9. `senior-role` — senior role definition (abbreviation on `Pyramid`)
10. `manager-role` — manager role definition
11. `staff-role` — staff role definition
12. `target-bonus` — target bonus per role (on `Compensation` sheet)
13. `payroll-overhead-factor` — payroll overhead factor per entity (on `Compensation`)
14. `bonus-split` — individual vs. company component of the bonus
15. `profit-share-pool` — partner profit-share mechanism (on `Ownership` sheet)
16. `equity-buy-in` — partner equity buy-in mechanism (on `Ownership`)
17. `valuation-approach` — how ownership stakes are valued
18. `corporate-tax-rate` — per-entity tax assumption (cross-links to the three entity pages above)
19. `dividend-policy` — (flagged as open in source)
20. `time-basis` — working-days / hours-per-year convention

3 entity pages + 20 concept pages from one workbook = 23 Layer 1
pages. That is the target density. Each page a few hundred words of
description, cross-linked to its neighbours, with the entity pages
carrying identity facts (legal form, registration, seat) that the
concept pages cite. The resulting Cortex is a graph, not a skeleton
with a summary bolted on.

The key move: legal entities go to `entities/` (they pay tax, sign
contracts, hire staff); the *mechanism* that calculates their tax
goes to `concepts/`. Cross-link them. The edge from
`corporate-tax-rate.md` → `entities/{firm}-uk.md` is what makes the
graph navigable.

---

## Failure modes to watch for

| Symptom | What went wrong | Fix |
|---|---|---|
| Ingest produced 1–3 entity/concept pages combined | Under-enumeration | Re-read the source; look for tables, legends, defined-terms lists, abbreviations, named parties |
| Concept pages have empty Descriptions | Principle "never invent facts" mis-read as "never write" | Synthesis within marked sections is allowed; describe what you read |
| All the richness is in a single briefing | Skipped Phase 3; went straight to Phase 7 | Regenerate: write entity and concept pages first, briefing last (or not at all) |
| Pages don't link to each other | Missed cross-linking | Every page needs Related/Relationships with 1+ entries |
| Skeleton files got rewritten with rich content | Skipped Phase 4; duplicated into the index | Strip skeleton files back to index lines pointing into `entities/` and `concepts/` |
| Multiple pages describe the same thing | Missed deduplication at enumeration time | Merge: pick one canonical slug, add the others to `aliases` |
| Named entities (people, firms, regulators) live under `concepts/` | Phone-call test not applied | Move the page to `entities/{slug}.md`, swap to entity template, fill in identity facts and footprint. Update inbound links |
| Mechanisms or KPIs live under `entities/` | Routing inverted | Move to `concepts/{slug}.md` with concept template. The thing doesn't act in the world; it describes how something works |
| Entity pages have empty identity facts | Identity not captured | Re-read source for legal form, seat, registration, role, dates. If genuinely unknown, leave a TODO row and a question in Open questions |
| TODO markers pile up but never get closed | Ingesting new sources without closing prior TODOs | Offer Lint (Workflow 6); aged TODOs are a lint warning |

---

## Tone — write for a future reader

The future reader of an entity or concept page is not the user who
asked for the Ingest. It is:

- The user, 3 months from now, who can't remember why a particular
  KPI is defined this way.
- A new team member onboarding onto the case.
- Another agent, in a different session, trying to answer a narrow
  question that touches this concept.
- An LLM generating a briefing that needs to cite this concept.

Write for them. Dense, richly described, cross-linked pages serve
them. Sparse skeletons do not.
