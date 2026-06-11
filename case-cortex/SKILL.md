---
name: case-cortex
version: 1.0.0
description: >
  Build and maintain a Case Cortex — a structured, living, machine-readable
  representation of a single bounded knowledge-work problem (a "case") that
  agents and humans share as their reasoning substrate. Use whenever the
  user wants to set up, seed, update, query, or regenerate artifacts from a
  Case Cortex. Triggers on phrases like "build a cortex for X", "start a new
  case", "initialize a case", "seed my cortex", "update the cortex", "add to
  the cortex", "ingest this document into the cortex", "what does the cortex
  say about Y", "regenerate the briefing", or "lint the cortex". A Cortex
  fits bounded analytical or advisory work (a deal, a matter, an
  investigation, a research question, a transformation programme); do NOT
  use for casual long-running tasks (workout logs, study schedules,
  shopping lists), one-shot research where no persistent artifact is
  wanted, or general-purpose wikis spanning multiple problems.
---

# Case Cortex — build and maintain

A Case Cortex is a structured, living representation of a single bounded
problem — a *case*. It lives as a directory of markdown + YAML files and is
designed to be the shared observation substrate for agents and humans
working on that problem over time.

The skill is modelled on the LLM-native wiki pattern (Ingest → Query →
Lint), generalised from documentation to any bounded problem. The core
move — **one source touches many pages; richness accumulates as concepts
branch out** — is baked into the workflows. If a Cortex starts looking
like a sparse skeleton with all the richness hidden in a single
briefing, the skill is being used wrong.

This SKILL.md is the routing and orientation document. Each workflow
lives in its own reference file, loaded only when needed. Read
`references/architecture.md` once per session to load the four-layer
model. Read the relevant workflow file when routing decides which
workflow applies.

## Skill version and compatibility

This skill is versioned independently from the Cortex schema. New
Cortexes created by this version should record both
`cortex_schema: 1` and `skill_version: 1.0` in `cortex.yaml`.
When future skill versions change template shapes or frontmatter
contracts, migration notes should be added under **Skill Changelog**
at the end of this file.

The per-case operating manual is named `CLAUDE.md` for compatibility
with the original LLM-native wiki pattern. In Codex or other agent
runtimes, treat `CLAUDE.md` as the canonical case manual unless the
case explicitly mirrors it to another runtime-specific file such as
`AGENTS.md` or `CODEX.md`.

---

## Read this first — source isolation

> **A Cortex contains only what the user explicitly provided in this
> conversation.** Memory, other skills loaded in the same session,
> stored facts about the user, and general world knowledge are
> *context for the LLM* — they are not *content for the Cortex*.
>
> When seeding, ingesting, or maintaining a Cortex, the question is
> not *what do I know about this case*, it is *what has the user
> handed me in this conversation*. Memory might tell the LLM that
> the user works at a specific firm, uses specific tools, and has
> specific clients — none of that goes into the Cortex unless the
> user mentions it as part of the case.
>
> If you find yourself about to write a name, an acronym, a tool, a
> client, a KPI, or any other specific detail, ask: *did the user
> just give me this, or am I pulling it from somewhere else?* If
> the latter — drop it. See Principle 1 in the Principles section
> for the full rule.

---

## Routing — figure out what the user wants

Match the user's request to one of the workflows below, then load the
corresponding reference file and follow it.

| Signal | Workflow | Reference to load |
|---|---|---|
| "build / start / initialize / set up a cortex for X", no path exists yet | Initialize | `references/workflows/1-initialize.md` |
| User has just initialized a full-mode Cortex, or says "seed / populate / fill in the cortex" | Seed | `references/workflows/2-seed.md` |
| User wants a document / source / meeting / workbook read into the cortex | Ingest | `references/workflows/3-ingest.md` (and `references/ingestion.md` for the methodology) |
| Cortex exists + user adds notes, decisions, facts, meetings | Maintain | `references/workflows/4-maintain.md` |
| Cortex exists + user asks a question / wants a briefing / wants an artifact | Use | `references/workflows/5-use.md` |
| "lint / audit / health-check / clean up / is anything stale / check consistency" | Lint | `references/workflows/6-lint.md` |

**Ingest vs. Maintain:** if the user is *bringing external content in*,
route to Ingest. If they are *dictating an update from their head*, route
to Maintain. When in doubt, ask.

**Minimal-mode Cortexes:** if the Cortex is in minimal mode, route
ordinary updates, first notes, decisions, and small pasted briefs to
Workflow 4's minimal-mode path. If the user wants to ingest a
substantial external source or asks questions the flat `notes.md`
cannot answer cleanly, offer migration to full mode first.

