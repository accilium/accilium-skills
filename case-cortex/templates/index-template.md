---
kind: index
updated: {{YYYY-MM-DD}}
---

# {{CASE_NAME}} — Index

> The curated catalog of every page in the Cortex, grouped by
> topical cluster. This is the page a user navigates by. Keep it
> grouped, not alphabetical — clusters are the high-bandwidth way
> to find what you need. Update on every Ingest.

## Spine

- [`overview.md`](./overview.md) — narrative entry point
- [`synthesis.md`](./synthesis.md) — current best thinking, open
  risks, parameters
- [`index.md`](./index.md) — this file

## Skeleton (Layer 1)

- [`identity.md`](./identity.md) — case identity, purpose, status
- [`scope.md`](./scope.md) — in-scope, out-of-scope, constraints
- [`context.md`](./context.md) — regulatory / sectoral / historical
  backdrop

## Entities — by cluster

> Each cluster groups entities by their role in the case. Add new
> cluster headings when entities justify their own grouping. Empty
> clusters are fine — they signal where future Ingest work will land.

### {{CLUSTER_A_CLIENT_SIDE}}

- [`entities/{{SLUG_1}}.md`](./entities/{{SLUG_1}}.md) — {{ONE_LINE_DESCRIPTION}}
- [`entities/{{SLUG_2}}.md`](./entities/{{SLUG_2}}.md) — {{ONE_LINE_DESCRIPTION}}

### {{CLUSTER_B_COUNTERPARTIES_ADVISORS}}

- ...

### {{CLUSTER_C_REGULATORS_JURISDICTIONS}}

- ...

## Concepts — by topical cluster

> Each cluster is a curated grouping. Add a new cluster heading
> rather than appending to a flat list when concepts justify their
> own grouping. Empty clusters are fine — they signal where future
> Ingest work will land.

### {{CLUSTER_A_PRICING_MECHANICS}}

- [`concepts/{{SLUG_1}}.md`](./concepts/{{SLUG_1}}.md) — {{ONE_LINE_DESCRIPTION}}
- [`concepts/{{SLUG_2}}.md`](./concepts/{{SLUG_2}}.md) — {{ONE_LINE_DESCRIPTION}}

### {{CLUSTER_B_DECISION_RULES}}

- ...

### {{CLUSTER_C_DEFINITIONS_AND_TERMS}}

- ...

## Sources (`01-canonical/sources/`)

> One entry per ingested source. Reverse-chronological.

- [`sources/{{YYYY-MM-DD}}_{{SLUG}}.md`](./sources/{{YYYY-MM-DD}}_{{SLUG}}.md) — {{ONE_LINE_SOURCE_DESCRIPTION}}

## Working memory pointers (Layer 2)

- [`../02-working-memory/decisions.md`](../02-working-memory/decisions.md) — append-only decision log
- [`../02-working-memory/open-questions.md`](../02-working-memory/open-questions.md) — open questions
- `../02-working-memory/log/` — chronological event log

## Derived artifacts (Layer 3)

> Active briefings, comparisons, lint reports, analyses generated
> from the Cortex. Older artifacts move to
> `../03-derived/_archive/` per the retention convention; archived
> entries do not need to appear here.

- {{NONE_YET_POPULATED_AS_WORKFLOW_5_PRODUCES_THEM}}

## External pointers (Layer 4)

- [`../04-pointers/systems.yaml`](../04-pointers/systems.yaml) — internal systems
- [`../04-pointers/external.yaml`](../04-pointers/external.yaml) — external sources

## Change Log

- {{YYYY-MM-DD}} — Initial index from cortex initialization.
