# Domain template — research

Layer 1 scaffolding for research programs (academic, industry,
policy, market research, journalism, etc.).

---

## identity.md

```markdown
# Identity

## Project

- **Name:** {{PROJECT_NAME}}
- **Slug:** {{PROJECT_SLUG}}
- **Research type:** {{empirical | theoretical | survey | literature review | investigative | mixed}}
- **Status:** {{scoping | data-gathering | analysis | writing | review | published}}
- **Started:** {{YYYY-MM-DD}}

## Research question

{{The central question this project tries to answer. One or two
sentences. If there are sub-questions, list them under it.}}

## Hypotheses (if applicable)

- {{H1}}
- {{H2}}

## Intended output

- {{paper | report | article | dataset | talk | internal memo}}
- {{target venue / publication / audience}}
- {{target date}}

## Success criteria

- {{what a successful outcome looks like}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```

---

## entities/ — initial seed list

Entities live as individual files under
`01-canonical/entities/{{SLUG}}.md`, one per named real-world thing
with identity that *acts* in the case. There is no `entities.md`
skeleton file — the directory is the structure. For research
programs, seed the `entities/` directory with at least these page
kinds at Initialize time (each file uses
`templates/entity-template.md`):

- **Research team** — one page per named team member (PI,
  co-author, RA, advisor) with `entity_type: person`. Affiliation
  goes into the identity-facts section.
- **Funders / sponsors** — one page per named funding body with
  grant number and reporting requirements as identity facts
  (`entity_type: organization`).
- **Subject institutions / named data sources** — one page per
  named institution accessed or named dataset (`entity_type:
  organization | product`). Methodologies and abstract populations
  are *concepts*, not entities.
- **Named collaborators / peer reviewers** — one page each for
  named external advisors with a meaningful role (`entity_type:
  person`).
- **Competing / related research groups** — one page per named
  group whose work the project engages with (`entity_type:
  organization`).

Reference these from `index.md` under the entities section. The
theoretical framings, methods, hypotheses, and competing claims
belong in `concepts/` and cross-link to the entities that hold or
contest them.

---

## scope.md

```markdown
# Scope

## Scope of inquiry

- {{what is being studied, at what level of analysis, over what
  time range}}

## Out of scope

- {{what is explicitly excluded and why}}

## Methodology

- {{method(s) — experimental, observational, computational,
  qualitative, etc.}}
- {{data sources and collection approach}}
- {{analytical approach}}

## Ethical / regulatory considerations

- {{IRB approval, consent, data protection, dual-use concerns}}

## Constraints

- {{time | budget | access | data availability | computational limits}}

## Deliverables

- {{manuscript, code, dataset, pre-registration, talk, etc.}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```

---

## context.md

```markdown
# Context

## Literature / prior work

{{Key prior work this project builds on or argues against. Link
citations to Layer 4 pointers.}}

## Theoretical framing

{{The conceptual lens used. What tradition, what school of
thought, what paradigm.}}

## Empirical backdrop

{{Relevant data, trends, events in the world that make this
research question live.}}

## Why now

{{What makes this research timely. New data available, recent
events, emerging debate, etc.}}

## Known gaps and contested claims

{{What the field doesn't yet know, and where experts currently
disagree — this is often where the contribution lives.}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```