If still ambiguous, ask the user which of the workflows they want. Do
not guess.

---

## Where the Cortex lives — handle this before Initialize

A Cortex is a directory of files. Where the directory actually lives
depends on the runtime, and the skill must surface this explicitly
before scaffolding anything.

**If running in Codex, Claude Code, or a similar local-filesystem environment**
— the user has a real, persistent file system. Ask the user for an
absolute path to a parent directory and create `{case-name}/` there
(see Workflow 1, Step 1.1). This is the canonical mode.

**If running in a sandboxed code-execution environment** (e.g. the
claude.ai code execution feature) — the working filesystem does not
persist across conversations. Be explicit with the user about this:
the Cortex can be built in `/mnt/user-data/outputs/cases/{case-name}/`
within a single conversation and downloaded as a zip, but to maintain
it across sessions the user must either (a) re-upload the zip at the
start of each session, or (b) host the Cortex in a synced location
(GitHub repo, cloud drive) and connect to it via available tools.

**If running in a chat-only environment with no filesystem at all** —
the skill cannot create files. Tell the user this directly and offer
the alternative: paste the scaffolding into the chat and have them save
it to disk themselves, or upgrade to a runtime with file access.

Do not begin scaffolding until the persistence question is settled. A
Cortex that vanishes at the end of the session is worse than no Cortex
— the user will rebuild it from scratch next time and lose trust in the
pattern.

---

## Two starting modes — minimal and full

The skill supports two ways to begin, chosen explicitly with the user:

**Minimal mode** — for users who want low commitment. Creates only
`CLAUDE.md`, `cortex.yaml`, `README.md`, and a single `notes.md` at the
case root. No layer directories. No spine files. Use this when the user
is exploring whether the Cortex pattern fits their work, or when the
case is too early to have meaningful structure. The skill watches for
signals that the case has outgrown minimal mode (notes file > ~500
lines, the user starts asking questions the structure can't answer,
multiple sources need ingesting) and offers to migrate to full mode.

**Full mode** — the four-layer architecture described in
`references/architecture.md`. Use this when the user knows they want
sustained reasoning over the case, when there are already multiple
sources to ingest, or when they have explicitly asked for the full
structure.

When in doubt, default to minimal and offer to upgrade. The friction of
upgrading later is much lower than the friction of an over-built scaffold
on day one.

The migration path is mechanical and described in
`references/workflows/1-initialize.md` under "Migrating minimal → full".

---

## The four-layer model in one paragraph

Every full-mode Cortex has four layers that differ in volatility,
ownership, and regenerability:

- **Layer 1 — Canonical** (`01-canonical/`): the ground truth. Spine files
  (overview, synthesis, index), skeleton files (identity, scope, context),
  entity pages (named real-world things that *act*), concept pages
  (mechanisms that *describe how something works*), source summaries.
- **Layer 2 — Working memory** (`02-working-memory/`): the live log.
  Decisions, open questions, dated entries. Append-only by convention.
- **Layer 3 — Derived** (`03-derived/`): regenerable artifacts. Briefings,
  analyses, lint reports. Each carries provenance frontmatter.
- **Layer 4 — Pointers** (`04-pointers/`): links to systems of record and
  external sources. The Cortex indexes, it does not re-host.

For full detail load `references/architecture.md`.

---

## Entity vs. concept — the routing primitive

A substantive source teaches both *things that act* (people, organisations,
products, regulators) and *things that describe how something works*
(mechanisms, KPIs, terms of art, clauses). These need different shapes,
so they live in separate directories.

**Decision tree** (apply in order, stop at first match):

1. **Is it a person, named team, named organisation, legal entity, or
   regulator with identity?** → entity. (Identity = it has a phone
   number, employee ID, registration number, or office.)
2. **Is it a named, scoped artefact that exists as a discrete object** —
   a specific contract, a specific tender, a specific software product,
   a specific dataset, a specific piece of legislation by number?
   → entity, with `entity_type: product` or `system`.
3. **Does it act in the world under a name once issued or instantiated?**
   (a specific court order, a specific regulatory decision, a specific
   policy programme with a leader and a charter) → entity.
4. **Is it a mechanism, formula, allocation rule, KPI definition,
   workflow, regime, doctrine, or generic clause type?** → concept.
5. **Is it the abstract regime an entity issues** (e.g. a privacy
   regulation, a reporting standard) while the issuer is itself an
   entity? → concept for the regime; cross-link to the entity that
   issues it.
