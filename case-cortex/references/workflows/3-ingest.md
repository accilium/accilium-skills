# Workflow 3 — Ingest

> **This is the fan-out primitive.** A source rarely teaches one
> thing; it usually teaches 10–30 things that map to distinct
> entities, concepts, relationships, or mechanisms. Ingest fans the
> source out into **one page per entity and one page per concept**,
> not a single summary. If you produce one summary and leave the
> Cortex otherwise unchanged, you have done it wrong.

**Read `references/ingestion.md` before running this workflow for
the first time in a session.** It contains the detailed methodology,
worked examples, and the enumeration heuristics. The summary below
is the operating procedure; the reference is the substance.

This workflow applies only to **full-mode** Cortexes. If the Cortex
is in minimal mode and the user wants to ingest a substantial source,
trigger the migration offer first (see
`references/workflows/1-initialize.md` "Migrating minimal → full").

---

## Source-isolation rule (read first)

Ingest writes the largest volume of content into the Cortex per
operation, so a contamination here is also the largest. The rule:

> **Pages produced by Ingest reflect only what is in the source
> the user named. Nothing else.**

Concretely:

- An entity page exists only if the source mentions a named
  entity. Don't pre-populate "obvious" entities the user "must
  also be dealing with" based on memory or general knowledge.
- A concept page captures only definitions, mechanisms, or terms
  the source actually uses. Don't add concepts from sibling skills
  loaded in the session, from the LLM's general knowledge of the
  domain, or from prior cases the user worked on.
- Identity facts on entity pages come from the source. If the
  source says "the auditor was {Firm}", the auditor entity gets
  that name and a TODO for everything else — not a guess from
  general knowledge about which auditor "{Firm}" probably refers
  to.
- KPI definitions, abbreviations, formulas, and acronyms come
  from the source's defined-terms list, legend, or context. If
  the source uses "CR4" without defining it, the concept page
  for `cr4` carries the source's usage and a TODO for the
  definition — not a borrowed definition from another case.
- Tool names, system names, vendor names: source only. If memory
  says the user uses Tool X for everything, but the source
  doesn't mention Tool X, Tool X is not in the Cortex.

If the source is truly silent on something the user clearly
expects, ask:

> The source doesn't mention {topic} but you've referenced it.
> Should I add that as user-asserted content (which I'll mark as
> such), or wait for a source that covers it?

When in doubt, leave a TODO. TODOs are cheap; phantom facts are
expensive.

---

## Goal

Take a source (document, workbook, meeting transcript, brief,
webpage, email thread) and turn it into structured, richly described
content under Layer 1 (`entities/`, `concepts/`, `sources/`, plus
skeleton and spine updates) with provenance.

---

## The procedure (refer to `ingestion.md` for detail)

### 3.1 — Stage provenance

Create or update a Layer 4 pointer for the source. Determine
confidentiality. Clarify intent (full-fan or scoped-fan).

### 3.2 — Read and enumerate

Read the source carefully. Produce **two enumeration lists**: one
for entities, one for concepts. Apply the routing rules from
SKILL.md ("Entity vs. concept — the routing primitive"). Target
**10+ entries combined from a substantive source**.

**Show the enumeration to the user before writing pages.** This is
cheap and prevents wasted writing on items the user considers out
of scope.

For large sources, chunk the confirmed enumeration before writing:

- Work in batches of at most **5 entity/concept pages combined**.
- After each batch, update the affected pages and `index.md`, then do
  a quick link/provenance sanity check before continuing.
- Show the user a short checkpoint after each batch: pages written,
  pages still queued, any uncertain routing decisions.
- If code execution is available, use it for mechanical checks such as
  hash computation, file existence, duplicate slugs, and link
  validation. Do not spend LLM attention on arithmetic or filesystem
  bookkeeping when a helper can do it reliably.

### 3.3 — Write the pages

- For each confirmed entity → `01-canonical/entities/{slug}.md`
  using `templates/entity-template.md`.
- For each confirmed concept → `01-canonical/concepts/{slug}.md`
  using `templates/concept-template.md`.

If a page already exists, update it (append identity facts, extend
description, add footprint row, append source pointer). Do not
overwrite. Add a Change Log entry.

Write richly. A page with only a 1-line definition and no
description is a failure mode. Cross-link eagerly — every page
needs at least one outbound link.

### 3.4 — Write the source summary (mandatory)

`01-canonical/sources/{YYYY-MM-DD}_{source-slug}.md` using
`templates/source-summary-template.md`. Its frontmatter uses
`sources:` to point back to the Layer 4 pointer for the ingested
source. Lists every entity and
concept page generated or updated.

### 3.5 — Update skeleton files as indexes

`identity.md`, `scope.md`, `context.md` get new pointer lines into
the entity and concept pages. Skeleton files stay short and
index-like — no rich content duplication.

### 3.6 — Update the spine files

- `index.md` — add new entries under entities, concepts, sources
  sections. **Mandatory.**
- `synthesis.md` — update only if the Ingest *materially* shifted
  your view. Do not bump the date for a no-change Ingest. **Update
  conditionally.**
- `overview.md` — touch only on major framing changes. **Optional.**

This step prevents the meta-layer gap. Do not skip it.

### 3.7 — Record open questions

Concept-specific → on the concept page. Entity-specific → on the
entity page. Case-level → `02-working-memory/open-questions.md`.

### 3.8 — Log the ingest

`02-working-memory/log/{YYYY-MM-DD}-ingested-{source-slug}.md`.
Summary of pages created/updated, skeleton/spine updates, open
questions added, honest state.

### 3.9 — Optional Layer 3 structural briefing

For genuinely complex sources (multi-sheet workbooks, long policy
docs), optionally write
`03-derived/briefing/{YYYY-MM-DD}-{source-slug}.md` mapping the
source's *structure*. Skip for the common case.

### 3.10 — Report back to the user

> Ingested {source}. Created/updated {E} entity pages and {C}
> concept pages, wrote source summary at `{path}`, updated {M}
> skeleton files, updated index and synthesis, added {K} open
> questions, logged the ingest. Top items: {1}, {2}, {3}. Want me
> to walk through any of them?

Do not dump the entity or concept pages into chat. The files are
the deliverable.

### 3.11 — Offer a lint pass

After any substantial Ingest (5+ entity or concept pages), offer
to run Workflow 6 (Lint) to catch under-ingestion, missing
cross-links, mis-routed pages, and empty Descriptions early.
