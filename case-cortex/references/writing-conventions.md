# Case Cortex — writing conventions

Small rules that make the Cortex consistent across cases, authors, and
sessions. Apply these always unless the user explicitly overrides via
`CLAUDE.md`.

---

## Language defaults

The skill defaults to **English** for all section headings, frontmatter
keys, and template fields. If the user wants a different language for
the case content, they declare it in `CLAUDE.md` section 3 (Language
convention) and the skill follows that override on subsequent edits.
Frontmatter keys remain English regardless of case language; only
values and body text follow the case language.

`CLAUDE.md` itself is always written in English — it is the LLM's
schema document, not case content.

For non-English Cortexes, maintain the heading map in `CLAUDE.md`
section 3. Use that map consistently when translating recurring page
headings such as Description, Role in case, Relationships, Footprint,
Open questions, Synthesis, and Change Log.

---

## Dates

- Always **ISO format**: `YYYY-MM-DD` for dates,
  `YYYY-MM-DDTHH:MM:SSZ` for timestamps.
- No `today`, `yesterday`, `last week` — resolve to absolute dates
  when writing.
- Time zones: UTC in machine-generated timestamps; local time
  acceptable in human-written notes if the time zone is stated.

---

## Headings

Every Layer 1 and Layer 2 file starts with an H1 that matches the
filename in human-readable form. Example: `identity.md` starts with
`# Identity`, `entities/example-corp.md` starts with `# Example Corp`.

Within files:

- **H2** for top-level sections
- **H3** for sub-sections
- **H4** sparingly, for nested attributes

Never skip heading levels.

---

## Structure over prose — except on entity and concept page descriptions

Prefer on **skeleton files**, **log entries**, **decisions**,
**pointers**, **spine files**:

- **Bullet lists** for parallel items
- **Tables** for attribute-heavy content
- **Definition lists** (`Name\n: Description`) for short labelled
  entries
- **Short paragraphs** (2–4 sentences) for genuinely narrative content

Avoid long flowing paragraphs on skeleton files. Skeleton files are
indexes; structure helps both agents and humans skim.

On **entity pages** (`01-canonical/entities/*.md`) and **concept pages**
(`01-canonical/concepts/*.md`), the rules invert. The Description
section is the point of the page and is *expected* to be rich
descriptive prose. Aim for 3–10 sentences on any non-trivial page.
Bullet lists and tables are fine where they fit (an entity's
identity-facts list is naturally a list, a concept's trade-offs benefit
from structure), but a page that is all bullets and no description is
a thin-cortex failure mode (see `ingestion.md`).

---

## Citations and pointers

When a Layer 1 claim has a source, cite it inline:

```markdown
- {{SUBJECT}} {{ASSERTION}} [→ pointers/external.yaml#{{POINTER_ID}}]
```

Formats accepted:

- `[→ pointers/{file}.yaml#{anchor}]` — internal pointer reference
- `[→ 02-working-memory/log/{YYYY-MM-DD}-{slug}.md]` — user assertion
  captured in a dated Maintain log entry
- `[→ {relative/path/to/file}]` — relative link to another file in the
  Cortex
- `[→ https://...]` — direct external URL (use sparingly; prefer
  pointer entries)

For working memory entries, cite the source of information if it's
not self-evident:

```markdown
- {{YYYY-MM-DD}} — {{EVENT}} [→ external#{{POINTER_ID}}]
```

## TODO format

Use dated TODOs so Lint can age them:

```markdown
TODO({{YYYY-MM-DD}}): {{SPECIFIC_QUESTION_OR_MISSING_FACT}}
```

Undated `TODO:` markers are allowed only during scratch drafting and
should be resolved before finishing the workflow; Lint flags them as
nits.

---

## Change logs on Layer 1 files

Every Layer 1 file has a `## Change Log` section at the bottom.
Format:

```markdown
## Change Log

- {{YYYY-MM-DD}} — {{ONE_LINE_SUMMARY_OF_CHANGE}}.
- {{YYYY-MM-DD}} — {{ONE_LINE_SUMMARY_OF_PRIOR_CHANGE}}.
- {{YYYY-MM-DD}} — Initial seeding.
```