6. **Is it a relationship pattern?** → concept only if load-bearing
   (e.g. "the parent-subsidiary dividend path"); otherwise leave it as
   a cross-link between two entity pages.

Phone-call test as a tiebreaker only: *can this thing make a phone
call?* Yes → entity. Used to act in the world with a name → entity.
Just describes how something works → concept.

Worked edge cases:

- A specific regulation by number (e.g. an order, a directive) →
  **entity** (it acts once issued).
- The regulation's *type* (the regime — directive class, standard
  framework) → **concept**.
- A specific tender or RFP → **entity** (`entity_type: product`).
- The tender's evaluation rubric → **concept**.
- A specific contract clause within a contract → **concept** (it's a
  mechanism); the contract itself → **entity**.

When still uncertain, ask the user — and prefer to err toward entity.
Mis-routed pages are cheap to fix later; lint catches them.

---

## Examples and detailed methodology

- `references/examples.md` — worked examples for each workflow.
- `references/ingestion.md` — the fan-out methodology (load before any
  Ingest in a session). This is the single most important reference for
  avoiding the thin-cortex failure mode.
- `references/writing-conventions.md` — formatting, dates, citation
  style, page conventions.

---

## Principles to preserve across every workflow

1. **Source isolation — the Cortex contains only what the user
   explicitly provided.** This is the most important principle. The
   only legitimate inputs to a Cortex are: (a) what the user has
   typed in this conversation, (b) files the user has uploaded or
   pointed at by path/URL in this conversation, (c) content the user
   has explicitly asked to be ingested from a connected tool. Nothing
   else qualifies. Specifically excluded:
   - **Stored memories about the user.** Anything from
     `userMemories`, prior-conversation history, or memory summaries
     is *context for the LLM*, not *content for the Cortex*. Do not
     bring in client names, project names, KPIs, terminology,
     stakeholder names, or any other case-specific detail from
     memory unless the user mentions it in the current conversation.
   - **Other skills' content.** Any skill loaded into the same
     session (showcases, demos, sibling skills, internal reference
     material) is invisible to the Cortex. Do not borrow names,
     terminology, examples, or worked cases from them.
   - **Pre-existing knowledge about real-world entities.** General
     world knowledge can be used to *understand* what the user
     provides (e.g. recognising what a CSRD is) but does not become
     a fact in the Cortex unless the user's source asserts it.
   - **Inferred or guessed content.** If the user provided a partial
     brief, fill what they gave; mark gaps as `TODO:`. Do not
     fill gaps with plausible-sounding details from training data
     or memory.

   Concretely: when scaffolding a new Cortex from a one-line user
   prompt ("build a cortex for my acquisition target evaluation"),
   the Cortex contains only the user's words plus generic structural
   placeholders. It does not name a target, a sector, or a
   counterparty unless the user did. If the user later ingests a
   teaser document, the Cortex grows from what's in that document —
   not from what the LLM happens to know about that company from
   elsewhere.

   When tempted to write something not directly traceable to a
   user-provided input, stop and ask: *did the user actually give me
   this in this conversation?* If no — don't write it.
2. **Structure over prose — except on entity and concept page
   descriptions.** Skeleton files, spine, logs, and pointers prefer
   lists and tables. Entity and concept page bodies are where richness
   lives — they are expected to be rich descriptive prose. Flattening
   those is a failure mode.
3. **Layer 1 is canonical, Layer 2 is append-only, Layer 3 is
   regenerable, Layer 4 is machine-maintained.** If you are about to
   violate one of these, stop and reconsider.
4. **Never invent facts about the world — but synthesise freely within
   marked sections.** A claim about the world the source did not
   support is a `TODO:`, not a fact. But describing, connecting,
   patterning, and interpreting the facts you *did* get is fair game
   when it lives in a `## Description` or `## Synthesis` section.
   This principle and #1 together: synthesis is allowed only over
   user-provided content, not over content the LLM brought in from
   elsewhere.
5. **One source, many pages.** A substantive source fans out into 10+
   entity *and* concept pages combined. If you find yourself writing
   one long summary instead of many interlinked pages, you are
   violating this principle.
