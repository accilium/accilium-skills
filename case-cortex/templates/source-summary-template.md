---
kind: source-summary
first_seen: {{YYYY-MM-DD}}
sources:
  - 04-pointers/{{FILE}}.yaml#{{POINTER_ID}}
confidentiality: {{CONFIDENTIALITY}}
tags:
  - {{TOPICAL_TAG}}
updated: {{YYYY-MM-DD}}
---

# {{HUMAN_READABLE_SOURCE_TITLE}}

> The LLM's reading notes on this source. Narrative-shape:
> describes what the source says, distinct from the fact-shape
> entity and concept pages that capture what the source teaches.
> Every Ingest produces one of these.

> Section headings below are English by default. If `CLAUDE.md`
> section 3 declares a different case language or heading map,
> translate the headings consistently and use the translated form
> thereafter.

## TL;DR

{{THREE_LINE_SUMMARY}}

## Source identity

- **Document type / Format**: {{DOCUMENT_TYPE}}
- **Author / Source**: {{AUTHOR_OR_SOURCE}}
- **As-of date**: {{SOURCE_AS_OF_DATE}}
- **Distribution / Confidentiality**: {{CONFIDENTIALITY}}
- **Size / Length**: {{SIZE_OR_LENGTH}}

## Parties involved

- **{{PARTY_1}}** — {{ROLE_IN_SOURCE}}
- **{{PARTY_2}}** — {{ROLE_IN_SOURCE}}

## Structural breakdown

{{STRUCTURAL_BREAKDOWN}}

### {{SECTION_OR_SHEET_1}}

{{SECTION_1_NOTES}}

### {{SECTION_OR_SHEET_2}}

{{SECTION_2_NOTES}}

## Key facts

> Numbered list. The 5-15 most load-bearing facts in the source.
> Each fact should be specific enough that someone reading only
> this section could quote the source on it.

1. {{FACT_1_WITH_PARAPHRASE_OR_QUOTE}}
2. {{FACT_2}}

## Notable quotes

> Direct quotes worth preserving verbatim: definitions, clauses,
> stipulations, surprising claims.

- > "{{QUOTE}}" — {{SECTION_OR_PAGE_REFERENCE}}

## Implications for the case

{{IMPLICATIONS_FOR_THE_CASE}}

## Generated entity pages

> Every entity page that was created or materially updated as a
> result of ingesting this source. Maintains the source-to-page
> fan-out audit trail.

- [`../entities/{{SLUG_1}}.md`](../entities/{{SLUG_1}}.md)
- [`../entities/{{SLUG_2}}.md`](../entities/{{SLUG_2}}.md)

## Generated concept pages

> Every concept page that was created or materially updated as a
> result of ingesting this source.

- [`../concepts/{{SLUG_1}}.md`](../concepts/{{SLUG_1}}.md)
- [`../concepts/{{SLUG_2}}.md`](../concepts/{{SLUG_2}}.md)

## Open questions from this source

- TODO({{YYYY-MM-DD}}): {{QUESTION_THIS_SOURCE_RAISED}}

## See also

- {{RELATED_SOURCE_SUMMARY}}
- {{RELATED_ENTITY_OR_CONCEPT_PAGE}}

## Change Log

- {{YYYY-MM-DD}} — Initial summary from ingest.
