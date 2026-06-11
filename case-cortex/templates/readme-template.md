# {{CASE_NAME}} — Case Cortex

{{ONE_LINE_PURPOSE}}

---

## What this is

This directory is a **Case Cortex**: a structured, living
representation of a single bounded problem. It is the shared
reasoning substrate for humans and AI agents working on this case
over time.

It is inspired by the LLM-native wiki pattern, generalized from
documentation to any bounded knowledge-work problem worth sustained
reasoning about.

This Cortex is in **{{minimal | full}}** mode. See `CLAUDE.md`
section 2 for what that implies.

## How it's organized (full mode)

- **`01-canonical/`** — ground truth of the case. Low-volatility
  facts. Spine files (overview, synthesis, index), skeleton files
  (identity, scope, context), entity pages, concept pages, source
  summaries. Review-gated edits.
- **`02-working-memory/`** — the live log. Decisions, open
  questions, dated entries. Append-only by convention for
  substantive content; benign edits permitted in place.
- **`03-derived/`** — artifacts generated from layers 1 and 2.
  Briefings, analyses, reports, lint reports. Regenerable.
  Superseded artifacts live in `_archive/`.
- **`04-pointers/`** — links to systems of record (CRM, DMS,
  trackers) and external sources.

## How it's organized (minimal mode)

- **`notes.md`** — single growing notes file. Drop notes whenever.
  The skill watches for migration triggers and will offer to
  upgrade to the full structure when the case has earned it.
- **`CLAUDE.md`** — the per-case operating manual.
- **`cortex.yaml`** — case metadata.

Every file is plain markdown or YAML. Edit in any text editor.
Agents read and write via the same interface.

## How to use it

- **Ask a question about the case:** the skill reads from Layer 1
  first (or `notes.md` in minimal mode), then Layer 2.
- **Record something new:** a decision goes in `decisions.md`; a
  meeting or event goes in `log/{{YYYY-MM-DD}}-{{SLUG}}.md`; a new
  fact about a named entity goes in
  `entities/{{SLUG}}.md`. (In minimal mode, all of these go to
  `notes.md`.)
- **Generate a briefing or analysis:** the skill reads the Cortex
  and writes to `03-derived/` with provenance frontmatter
  (content hashes of inputs).
- **Update a canonical fact:** edit the relevant file in
  `01-canonical/` and add a line to its Change Log.

## Conventions

- Dates are ISO: `YYYY-MM-DD`.
- Layer 2 is append-only for substantive content. Supersede,
  don't rewrite.
- Every derived artifact declares its inputs in frontmatter, with
  content hashes for staleness detection.
- Facts cite pointers; guesses are marked `TODO:`.
- See `CLAUDE.md` for per-case overrides on the above.

## Getting help

Invoke the `case-cortex` skill with phrases like "update the
cortex", "generate a briefing from the cortex", or "what does the
cortex say about X".

---

*Created: {{YYYY-MM-DD}} · Owner: {{OWNER_NAME}}*
