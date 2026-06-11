# CLAUDE.md — {{CASE_NAME}} operating manual

This file is the schema and operating manual for **this** Cortex. It is
loaded into the LLM's context on every session that touches this
case. Read it first; keep it current as conventions evolve.

The generic skill (`case-cortex`) provides the overall four-layer shape
and the six workflows. This file is the per-case overlay: domain
conventions, language, terminology to preserve, jurisdiction defaults,
tone bias, and any case-specific tweaks to the generic workflows.

The pattern is co-evolutionary: *you and the LLM co-evolve this over
time as you figure out what works for your domain.* When the LLM
notices a recurring convention, it should propose an addition here.
When a convention here turns out to be wrong, it should be revised in
place (with the prior version captured in the Change Log).

---

## 1. Purpose of this Cortex

{{One short paragraph. What this case is, what it produces, who reads
it. A reader who has never seen the Cortex should be able to decide,
from this section alone, whether they're in the right place.}}

---

## 2. Pointer to the generic schema

This Cortex follows the **case-cortex skill** four-layer model
({{minimal | full}} mode):

For full mode:

- **Layer 1 — Canonical** (`01-canonical/`) — overview, synthesis,
  index, skeleton, concepts, entities, sources
- **Layer 2 — Working memory** (`02-working-memory/`) — decisions,
  open-questions, log
- **Layer 3 — Derived** (`03-derived/`) — briefings, analyses,
  comparisons, lint reports; superseded artifacts move to `_archive/`
- **Layer 4 — Pointers** (`04-pointers/`) — systems.yaml, external.yaml

For minimal mode:

- A single `notes.md` plus this file, `cortex.yaml`, and `README.md`.
  The skill will offer to migrate to full mode when this Cortex
  outgrows the flat structure (notes file long, multiple sources to
  ingest, queries that need structure to answer).

For the full architecture and workflows see the skill's
`references/architecture.md` and `references/ingestion.md`. Do not
duplicate that material here — point to it.

---

## 3. Language convention

{{Pick one. Examples:

- This Cortex is written in English. Section headings, frontmatter
  keys, and template fields are all English. (This is the skill
  default — leave the rest of this section short if so.)
- This Cortex is written in {{LANGUAGE}}. YAML keys stay English; YAML
  values and all page bodies are in {{LANGUAGE}}. Section headings
  on pages should be translated to {{LANGUAGE}} (e.g. translate
  "Description", "Role in case", "Relationships", "Footprint",
  "Open questions", "Synthesis", "Change Log" to their {{LANGUAGE}}
  equivalents and apply consistently).
- Mixed: skeleton/index/synthesis in English; entity identity facts
  and source quotes in original language.}}

### Heading map

If this Cortex is not written in English, maintain a heading map here.
The left side is the canonical English section name used by the skill;
the right side is the case-language heading to use in files.

| Canonical heading | Case heading |
|---|---|
| Description | {{TRANSLATED_DESCRIPTION}} |
| Role in case | {{TRANSLATED_ROLE_IN_CASE}} |
| Relationships | {{TRANSLATED_RELATIONSHIPS}} |
| Footprint | {{TRANSLATED_FOOTPRINT}} |
| Open questions | {{TRANSLATED_OPEN_QUESTIONS}} |
| Synthesis | {{TRANSLATED_SYNTHESIS}} |
| Change Log | {{TRANSLATED_CHANGE_LOG}} |

---

## 4. Domain-specific page conventions

{{Anything the generic skill doesn't say, that this case needs.
Examples (illustrative — replace with your own):

- Concept pages here include a `## Tax treatment` section because
  jurisdiction-specific tax handling is in scope for every mechanism.
- Entity pages for advisors include a `## Fee arrangement` section.
- Source summaries that ingest contracts include a `## Clause overview`
  section listing every numbered clause.
- Date convention: ISO `YYYY-MM-DD`, but where the source uses a local
  format, preserve it in quoted material.

Leave empty for the first session; fill in as conventions emerge.}}

---

## 5. Domain-specific workflow tweaks

{{Per-workflow overrides on top of the generic skill. Examples
(illustrative):

- **Ingest** — every contract redline ingested also produces a Layer 3
  diff briefing summarising the substantive changes from the prior
  version.
- **Maintain** — scope changes must cite the steering committee
  decision and link to the corresponding `decisions.md` entry.
- **Use (5b)** — derived briefings here include a `## Open legal risk`
  section called out at the top.
- **Lint** — also flag any identity facts in entity pages that lack a
  source citation.

Leave empty for the first session.}}

---

## 6. Jurisdictional and regulatory defaults

{{If the case has a default legal/regulatory frame, name it here so
the LLM doesn't ask every time. Examples (illustrative):

- Default jurisdiction: {{country}}. Treat all unmodified legal terms
  as {{country}}-law unless explicitly tagged otherwise.
- Default tax frame: {{country}} corporate tax. Cross-border treatment
  is in scope only for items explicitly flagged as such.
- Default GAAP: {{IFRS | local GAAP}} for the consolidated view;
  {{local GAAP}} for individual entities.

Leave empty if no defaults apply.}}

---

## 7. Tone and bias

{{How the LLM should write inside this Cortex. Examples (illustrative):

- Decision-bearing: the user is the decision-maker; the LLM
  structures, synthesises, challenges, bookkeeps.
- Concrete over abstract: prefer numbers, percentages, specific
  language over vague abstractions.
- Hedge sparingly but flag real uncertainty. Don't manufacture
  confidence the source doesn't support.
- When comparing peer firms, label estimates vs. known facts.}}

---

## 8. Open items for this Cortex

{{Living list of conventions to figure out. Move resolved items to
section 4, 5, 6, or 7 once stable.}}

- [ ] {{example: decide naming convention for cross-jurisdiction
      concepts.}}
- [ ] {{example: confirm whether entity pages for individuals should
      include contact details or just role/title.}}

---

## 9. Source isolation reminder

This Cortex contains only what has been provided in conversation
or via explicit ingest. The LLM does not import facts from memory,
sibling skills loaded in the same session, or general knowledge.

If the LLM proposes content for this Cortex that doesn't trace to
a source listed in `04-pointers/`, an explicit user statement
captured in `02-working-memory/log/`, or an ingested document under
`01-canonical/sources/`, treat the proposal as a question to
confirm — not as a fact to record.

---

## 10. Concurrency and Git

{{Case-specific merge or branch conventions. Default: read files before
editing, keep edits narrow, preserve append-only Layer 2 history, and
merge conflicts by keeping both pieces of provenance unless the user
explicitly says one is wrong.}}

---

## 11. Change Log

> Append-only. Newest first. When a convention is revised, write a new
> entry; do not silently rewrite an old one.

- {{YYYY-MM-DD}} — Initial CLAUDE.md from cortex initialisation.
