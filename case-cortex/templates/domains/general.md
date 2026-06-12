# Domain template — general

Layer 1 scaffolding for cases that don't fit a specific domain flavor — or
where the user wants a minimal, flexible starting point.

Fewer prescribed sections than the domain-specific templates. Use this
when you're not sure which flavor fits, and extend from here.

---

## identity.md

```markdown
# Identity

## Case

- **Name:** {{CASE_NAME}}
- **Slug:** {{CASE_SLUG}}
- **Status:** {{initialized | active | on-hold | wrapping-up | closed}}
- **Started:** {{YYYY-MM-DD}}

## Purpose

{{One paragraph: what this case is about and why it exists.}}

## Desired outcome

{{What a successful end-state looks like. Not necessarily measurable
on day one — refine as the case progresses.}}

## Key dates

- {{event}}: {{YYYY-MM-DD}}

## Owner

- {{name}} — {{role / context}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```

---

## entities/ — initial seed list

Entities live as individual files under
`01-canonical/entities/{{SLUG}}.md`, one per named real-world thing with
identity that *acts* in the case. There is no `entities.md` skeleton
file — the directory is the structure. For a generic case, seed the
`entities/` directory with whichever of these page kinds apply (each
file uses `templates/entity-template.md`):

- **People** — one page per named individual with a meaningful role
  (`entity_type: person`).
- **Organizations** — one page per named org or legal entity
  (`entity_type: organization | legal-entity`).
- **Systems, assets, or named artifacts** — one page per named
  system, asset, or named artifact with identity (`entity_type:
  system | product`). Generic categories ("our infrastructure")
  stay as a concept page.

Don't seed empty entity pages. Add a page when the entity actually
shows up in a source or a working-memory entry, and the user has
confirmed the slug. Mechanisms, ideas, and policies belong in
`concepts/`.

Reference seeded entity pages from `index.md` under the entities
section.

---

## scope.md

```markdown
# Scope

## In scope

- {{what this case covers}}

## Out of scope

- {{what is explicitly excluded}}

## Assumptions

- {{what we're taking as given}}

## Constraints

- {{time, budget, access, confidentiality, or other constraints}}

## Deliverables / outputs

- {{what gets produced by the end of this case}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```

---

## context.md

```markdown
# Context

## Background

{{What the reader needs to know to make sense of this case. Situational
context, history, environment.}}

## Why now

{{What makes this case live — the trigger, the deadline, the opportunity.}}

## Related history

{{Prior work, prior attempts, institutional memory that bears on this
case.}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```
