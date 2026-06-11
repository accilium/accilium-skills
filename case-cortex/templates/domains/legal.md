# Domain template — legal

Layer 1 scaffolding for legal matters (litigation, transactions,
regulatory matters, internal investigations handled by counsel).

---

## identity.md

```markdown
# Identity

## Matter

- **Name:** {{MATTER_NAME}}
- **Slug:** {{MATTER_SLUG}}
- **Matter type:** {{litigation | transaction | regulatory | advisory | investigation}}
- **Status:** {{intake | active | pending | on-hold | closed}}
- **Opened:** {{YYYY-MM-DD}}
- **Client:** {{client org or individual}}

## Matter summary

{{One paragraph describing the matter in plain terms.}}

## Objectives

- {{client's primary objective}}
- {{secondary objectives}}

## Key dates

- {{event}}: {{YYYY-MM-DD}}
- {{statute of limitations / filing deadline / closing date}}: {{YYYY-MM-DD}}

## Engagement

- **Lead counsel:** {{name}}
- **Team:** {{associates, paralegals}}
- **Billing arrangement:** {{hourly | flat | contingency | hybrid}}
- **Conflict check completed:** {{YYYY-MM-DD}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```

---

## entities/ — initial seed list

Entities live as individual files under
`01-canonical/entities/{{SLUG}}.md`, one per named real-world thing
with identity that *acts* in the case. There is no `entities.md`
skeleton file — the directory is the structure. For legal
matters, seed the `entities/` directory with at least these page
kinds at Initialize time (each file uses
`templates/entity-template.md`):

- **Parties** — one page per named party: client, opposing party,
  co-defendant, counterparty, key witness, named third party
  (`entity_type: person | organization | legal-entity`).
- **Counsel** — one page per named law firm involved (our firm,
  opposing counsel, co-counsel) (`entity_type: organization`).
  Lead attorneys can be separate `entity_type: person` pages if
  individually load-bearing.
- **Tribunals / regulators / courts** — one page per named court
  or agency (`entity_type: regulator | jurisdiction`). The court
  is the entity; the docket / case number is identity-fact data
  on its identity section or on the matter's `identity.md`.
  Statutes and rulings are *concepts*, not entities — they
  describe how the law applies. (Specific named regulations or
  orders can be entities — see SKILL.md "Entity vs. concept" for
  the routing.)
- **Key non-party actors** — named experts, advisors, or
  witnesses whose individual identity matters (`entity_type:
  person`).

Reference these from `index.md` under the entities section. The
legal theories, statutes types, doctrines, and rulings the matter
turns on belong in `concepts/`, cross-linked to the entities that
invoke or are bound by them.

---

## scope.md

```markdown
# Scope

## Claims / issues in scope

- {{claim 1 — legal theory, elements, target relief}}
- {{claim 2}}

## Claims / issues explicitly out of scope

- {{excluded claims or issues}}

## Jurisdictional scope

- {{applicable jurisdiction(s), choice of law, venue}}

## Privilege ring

- {{who is covered by attorney-client privilege on this matter}}
- {{common-interest or joint-defense arrangements, if any}}

## Confidentiality

- {{protective orders, NDAs, ethical walls}}

## Deliverables

- {{named deliverables — filings, memos, opinion letters, settlement docs}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```

---

## context.md

```markdown
# Context

## Factual background

{{Plain-language narrative of what happened, in chronological
order. This is the "story" layer that non-lawyers can follow.}}

## Procedural history (if applicable)

{{Prior filings, rulings, settlements, related matters.}}

## Legal landscape

{{Controlling authorities, relevant statutes and regulations,
leading cases. Link to Layer 4 pointers for full texts.}}

## Commercial context

{{Business stakes — why this matter matters to the client beyond
the legal outcome. Impacts on operations, reputation, financials.}}

## Precedent / analogous matters

{{Related work by the firm, relevant industry precedent, comparable
cases.}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```