6. **Provenance on everything.** Every entity and concept page cites
   the source(s) it came from. Valid provenance is either a Layer 4
   pointer to a user-provided source or a dated Layer 2 log entry that
   records a user assertion made in this conversation. Every Layer 3
   artifact lists its inputs. No exceptions. If you cannot name a
   user-provided source or user-assertion log entry for a claim, the
   claim does not belong in the Cortex (see #1).
7. **Date everything in ISO format.** `YYYY-MM-DD`, no ambiguity.
8. **Don't replace existing systems.** The Cortex indexes CRMs and
   document stores via Layer 4 pointers — it does not re-host them.
9. **Small, frequent writes beat large, rare ones.** Encourage the user
   to log decisions the same day, not in monthly batches.
10. **Defer to `CLAUDE.md` for per-case overrides.** If the per-case
    operating manual contradicts a generic convention, the per-case
    convention wins (the LLM and user co-evolve it). The generic skill
    provides the shape; `CLAUDE.md` provides the per-case overlay.

---

## Reference files

- `references/architecture.md` — the four-layer model. Load once per session.
- `references/ingestion.md` — fan-out methodology. Load before the first
  Ingest. **Most important reference for avoiding the thin-cortex
  failure mode.**
- `references/writing-conventions.md` — formatting, dates, citation style,
  page conventions.
- `references/examples.md` — worked examples.
- `references/workflows/1-initialize.md` — Initialize workflow detail.
- `references/workflows/2-seed.md` — Seed workflow detail.
- `references/workflows/3-ingest.md` — Ingest workflow operating procedure.
- `references/workflows/4-maintain.md` — Maintain workflow detail.
- `references/workflows/5-use.md` — Use workflow detail (queries and
  derived artifacts).
- `references/workflows/6-lint.md` — Lint workflow detail.

## Templates

- `templates/cortex-yaml-template.yaml` — case-level metadata.
- `templates/claude-md-template.md` — per-case operating manual.
- `templates/readme-template.md` — per-case README.
- `templates/notes-template.md` — minimal-mode single notes file.
- `templates/working-memory-skeleton.md` — initial decisions and open-questions.
- `templates/pointers-template.yaml` — deprecated compatibility note;
  use the split pointer templates below for new Cortexes.
- `templates/systems-template.yaml` — starter Layer 4 system pointers.
- `templates/external-template.yaml` — starter Layer 4 external pointers.
- `templates/concept-template.md` — per-concept page shape.
- `templates/entity-template.md` — per-entity page shape.
- `templates/overview-template.md` — Layer 1 spine: narrative entry point.
- `templates/synthesis-template.md` — Layer 1 spine: opinion-bearing thinking.
- `templates/index-template.md` — Layer 1 spine: curated catalog.
- `templates/source-summary-template.md` — per-source reading notes.
- `templates/derived-artifact-header.md` — Layer 3 provenance frontmatter.
- `templates/domains/{flavor}.md` — Layer 1 skeleton scaffolding per domain:
  `consulting`, `legal`, `research`, `engineering`, `investigation`, `general`.

---

## Placeholder convention

Templates use double braces for values to substitute. Two forms are
permitted:

- **Atomic tokens** in `{{UPPER_SNAKE_CASE}}` — for single values the
  scaffolder fills in: `{{CASE_SLUG}}`, `{{YYYY-MM-DD}}`,
  `{{POINTER_ID}}`. This is the default and preferred form.
- **Lowercase descriptive prose** like `{{alternative names or
  abbreviations}}` — only inside guidance text or example bodies where
  the placeholder describes the *kind* of content the author should
  write rather than a single drop-in value.

Single-brace examples are avoided in templates so scaffolding is
visually unambiguous. References may still use single braces in prose
when describing abstract syntax (e.g.
`[→ pointers/{file}.yaml#{anchor}]`), but generated files should use
resolved values, not literal placeholders.

---

## Skill Changelog

- 1.0 — Initial versioned Case Cortex skill with four-layer model,
  minimal/full modes, provenance rules, derived artifact staleness
  checks, and lint workflow.
  - **Breaking change for pre-1.0 Cortexes:** source-summary
    frontmatter renamed `source_path:` → `sources:` (now a list, to
    match entity/concept frontmatter and to allow multiple back-pointers).
    Migration: in each `01-canonical/sources/*.md`, replace the single
    `source_path: 04-pointers/{file}.yaml#{id}` line with a `sources:`
    list whose first item is that same pointer reference. Lint accepts
    legacy `source_path:` as a **warning** ("legacy source_path key —
    migrate to sources list") for one skill version; it becomes a
    blocker in the next major bump.
  - Pointer template split: `pointers-template.yaml` is deprecated in
    favor of `systems-template.yaml` and `external-template.yaml`. The
    deprecated file is retained as a landing note; existing Cortexes
    are unaffected.
