# Domain template — investigation

Layer 1 scaffolding for investigations (internal, forensic,
journalistic, compliance, incident post-mortem).

---

## identity.md

```markdown
# Identity

## Investigation

- **Name / code name:** {{INVESTIGATION_NAME}}
- **Slug:** {{INVESTIGATION_SLUG}}
- **Investigation type:** {{internal | forensic | journalistic | compliance | incident-post-mortem | regulatory}}
- **Status:** {{intake | fact-gathering | analysis | reporting | closed}}
- **Opened:** {{YYYY-MM-DD}}
- **Opened by:** {{who initiated — GC, compliance, editor, IR lead, etc.}}

## Predicate

{{What triggered this investigation. A complaint, an anomaly, a tip,
an incident. One paragraph.}}

## Central questions

- {{primary question the investigation must answer}}
- {{secondary questions}}

## Scope and limits set at intake

- {{explicit bounds — time period, entities, systems, subject matter}}

## Deadlines

- {{preliminary findings due}}: {{YYYY-MM-DD}}
- {{final report due}}: {{YYYY-MM-DD}}
- {{external deadline — filing, disclosure, publication}}: {{YYYY-MM-DD}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```

---

## entities/ — initial seed list

Entities live as individual files under
`01-canonical/entities/{{SLUG}}.md`, one per named real-world thing
with identity that *acts* in the case. There is no `entities.md`
skeleton file — the directory is the structure. For
investigations, seed the `entities/` directory with at least these
page kinds at Initialize time (each file uses
`templates/entity-template.md`); investigations are an
entity-heavy domain — every named subject, witness, advisor,
regulator gets its own page so the trail of allegations and
evidence can hang off it.

- **Subjects / persons of interest** — one page per named
  individual (`entity_type: person`), with status (subject |
  witness | cooperating | uncooperative | cleared) tracked in the
  identity-facts section and updated as the investigation
  progresses.
- **Investigation team** — one page per named lead, member, and
  external advisor (`entity_type: person | organization`).
- **Oversight body** — one page for the audit committee, GC,
  regulator the investigation reports to (`entity_type:
  organization | regulator`).
- **Privilege ring members** — flagged on each relevant person's
  entity page rather than as a separate list.
- **Counterparties / external bodies** — one page each for named
  regulators, law-enforcement contacts, auditors, press contacts
  (`entity_type: organization | regulator`).

Reference these from `index.md` under the entities section.
Allegations, applicable rules, control mechanisms that should have
caught the issue, and evidentiary standards belong in `concepts/`
and cross-link to the entities they implicate. The footprint
section on each subject's entity page becomes the per-subject case
file.

---

## scope.md

```markdown
# Scope

## In scope

- {{entities, time periods, subject areas, transaction types}}

## Out of scope

- {{explicit exclusions — often as important as inclusions in
  investigations}}

## Evidentiary sources

- {{document custodians, data systems, interview subjects, external records}}

## Preservation / legal hold

- {{date legal hold imposed}}
- {{scope of hold — custodians, systems, date ranges}}

## Methodology

- {{approach to fact-gathering — interviews, document review, data
  analysis}}
- {{standards applied — balance of probabilities, clear and
  convincing, beyond reasonable doubt}}

## Constraints

- {{access limitations, jurisdictional issues, time pressure,
  resource limits}}

## Deliverables

- {{preliminary memo, interim updates, final report, referrals}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```

---

## context.md

```markdown
# Context

## Factual background

{{What is known to have happened, in chronological order, at the
time of intake. This evolves — update as new facts are
established, not as things are merely alleged.}}

## Organizational context

{{Structure, reporting lines, controls, governance relevant to the
investigation. Who was supposed to catch this, what control was
supposed to prevent it.}}

## Regulatory / legal context

{{Applicable laws, regulations, internal policies, industry
standards. What rule would be broken if allegations are
substantiated.}}

## Prior history

{{Previous investigations of similar issues, prior concerns raised
about the same subjects, relevant institutional memory.}}

## External environment

{{Market, political, media context. Whether this investigation is
likely to become public, whether regulators are already looking,
whether peers have had similar issues.}}

## Change Log

- {{YYYY-MM-DD}} — Initial seeding.
```