Entries go newest-first. One line per change. If a change needs more
explanation, link to a Layer 2 log entry.

---

## Layer 2 log entries

Filename: `{{YYYY-MM-DD}}-{{SHORT_SLUG}}.md`. Slug is 2-5 words,
hyphenated, lowercase. Examples: `2026-04-22-kickoff-meeting`,
`2026-04-24-scope-change`.

Each entry has this skeleton:

```markdown
# {{TITLE}}

**Date:** {{YYYY-MM-DD}}
**Participants:** {{NAMES_OR_SOLO}}
**Related files:** {{OPTIONAL_POINTERS_TO_DOCUMENTS_DISCUSSED}}

## What happened

{{TWO_TO_FIVE_SENTENCES}}

## Decisions taken

- {{DECISION_1}}
- {{DECISION_2}}

## Open questions raised

- {{QUESTION_1}}

## Next steps

- {{ACTION}} — {{OWNER}} — {{DUE_DATE}}
```

Omit sections that don't apply. Never write a log entry with no
content just to have one.

---

## Decisions log format

`02-working-memory/decisions.md` uses append-only entries:

```markdown
## {{YYYY-MM-DD}} — {{DECISION_TITLE}}

**Context:** {{WHAT_WAS_OPEN_AND_ALTERNATIVES}}.
**Decision:** {{WHAT_WAS_CHOSEN}}.
**Rationale:** {{WHY_CONCRETE_NUMBERS_TRADE_OFFS_CONSTRAINTS}}.
**Superseded by:** —
**Related log:** [→ log/{{YYYY-MM-DD}}-{{SLUG}}.md]
```

When a later decision reverses or updates a prior one, **do not edit
the substance of the old entry**. Write a new entry and add a
`**Superseded by:**` line to the original pointing to the new entry's
date-slug.

Benign edits to existing entries (typos, formatting fixes,
frontmatter corrections) are permitted in place. Substantive changes
— anything that alters meaning, decision content, rationale, or
related artifacts — must be a new superseding entry.

---

## Open questions format

`02-working-memory/open-questions.md` is a live list:

```markdown
## Open

- **{{QUESTION}}**
  - Raised: {{YYYY-MM-DD}} in [→ log/{{YYYY-MM-DD}}-{{SLUG}}.md]
  - Why it matters: {{CONCRETE_CONSEQUENCE_IF_UNRESOLVED}}.

## Resolved

- **{{QUESTION}}** — [resolved {{YYYY-MM-DD}}: {{ANSWER}}, see
  pointers/{{FILE}}.yaml#{{ID}}]
```

Keep the Resolved section for audit trail. Do not delete resolved
questions.

---

## Layer 3 artifact frontmatter

Every derived artifact starts with YAML frontmatter. See
`templates/derived-artifact-header.md` for the full template. Minimum:

```yaml
---
generated_at: {{YYYY-MM-DDTHH:MM:SSZ}}
generator: {{SKILL_NAME_OR_MANUAL}}
inputs:
  - path: 01-canonical/identity.md
    hash: sha256:{{FIRST_12_CHARS}}
    hash_mode: material-v1
  - path: 01-canonical/entities/{{SLUG}}.md
    hash: sha256:{{FIRST_12_CHARS}}
    hash_mode: material-v1
  - path: 02-working-memory/decisions.md
    hash: sha256:{{FIRST_12_CHARS}}
    hash_mode: material-v1
kind: briefing | analysis | summary | report | recommendation | deck | model | memo
case: {{CASE_ID}}
confidentiality: public | internal | restricted | confidential
redaction: none | applied
---
```

`material-v1` hashes are preferred over mtimes and raw hashes because
they normalize away maintenance-only changes. Raw hashes are acceptable
but conservative: Change Log and whitespace edits can mark an artifact
stale. When git is available, commit hashes are acceptable. When
neither hash nor git is available, fall back to date-only markers
(`{{PATH}}@{{YYYY-MM-DD}}`) and the skill should tell the user
staleness detection is best-effort under that fallback.

Derived artifacts inherit the strictest confidentiality level of their
inputs. Public artifacts generated from restricted or confidential
inputs require a redaction pass plus `redaction: applied` and
`redaction_notes`.

---

