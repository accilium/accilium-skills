# Workflow 2 — Seed

Goal: move a freshly initialized Cortex from empty scaffold to useful
baseline. Three modes — wizard, one-shot brief, ingest a source.

This workflow only applies to **full-mode** Cortexes. Minimal-mode
Cortexes don't need seeding; the user just starts dropping notes.

---

## Source-isolation rule (read first)

Seeding is the highest-risk moment for contamination. The Cortex
is empty, the LLM has lots of context (memory, other skills, prior
conversation history), and the temptation to "fill in plausible
detail" is strongest. Resist it.

The only legitimate inputs to seeding are:

1. The user's answers to wizard questions (Mode A).
2. A brief or document the user pastes or attaches in this
   conversation (Modes B and C).
3. Files the user has explicitly pointed at by path or URL.

Everything else — including the user's stored profile, prior cases
they've worked on, tools you know they use, terminology from
sibling skills loaded in the same session, generic world knowledge
about real-world entities — stays out of the Cortex.

If the user says "build a cortex for evaluating an acquisition
target" without naming the target, the seeded Cortex names no
target. It scaffolds with `{TARGET}` placeholders the user will
fill later. It does not pick a plausible-sounding target from
context.

If memory tells you the user works at "Firm X" and has clients "A,
B, C", but the user has not mentioned Firm X or any of those
clients in this conversation — none of those names appear in the
Cortex.

When in doubt, ask the user. A wizard question costs nothing; a
contaminated Cortex costs trust.

---

## Ask the user which mode they want

If not already clear:

> Three ways to seed:
>
> 1. **Wizard** — I ask targeted questions, layer by layer, you
>    answer, I write. Best when you know the case in your head but
>    don't have it written down anywhere.
> 2. **One-shot brief** — you paste or describe the situation in
>    your own words (a memo, an intake note, a meeting transcript
>    — anything), I parse it and populate the Cortex. This invokes
>    Ingest (Workflow 3) on your brief.
> 3. **Ingest a source** — you point me at a document, workbook,
>    or resource. I run full Ingest (Workflow 3) on it. Best when
>    there is already an authoritative source you want digested.
>
> Which do you prefer?

---

## Mode A: Wizard

Walk through Layer 1 skeleton files in this order, asking 2–5
questions per file. Do not ask everything in one mega-prompt — go
file by file so the user can think.

1. **`identity.md`** — case name (confirm), type, one-paragraph
   purpose, start date, current status, success criteria.
2. **Entities** — who/what is involved? People (with roles),
   organisations, systems, assets. For each named entity the user
   mentions, create a file under
   `01-canonical/entities/{slug}.md` using
   `templates/entity-template.md`. Even a thin first pass is fine
   — fill identity facts, role-in-case, and leave the description
   and footprint to grow during Ingest. Do not collect entities
   into a single skeleton file; the directory layout is the
   structure. Don't require exhaustiveness on the first pass.
3. **`scope.md`** — in-scope, out-of-scope, constraints,
   assumptions.
4. **`context.md`** — background the case sits in: regulatory,
   sector, historical, competitive, whatever is relevant.

For each file, use the domain template as the shape of the content.
Write filled-in markdown with clear headings. Never invent facts
about the world — if the user doesn't answer something, leave a
`TODO:` marker with a specific question. (You may still synthesise
and describe freely — see Principle #3 in SKILL.md.)

After Layer 1, ask whether they want to add anything to Layer 4
(pointers) now — links to CRM records, document stores, external
sources. If yes, populate `04-pointers/systems.yaml` and
`external.yaml`. If no, skip.

After Layer 4, write a first pass of the **spine files** from what
the wizard just elicited:

- `overview.md` — three or four sentences synthesising the case
  context, what's at stake, the shape of the problem, and what the
  user wants out of the Cortex. Plus a short "where to start
  reading" pointer list to the Layer 1 skeleton files just
  populated.
- `synthesis.md` — explicitly state "no synthesis yet — Cortex was
  just seeded, no sources ingested". List the open questions from
  Layer 1 as the initial parked items. Synthesis grows during
  Ingest and Use.
- `index.md` — generate the catalog: list every file just created
  under Layer 1, grouped by topical sections (Identity, Entities,
  Scope, Context). Concepts and sources sections are empty
  placeholders waiting for Ingest output.

Wizard mode produces **entity pages** in `01-canonical/entities/`
for the named real-world things the user named, but does **not**
produce concept pages in `01-canonical/concepts/`, nor source
summaries in `01-canonical/sources/`. Concepts and source
summaries come from Ingest. If the user wants concept pages, ask
them to point you at a source and route to Workflow 3.

Do not populate Layer 2 (working memory) from the wizard unless
the user explicitly has events to log. Layer 2 is for live-case
entries, not retrospective scaffolding.

Do not touch Layer 3 (derived) during seeding.

---

## Mode B: One-shot brief

The user pastes or describes the situation. This is **Ingest on a
brief**: route to Workflow 3 with the brief as the source. The
Ingest workflow covers parsing, page fan-out, and Layer 1 skeleton
updates.

---

## Mode C: Ingest a source

The user points at a document, workbook, URL, or resource. Route
directly to Workflow 3.

---

## In all modes — finish with the welcome entry

Append a single entry to `02-working-memory/log/` called
`{YYYY-MM-DD}-cortex-initialized.md` with a short note on what was
seeded, which mode was used, which sources (if any) were ingested,
and what gaps remain. This is the first entry in the case's working
memory and establishes the convention that everything material gets
logged.
