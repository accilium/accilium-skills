# Workflow 4 — Maintain

Goal: keep the Cortex alive as the case progresses. This is the
workflow that runs most often in practice.

---

## Source-isolation rule (read first)

The same rule that governs Seed and Ingest applies here: the
Cortex grows only from what the user gives the LLM in this
conversation. When the user dictates an update — "add a stakeholder
{name}", "we decided X", "scope now includes Y" — write *only*
what the user actually said. Don't enrich with details from memory,
general knowledge, or sibling skills.

If the user says "we added a new advisor, the firm is {Firm}", the
entity page is created with that one fact and a TODO for everything
else (jurisdiction, partner, fee arrangement, history). The LLM
might know more about {Firm} from general knowledge — that
knowledge does not become Cortex content. If the LLM has memory of
prior cases involving {Firm}, that memory does not become Cortex
content. The Cortex is anchored to *this conversation*.

When the user dictates a fact that contradicts something the LLM
"knows", trust the user. The user is the source of truth for their
case.

User-dictated updates still need provenance. For every Maintain update
that writes a fact into Layer 1, create or update a dated Layer 2 log
entry first, then cite that log entry in the affected page's `sources:`
frontmatter or inline citation. In this workflow, a log entry is a
valid source because it records a user assertion made in the current
conversation.

---

## Recognise what the user is adding

When the user says things like:

- *"Add to the cortex that we met with X today and decided Y"* →
  **decision + log entry**
- *"Record that the counterparty filed Z"* → **see "Ingest vs.
  Maintain" below**
- *"New stakeholder: {name}, {role}"* → **create or update an
  entity page** at `01-canonical/entities/{slug}.md`, plus a
  Layer 2 log entry.
- *"New mechanism / KPI / clause: {name}"* → **create or update a
  concept page** at `01-canonical/concepts/{slug}.md`.
- *"Scope changed — we're now also covering W"* → **Layer 1 scope
  update + log entry**.
- *"Open question: can we rely on {source}?"* → **Layer 2
  open-questions update**.
- *"Here's a document to add"* / *"read this and update the
  cortex"* → **Ingest** (Workflow 3).
- *"Henceforth do X like Y in this case"* / *"always treat Z
  as …"* / *"from now on, …"* → **`CLAUDE.md` update** (see
  "CLAUDE.md as a co-evolving document" below).

Read the relevant file(s) before editing. Never overwrite Layer 1
silently — Layer 1 is the canonical facts and deserves deliberate
edits.

If the Cortex is in minimal mode, use the minimal-mode path below
instead of trying to write full-mode files that do not exist.

---

## Ingest vs. Maintain — the boundary

The line between "user is bringing external content in" (Ingest)
and "user is dictating from their head" (Maintain) is occasionally
blurry. Some heuristics:

