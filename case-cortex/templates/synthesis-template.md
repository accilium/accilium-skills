---
kind: synthesis
updated: {{YYYY-MM-DD}}
---

# {{CASE_NAME}} — Synthesis

> This is the opinion-bearing layer of the Cortex. Concept and
> entity pages describe what *is*; this page describes what we
> *think*. It is allowed to be wrong, allowed to be incomplete,
> allowed to contradict its prior self as long as the supersession
> is dated. Update only on Ingests that *materially* shift your
> view — do not bump the date on a no-change Ingest. Lint detects
> material staleness via content hash, not mtime.

> Section headings below are English by default. If `CLAUDE.md`
> section 3 declares a different case language, translate the
> headings consistently and use the translated form thereafter.

## Current direction

{2–4 short paragraphs. Where the case is pointing right now — the
working hypothesis, the current best design, the position you would
defend in front of a reviewer today. Be concrete: name parameters,
mechanisms, and the structural choices behind them. Don't hedge
into mush. If you don't know, say "unknown — see open questions"
rather than soft-pedalling.}

## Open risks

{Numbered list. The risks you would warn the user about if they
shipped the current direction tomorrow. Each item: what could go
wrong, why, and the trigger that would tell you it has gone wrong.}

1. **{{RISK_TITLE}}** — {{SHORT_DESCRIPTION_AND_WHY_NON_TRIVIAL}}.
2. ...

## Parameter calibrations

{{WHERE_THE_CASE_HAS_PARAMETERS_AND_REASONING_FOR_CURRENT_CALIBRATION}}

- **{{PARAMETER_NAME}}** — current value: {{VALUE}}. Reasoning: {{WHY_THIS_VALUE_AND_ALTERNATIVES}}.

## Chosen design patterns

- **{{PATTERN}}** — chosen because {{REASON}}; trade-off accepted:
  {{WHAT_WE_GAVE_UP}}.

## Rejected design patterns

- **{{PATTERN}}** — rejected because {{REASON}}. Could be revisited if
  {{TRIGGER_CONDITION}}.

## Benchmark gap

{What comparable cases / peer firms / prior precedents we *should*
have looked at but haven't yet. Be honest about gaps in the
comparison set — they age fastest.}

## Open questions by topic

### {{TOPIC_BLOCK_1}}

- {{QUESTION_1}}
- {{QUESTION_2}}

### {{TOPIC_BLOCK_2}}

- {{QUESTION_1}}

## Parked items

{Things that are out of scope right now but worth re-raising later.
Each item carries a date so we can age it out.}

- {{YYYY-MM-DD}} — {{TOPIC}}. Re-raise when {{TRIGGER}}.

## Change Log

- {{YYYY-MM-DD}} — Initial synthesis stub. No sources ingested yet;
  this page will fill in as Ingest fans out concepts and entities.
