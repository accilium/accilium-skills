# Domain template — consulting

Layer 1 scaffolding for consulting cases (strategic reviews,
transformations, due diligence, tender responses, advisory mandates).

---

## identity.md

```markdown
# Identity

## Case

- **Name:** {{CASE_NAME}}
- **Slug:** {{CASE_SLUG}}
- **Type:** {{strategic review | transformation | DD | tender | advisory | other}}
- **Status:** {{pre-kickoff | active | on-hold | wrapping-up | closed}}
- **Started:** {{YYYY-MM-DD}}

## Purpose

{{One paragraph: why this case exists, what it is meant to achieve.}}

## Success criteria

- {{measurable outcome 1}}
- {{measurable outcome 2}}
- {{measurable outcome 3}}

## Mandate

- **Sponsor:** {{client-side executive sponsor}}
- **Scope owner:** {{who signs off on scope changes}}
- **Primary deliverable:** {{what the client actually walks away with}}
- **Timeline:** {{start → milestone dates → end}}

## Commercials

- **Engagement type:** {{fixed fee | T&M | success fee | hybrid}}
- **Budget or fee:** {{amount}}
- **Billing milestones:** {{if any}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```

---

## entities/ — initial seed list

Entities live as individual files under
`01-canonical/entities/{{SLUG}}.md`, one per named real-world thing
with identity that *acts* in the case. There is no `entities.md`
skeleton file — the directory is the structure. For consulting
cases, seed the `entities/` directory with at least these page
kinds at Initialize time (each file uses
`templates/entity-template.md`):

- **Client organization** — `entities/{{CLIENT_SLUG}}.md`
  (organisation; identity facts = HQ, ownership, sector, size).
- **Client stakeholders** — one page per named individual who
  plays a meaningful role: sponsor, champion, skeptic, blocker
  (`entity_type: person`).
- **Engagement team (ours)** — one page per named team member with
  a meaningful role on the case (`entity_type: person`).
- **Third parties** — one page per named auditor, legal counsel,
  specialist vendor, consortium partner (`entity_type:
  organization` or `legal-entity`).
- **Competitors / comparable actors** — one page each, only if
  they actually matter to the case logic (not just "in the same
  market").

Reference these from `index.md` under the entities section. Use
`scope.md` and `context.md` to point into them with one-line
links — the rich content lives on the entity pages, not in the
skeleton.

---

## scope.md

```markdown
# Scope

## In scope

- {{workstream / topic / asset 1}}
- {{workstream / topic / asset 2}}

## Out of scope

- {{explicit exclusions — these matter as much as inclusions}}

## Assumptions

- {{assumption 1 — what we're taking as given}}
- {{assumption 2}}

## Constraints

- {{time | budget | access | confidentiality | regulatory constraint}}

## Dependencies

- {{things this case depends on that we don't control}}

## Deliverables

- {{named deliverable 1 + format + due date}}
- {{named deliverable 2}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```

---

## context.md

```markdown
# Context

## Sector context

{{2–4 short paragraphs on the sector the client operates in.
Relevant dynamics, trends, regulatory environment, competitive
pressures.}}

## Client context

{{What is going on with this specific client right now that makes
this case relevant. Recent events, strategic shifts, leadership
changes, M&A activity.}}

## Historical context

{{Prior engagements with this client, past attempts at this
problem, relevant institutional memory.}}

## Regulatory / compliance context

{{Applicable regulations, reporting requirements, standards. Link
to Layer 4 pointers for authoritative sources.}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```