- **Pure dictation** ("we decided to use Approach A; rationale is
  cost") → Maintain. No source to ingest; the user is the source.
- **External document** ("read this PDF and update the cortex")
  → Ingest, every time.
- **Meeting recap with attached transcript** → Ingest the
  transcript. The recap and any decisions taken in the meeting
  are still Maintain entries (decisions, log) but the substance
  goes through Ingest.
- **Meeting recap, no transcript, just user paraphrasing** →
  Maintain. Treat the user's paraphrase as authoritative dictation
  for the log entry.
- **"X just emailed me that Y"** → if the user paraphrases without
  the email, Maintain. If they forward the email, Ingest the email.
- **"The counterparty filed Z"** with the filing attached →
  Ingest the filing. Without the filing → Maintain (treat as a
  user-asserted fact, log it; flag a TODO to ingest the filing
  when available).

When genuinely ambiguous, ask:

> Are you giving me content to read and turn into pages, or are
> you dictating an update to write directly?

---

## Writing conventions

### Minimal-mode path

Minimal-mode Cortexes have only `CLAUDE.md`, `cortex.yaml`,
`README.md`, and `notes.md`. For ordinary updates:

- Read `notes.md` before editing.
- Append dated entries under `## Notes log`, newest first.
- Add decisions under `## Decisions`, preserving append-only
  semantics. Supersede decisions rather than rewriting their substance.
- Add questions under `## Open questions`; when resolved, keep the
  original question and move or mark it with `[resolved YYYY-MM-DD:
  {{ANSWER}}]`.
- Add source or system links under `## Pointers` with a short
  description.
- For a small pasted brief, summarize it into a dated Notes log entry
  and list any questions/decisions it creates. For a substantial
  external source, offer migration to full mode before Ingest.

After each minimal-mode update, check migration triggers: `notes.md`
over roughly 500 lines, a second substantial source, repeated
cross-references, or a user question that requires structured entity /
concept lookup.

### Full-mode path

- **Layer 1 skeleton edits** — update in place. Add a one-line
  entry to the `## Change Log` section at the bottom of the file
  with date + one-line summary. If the file has no change log
  section, add one.
- **Layer 1 concept edits** — update in place. Append to the
  concept's own `## Change Log` section. If the update is a
  material fact change, also add a reference to the triggering log
  entry or ingest.
- **Layer 1 entity edits** — same as concept edits. Update in
  place, append to the entity's `## Change Log`. When the entity
  participates in a new case event, append a row under
  `## Footprint` (or the localised equivalent declared in
  `CLAUDE.md`) linking to the log entry. Do not silently rename a
  slug — entity slugs are stable; if an entity is renamed, keep
  the old slug as an alias and add a new Change Log entry.
- **Layer 2 decisions** — *append* to `decisions.md` for any
  substantive change (new decision, reversal, supersession).
  Benign edits (typos, formatting fixes, frontmatter corrections)
  are permitted in place. Anything that alters meaning, decision
  content, or rationale must be a new superseding entry.
- **Layer 2 open questions** — edit in place. Mark resolved
  questions with `[resolved YYYY-MM-DD: {answer}]` rather than
  deleting them.
- **Layer 2 log entries** — create a new file at
  `02-working-memory/log/{YYYY-MM-DD}-{short-slug}.md`. Keep it
  short: what happened, who was involved, decisions taken, next
  steps. Link to any documents that were produced or discussed
  via relative paths or Layer 4 pointers.
- **user-assertion provenance** — when a log entry is the source for
  a Layer 1 fact, cite it as
  `02-working-memory/log/{YYYY-MM-DD}-{short-slug}.md` in the page's
  `sources:` frontmatter or next to the specific claim.
- **Layer 4 pointers** — edit the relevant YAML file. Always
  include a `description` field so the pointer is self-explanatory.

---

## CLAUDE.md as a co-evolving document

`CLAUDE.md` at the case root is the per-case operating manual.
Unlike the generic skill (which is shared across all Cortexes),
`CLAUDE.md` captures the conventions specific to *this* case:
language, jurisdiction, tone, domain-specific page conventions,
workflow tweaks. It is read into the LLM's context on every session
that touches this Cortex.

Treat it as a living document the LLM and the user co-evolve, in
the spirit of the LLM-native wiki pattern: *you and the LLM
co-evolve this over time as you figure out what works for your
domain.*

When to update `CLAUDE.md`:

- The user explicitly states a convention ("from now on, treat all
  dates in source quotes verbatim", "always include a tax section
  on concept pages") → update sections 4 (Domain conventions), 5
  (Workflow tweaks), 6 (Jurisdictional defaults), or 7 (Tone) as
  appropriate.
- The LLM notices a recurring pattern across two or more Ingests
  or edits ("we keep producing entity pages for advisors with a
  fee-arrangement section — should that be a convention?") →
  propose the addition to the user *before* writing it. Do not
  silently codify conventions.
- A previously codified convention turns out to be wrong → revise
  it in place, **and** record the prior version's removal in the
  Change Log section. Never silently rewrite a convention; the
  Change Log is the audit trail for how the manual evolved.
- An item in the Open items section is resolved → move the
  resolution to the relevant section (Domain conventions, Workflow
  tweaks, Jurisdictional defaults, or Tone) and strike the open item.

When *not* to update `CLAUDE.md`:

- Case facts go in Layer 1 pages. `CLAUDE.md` describes how the
  Cortex is structured, not what is in it.
- Decisions about case content go in
  `02-working-memory/decisions.md`. `CLAUDE.md` is for decisions
  about the Cortex *as an artefact*.

Always append a Change Log entry in the `CLAUDE.md` Change Log section
for any update. Newest first.

---

## Staleness checks

Whenever Layer 1 changes materially (scope, core entities, mandate,
or any concept page), immediately re-hash the changed file(s) and
scan Layer 3 for any derived artifact whose `inputs:` list includes
any of them. For each artifact whose stored hash no longer matches
the current content hash, add a line at the top:

```markdown
> ⚠️ **Stale**: one or more inputs to this artifact changed on
> {YYYY-MM-DD}. Consider regenerating. Changed inputs: {list}.
```

Do not silently regenerate. Tell the user what is stale and ask if
they want to regenerate now. Prefer `material-v1` hashes when a helper
is available; if the artifact uses `raw` hashes, label the finding as
conservative raw-hash staleness because Change Log or whitespace edits
can change raw hashes without changing substance.

---

## Conventions for consistent writing

Read `references/writing-conventions.md` the first time you work on
a Cortex in a session to align on dates, headings, citation format,
log shape, and Layer 1 / Layer 3 frontmatter.
