# Domain template — engineering

Layer 1 scaffolding for engineering projects (product builds,
infrastructure work, systems integrations, incident investigations,
migrations).

---

## identity.md

```markdown
# Identity

## Project

- **Name:** {{PROJECT_NAME}}
- **Slug:** {{PROJECT_SLUG}}
- **Project type:** {{new-build | migration | integration | optimization | incident-response | research}}
- **Status:** {{scoping | in-development | testing | deployed | maintenance | retired}}
- **Started:** {{YYYY-MM-DD}}

## Problem statement

{{What problem this project solves, in 2–3 sentences. User-facing
phrasing preferred over technology phrasing.}}

## Goals

- {{functional goal}}
- {{non-functional goal — latency, availability, cost, etc.}}

## Non-goals

- {{things this project explicitly does not address}}

## Success criteria

- {{measurable, testable criteria}}

## Target timeline

- {{milestone}} — {{YYYY-MM-DD}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```

---

## entities/ — initial seed list

Entities live as individual files under
`01-canonical/entities/{{SLUG}}.md`, one per named real-world thing
with identity that *acts* in the case. There is no `entities.md`
skeleton file — the directory is the structure. For engineering
projects, seed the `entities/` directory with at least these page
kinds at Initialize time (each file uses
`templates/entity-template.md`):

- **Project team** — one page per named team member with a
  meaningful role on the project (`entity_type: person`).
- **Stakeholders** — one page each for named sponsor, named user
  persona owner, named reviewer / approver (`entity_type:
  person`). Generic personas ("end users") stay as a concept page.
- **Systems involved** — one page per named system, service, or
  database in scope (`entity_type: system`). Each page's
  identity-facts section carries owner team, criticality, runbook
  pointer.
- **External dependencies** — one page per named vendor or
  third-party service (`entity_type: organization | system`) with
  contract / SLA / licensing context as identity facts.

Reference these from `index.md` under the entities section.
Architectural patterns, protocols, technology choices, and design
decisions belong in `concepts/`, cross-linked to the systems they
apply to.

---

## scope.md

```markdown
# Scope

## In scope

- {{feature / system / integration}}

## Out of scope

- {{what is deferred or explicitly not part of this project}}

## Technical approach

- {{architectural direction, key decisions taken}}
- {{technology choices with one-line rationale each}}

## Constraints

- **Performance:** {{latency / throughput / capacity targets}}
- **Security:** {{classification, access controls, compliance regimes}}
- **Compatibility:** {{backward compatibility requirements, supported clients}}
- **Budget:** {{cost ceiling or target}}
- **Deadline:** {{hard or soft, and consequences of missing it}}

## Dependencies

- {{things this project needs from other teams}}

## Deliverables

- {{artifact — code, service, documentation, runbook, postmortem}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```

---

## context.md

```markdown
# Context

## Current state

{{What exists today. How users / systems solve this problem currently.}}

## Why now

{{Trigger for the project — new requirement, scaling issue,
deprecation, regulatory change, opportunity.}}

## Prior attempts (if any)

{{Previous efforts to address this, what worked, what didn't, what
was learned.}}

## Technical landscape

{{Relevant platforms, services, internal tools, external
dependencies. Link to Layer 4 pointers for runbooks, architecture
docs, ADRs.}}

## Known risks

- {{technical risk}}
- {{organizational risk}}
- {{timeline risk}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```