## Spine files (`overview.md`, `synthesis.md`, `index.md`)

The three spine files in `01-canonical/` have distinct shapes and
distinct update cadences.

**`overview.md`** — narrative entry point. Use prose paragraphs, not
lists, for the *What is this case* and *Why does it exist* sections.
Keep it short (under 60 lines): a new reader should be oriented in
90 seconds. The "where to read next" section at the bottom is a
curated list of 3–5 pointers, not a flat dump. Update only when the
case framing materially changes; most Ingests do not require an
`overview.md` edit. See `templates/overview-template.md`.

**`synthesis.md`** — opinion-bearing. This is the one Layer 1 file
that is allowed to be wrong, allowed to evolve, allowed to contradict
its prior self as long as the supersession is dated. Sections have
fixed names (current direction, open risks, parameter calibrations,
chosen / rejected design patterns, benchmark gap, open questions by
topic block, parked items) so an LLM can reliably find each. Update
only on Ingests that *materially* shift your view — do not bump the
date on a no-change Ingest. Lint detects material staleness via
content hash, not mtime. See `templates/synthesis-template.md`.

**`index.md`** — curated catalog. Entities and concepts are listed
in distinct sections; within each, group by topical cluster, not
alphabetically. Add new cluster headings when concepts justify their
own grouping. Empty clusters are fine — they signal where future
Ingest work will land. See `templates/index-template.md`.

All three spine files have a `## Change Log` at the bottom.

---

## Source summaries (`01-canonical/sources/`)

One file per ingested source, named
`{{YYYY-MM-DD}}_{{SOURCE_SLUG}}.md` (the date prefix is the date of
ingest, not the date of the source). See
`templates/source-summary-template.md` for the full shape.

The frontmatter must include `sources:` pointing at the Layer 4
pointer for the source. The body must include a
`## Generated entity pages` section listing every entity page
generated or materially updated by this Ingest, and a
`## Generated concept pages` section listing every concept page
likewise. This is what makes the source-to-page fan-out auditable in
both directions — Lint walks these lists to detect under-ingestion.

Source summaries are append-once; later edits should be limited to
adding to the Generated entity pages and Generated concept pages
lists, and the Change Log, when subsequent Ingests touch the same
source.

---

## Entity page format

Every entity page (`01-canonical/entities/{slug}.md`) uses the shape
defined in `templates/entity-template.md`. The slug is lowercase,
hyphenated, and stable — once a slug exists, every later source that
mentions the entity uses the same slug. Slug stability matters
because cross-links across the Cortex resolve to slugs.

Frontmatter must include:

- `kind: entity` — always literal
- `entity_type` — one of `person | organization | team | legal-entity |
  product | system | project | regulator | jurisdiction`
- `first_seen` — date this entity first entered the Cortex (do not
  update on later edits)
- `sources` — list of pointer IDs the entity is anchored on; append on
  later Ingests, do not replace
- `aliases` — alternative names, abbreviations, predecessor names
- `confidentiality` — propagated from the strictest source touching
  the entity
- `status` — `active | inactive | archived`

Body sections (template uses English defaults; `CLAUDE.md` may
override the heading language for the case):

- **Identity** — short structured list of identity facts. Adjust by
  entity_type: people get role/title/team; organisations get legal
  form/seat/registration; products get version/owner; jurisdictions
  get regulator/scope.
- **Description** — rich prose describing the entity. Same richness
  expectation as concept pages.
- **Role in case** — what this entity *does* in this case. The
  section that distinguishes an entity page in this Cortex from a
  generic Wikipedia stub.
- **Relationships** — links to other entities and concepts.
- **Footprint** — optional. Trail this entity has left (meetings,
  filings, decisions, contributions). Useful for entities whose
  actions drive the timeline.
- **Open questions**, **Synthesis**, **Change Log** — same as concept
  pages.

Entity pages are mandatorily cross-linked. An entity acquires meaning
in the case by what mechanisms (concepts) it interacts with and which
other entities it deals with — zero outbound links is a lint nit.

---

## Concept page format

Every concept page (`01-canonical/concepts/{slug}.md`) uses the shape
defined in `templates/concept-template.md`. Frontmatter:

- `kind: concept` — always literal
- `first_seen` — date this concept first entered the Cortex
- `sources` — list of pointer IDs
- `aliases` — alternative names, abbreviations, competing terms
- `confidentiality` — propagated from the source

Body sections:

- **Definition** — 1–3 sentences, fact-grounded, source-citable
- **Description** — rich prose, 3–10 sentences for any non-trivial
  concept. **The point of the page.** An empty Description is a lint
  warning.
- **Related concepts and entities** — at least one outbound link
- **Open questions** — concept-specific gaps
- **Trade-offs** — expected for design-bearing concepts (mechanisms,
  calibrations, clauses, allocation rules); optional for purely
  descriptive concepts
- **Synthesis** — optional but encouraged; explicitly marked as
  interpretation, not fact
- **Change Log** — append-only

A concept page with zero outbound related-concept entries is a lint
nit — either the enumeration missed its neighbours or the concept is
mis-scoped.

---

## Pointer entries

`04-pointers/systems.yaml` and `external.yaml` use this shape:

```yaml
- id: {{SLUG_STYLE_ID}}
  system: {{SYSTEM_NAME}}
  kind: account | contact | deal | document | folder | issue | repo | thread | channel
  url: https://...
  description: {{ONE_LINE_DESCRIPTION}}
  last_verified: {{YYYY-MM-DD}}
```

Every pointer MUST have `id`, `url`, and `description`. The `id` is
used for inline citation via `[→ pointers/{{FILE}}.yaml#{{ID}}]`.

---

## CLAUDE.md (per-case operating manual)

`CLAUDE.md` lives at the case root and is generated from
`templates/claude-md-template.md`. It captures conventions specific
to *this* case: language, jurisdiction, tone, domain-specific page
conventions, workflow tweaks. The generic skill provides the
four-layer shape and the six workflows; `CLAUDE.md` is the per-case
overlay the LLM and the user co-evolve.

`CLAUDE.md` itself is written in **English** even when the rest of
the Cortex is in another language. Section 3 (Language convention)
declares the language of the case content.

Edit conventions:

- The Domain conventions, Workflow tweaks, Tone, and Open items
  sections co-evolve. The LLM should propose additions when it
  notices a recurring pattern across two or more Ingests; do not
  silently codify.
- When a previously codified convention turns out to be wrong, revise
  in place **and** record the prior version's removal in the Change
  Log section. Never silently rewrite a convention.
- Always append a Change Log entry for any update. Newest first.

`CLAUDE.md` is read once per session before answering any question.
Lint checks for its presence and Change Log; missing → blocker.

---

## What not to do

- **Don't invent facts about the world.** If the source didn't say
  it, don't assert it as fact. Use dated `TODO({{YYYY-MM-DD}}):`
  markers for factual gaps.
  *But:* this rule is about claims about the world, not about
  descriptive writing. Synthesis, pattern-naming, and rich
  description of facts you *did* get are encouraged when they live
  in `## Description` or `## Synthesis` sections of concept pages.
- **Don't suppress richness on entity or concept pages.** A page
  with a one-line definition and no description is the failure mode
  this skill exists to avoid. If the source is thin, write what you
  have and flag the gap as a TODO inside the Description — don't
  leave the section empty.
- **Don't rewrite history.** Layer 2 is append-only for substantive
  content. Supersede, don't edit.
- **Don't dump full documents into the Cortex.** The Cortex indexes;
  it does not host. Put the document in a system of record and add a
  pointer.
- **Don't mix layers.** A meeting note doesn't belong in Layer 1. A
  canonical fact doesn't belong in a log entry. A concept page
  doesn't belong in Layer 3.
- **Don't skip provenance.** Entity and concept pages list `sources`
  in frontmatter. Layer 3 artifacts list `inputs` in frontmatter. No
  exceptions.
- **Don't write long prose where a table would do — except on entity
  and concept page descriptions.** Skeleton files, logs, decisions,
  and pointers prefer structure. Description sections prefer prose.
- **Don't collapse a substantive source into one summary.** One
  source, many pages. See `ingestion.md`.
- **Don't bump synthesis date stamps when nothing materially
  changed.** Lint detects staleness via content hash, not mtime — a
  no-op date bump is noise.
