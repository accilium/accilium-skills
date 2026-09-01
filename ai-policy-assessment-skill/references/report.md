<!-- Loaded in step 4, together with references/report-template.html. -->

# The report

Three moves: fill the data object, copy the template verbatim, run the checklist.

Only two things in the template are replaced: the object `REPORT_DATA` and the
placeholder `{{CLIENT}}` in the `<title>`. Structure, CSS and renderers stay
untouched.

**Copy the template, do not rewrite it from memory.** Reproducing the markup by hand
is where the layout breaks — reason texts squeezed into a narrow column, a table
wrapping one word per line, sections in the wrong order. If you cannot reproduce it
exactly, say so rather than shipping an approximation.

**Where a mandatory field is missing, work it out or say it is unknown — never
invent a number.** A report with made-up figures is worse than none, because it looks
checked.

**The report is written in English**, whatever language the conversation is in. That
is deliberate: the fixed labels in the template are English, the report travels
between teams and jurisdictions, and a half-translated report reads worse than a
consistently English one. Quotes from the policy stay in the policy's own language,
with a short English gloss where the quote alone would not carry.

## The three parts

The template renders three parts as **tabs** — one visible at a time, a sticky bar to
switch. Nothing in the data chooses the order or the labels; both are fixed.

| Part | Answers | Data used |
|---|---|---|
| **1 Input Overview** | Who is this, and which laws apply to them? | `meta.brief`, `profile`, `meta.value_streams`, `meta.assumed`, `legal` |
| **2 Management Summary** | What is not covered, how far does coverage go, where is it too strict — tiles and the matrix, kept visual on purpose | `headline`, `alerts`, `tiles`, `findings` (for the matrix) |
| **3 Deep Dives** | What exactly, based on which sentence, and what to change? | `duties`, `latitude`, `norms`, `risks`, `findings`, `na` |

Nothing is removed from the DOM when a tab is hidden, so printing and Ctrl+F reach
every part. `@media print` shows all three in sequence.

**Management Summary is kept deliberately light** — the insight sentence, the tiles and the matrix, almost no prose beyond that. Anything that needs a paragraph per row (open duties, the risk list, coverage bars, the findings table) belongs in Deep Dives instead, however tempting it is to surface it earlier for visibility.

Three sections hide themselves when their array is empty: `alerts`, `latitude`, `na`.
An empty box reads as an omission; no box reads as "not applicable here".

## The data contract

Twelve blocks. What is not listed here does not render.

### `meta`

| Field | Required | Content |
|---|---|---|
| `client` | yes | client name — appears in the subtitle and the file name |
| `policy` | yes | document name with version and date, e.g. `"AI Policy v2.1 (as of 03/2026)"` |
| `generated` | yes | `YYYY-MM-DD` |
| `classification` | yes | default `"Confidential"`; renders as a badge and in the footer |
| `depth` | yes | `"quick"` · `"standard"` · `"extensive"` — renders as a badge and a footer paragraph |
| `method` | yes | one sentence: checks in the catalogue, of those active, of those not applicable |
| `assumed` | no | array of things defaulted rather than answered, in plain words (`"what already exists internally"`, not `"profile.has"`). An empty array hides the line |
| `scope` | yes | `"S1"` group · `"S2"` company · `"S3"` function · `"S4"` use case. The template renders it in plain words in the footer; the code itself never reaches the reader |
| `scope_text` | yes | the scope in plain words |
| `scope_note` | yes | **the calibration rule that applied** — what counted as actionable at this level. Without it every framework policy reads like a bad use-case policy. State the rule only: the template already prints the scope in plain words ahead of it, so do not open with "Assessed as a group policy" |
| `brief` | yes | **one paragraph** in the client's own terms: who they are, how they use AI, which data is in scope, what kind of document this is. Not a restatement of the intake option labels |
| `value_streams` | no | the free-text answer, recognisably close to what the client said. Omit it and the highlighted line disappears |
| `legal_asof` | yes | `YYYY-MM-DD` — **the date the stored legal texts were checked**, read from `laws/README.md`. Not the generation date. Renders in the banner above the tabs and in the footer. Conflating the two would tell the reader the law was checked today when it was not |
| `sources` | yes | one sentence: which acts were cited, that wording came from the stored official text where available and is otherwise a paraphrase, and that ISO numbers are mapping aids against a licensed standard. **One sentence, no per-norm marks** — see `method.md` § 4.7 |

`depth` is not cosmetic. At `quick` the report contains states that look like
findings but are not — NIS2 "to be checked", no high-risk classification, generic
recommendations. The footer explains that those follow from what was never asked.

### `profile`

A free object of short key/value pairs, in display order, rendering as the fact grid.
Usual keys: Scope, Role, Sourcing, Data, Systems may, Operates in.

**Grid cells, not sentences.** The narrative belongs in `meta.brief`.

### `legal`

`frameworks` is an array of `name`, `status`, `trigger`.

- `status` — use `"applies"` for the affirmative case; the template colours anything
  starting with "appl" teal and everything else grey. `"to be checked"` is a valid and
  honest state, not a gap.
- `trigger` — the intake answer the applicability follows from, e.g. `"Personal data
  in scope (answer D)"`. Never "per the catalogue": the reader has to be able to check
  it.

`divergence` is `null` or text: a difference between what the client assumed and what
the answers imply, in either direction, with the triggering answer. See `method.md`
§ 4.4.

### `alerts`

An array. **Empty hides the section, which is the normal case.** Only for the two
special findings in `method.md` § 4.5 — a prohibited practice, automated individual
decision-making. Fields: `title` (the finding in one line), `body` (why it applies,
with the triggering answer), `basis` (the provision, plus the sentence saying this is
not a design option).

### `tiles` — exactly five, in this order

| # | Label | Value | Segments |
|---|---|---|---|
| 1 | `"Legal duties met"` | the count, e.g. `"9"`, unit `"of 12"` | none |
| 2 | `"Information security"` | the mean, one decimal, unit `"of 5"` | the mean rounded to a whole number |
| 3 | `"AI governance"` | the mean, one decimal, unit `"of 5"` | as above |
| 4 | `"AI-specific risks"` | categories covered, unit `"of 8 checked"` | none |
| 5 | `"Stricter than needed"` | the count of `strict` findings, unit `"rules"` | none |

Each carries `note` — one short sentence saying what the number means for this
client, not what the metric is — and `tone`: `"ok"` teal, `"bad"` magenta,
`"neutral"` grey, which colours only the left edge and the segments.

**Why five and not four, and why this fifth one.** The first three answer legal
exposure and maturity; the fifth answers business cost. None of them answers whether
the threats specific to *this technology* are covered — and that is the question that
goes stale fastest, because the attack surface moves while the law stands still. A
policy can be at 9 of 12 legal duties and not mention prompt injection.

**Tile 4 must not read like tile 1.** Its unit says `"of 8 checked"`, not `"of 10"`,
because this catalogue checks eight of the ten OWASP categories and saying otherwise
would imply coverage that is not there. Its `note` names the most serious uncovered
category in plain words — "Instructions hidden in content the assistant reads are not
addressed" — never a bare count. `tone` may be `"bad"` where a real risk is
uncovered: the tile is about actual exposure, not legal shortfall. What it must never
do is suggest a legal consequence; the label says "AI-specific risks", not
"compliance".

There is still no overall maturity number. Two coverage figures and a duty ratio say
more than one blended number, which would hide the divergence between security and
governance. `note` on tiles 2 and 3 carries the word from `method.md` § 5.8 — weak,
partial, solid, strong — because a reader takes the word before the decimal.

### `duties`

`total` and `met` are numbers (`met` = level 4 or higher). `open` is the array of
unmet duties: `id`, `title` (the requirement in a few words), `norm` (the reference),
`risk` (**the named exposure** — "supervisory measures", "injunctive relief", "loss of
trade secret protection" — never "compliance risk"), `level` (1-5, same scale as
`findings[].level` — the template labels the column and states the level-4 bar
in the intro sentence; a bare number with nothing to read it against is not a
finding, it is a cipher).

Kept apart from `findings` because a management board needs the one number, not the
mixture of duty and good practice.

### `latitude` — what is required, and what you decide

An array, one entry per topic that matters for this profile. Three to eight entries —
a decision aid, not a catalogue dump. Empty hides the section.

| Field | Content |
|---|---|
| `topic` | in the client's words, e.g. "Customer data in AI systems" |
| `norm` | the norm that sets the minimum, or plainly `"no direct legal requirement"` |
| `must` | what is not up for discussion, one or two sentences |
| `choice` | what is left to the company, concrete enough to decide on |
| `evidence` | the sentence from the policy that settles it, with its section |
| `use` | `"used"` · `"unused"` a flat answer where the law grades · `"beyond"` the policy goes further than the law requires |

Two rules hold this section honest:

1. **Never claim freedom that does not exist.** Where the duty is absolute, `must`
   carries it and `choice` says so. Inventing latitude is worse here than anywhere
   else in the report, because a client may act on it.
2. **`beyond` is not a defect.** Going further than the law is legitimate — for a
   certification goal, for customer requirements, out of caution. This section only
   makes it visible as a decision rather than an obligation.

### `headline`

`title` — the finding-bearing sentence in the header. Not a topic label ("Results of
the assessment") but the result itself.

`insight` is inserted **as HTML**: `<b>` is allowed, to highlight the decisive part.
For exactly that reason **no unchecked string from the client document goes in
there** — quotes belong in `findings`, where they are escaped.

### `findings`

The core. Per finding:

| Field | Content |
|---|---|
| `id` | criterion ID from `criteria.md`. Renders small and grey, not as the leading column |
| `nature` | `"duty"` · `"duty_conditional"` · `"choice"` — **as it stands for this client**, not as the catalogue classifies it in the abstract. A `duty_conditional` criterion whose condition is not met is passed as `"choice"`; otherwise the table labels it "Required by law" when no law requires it here |
| `group` | `data` · `model` · `use` · `infra` · `governance` — drives the filter chips |
| `type` | `"ok"` · `"gap"` · `"strict"` |
| `level` | 1-5, teal from 4 up |
| `risk` | 1-5, the vertical matrix axis |
| `strictness` | 1-5, the horizontal matrix axis |
| `statement` | the finding as a statement, not a question and not a topic label |
| `note` | optional, one sentence. Use it for the cannot-work case (`method.md` § 5.6) or to say a finding rests on a default |
| `evidence` | `{ref, quote}` — section plus a verbatim quote of at most two sentences — or `null` |
| `recommendation` | the concrete change to the rule. Never "review this" |

Five rules that are not negotiable:

1. **No level above 1 without `evidence`.** `evidence: null` renders visibly as "not
   addressed", which is a valid statement. An invented quote devalues the whole
   report.
2. **An unmet duty is never `strict`.** Where the law leaves no room, a flat rule is
   the requirement.
3. **`risk` and `strictness` are independent of `level`.** The matrix asks whether the
   depth of regulation matches the risk; `level` asks how well the rule is made. A
   finding can be level 5 and still be too strict.
4. **Spread `risk` and `strictness` honestly across 1-5.** If everything lands on 4
   and 5 the matrix says nothing.
5. **Sorting is built in.** Unmet duties first, then over-strict rules, then by level
   ascending. The order you pass has no effect.

Cap the count by depth: 10 at `quick`, 18 at `standard`, all at `extensive`.

### `norms`

An array of `name`, `kind`, `covered`, `total`. `kind` is `"law"` (a gap is a legal
shortfall) or `"standard"` (relevant only with a certification goal, otherwise a
benchmark). The template prints that explanation per group, and renders `standard`
rows visibly lighter — thinner track, grey fill — than `law` rows.

**The `standard` rows need the harder disclaimer, not the softer one.** ISO/IEC
27001, 27017 and 27701 are generic information-security standards, and a bar
labelled with one of those names inside an *AI policy* report reads, at a glance,
like this tool has started auditing the company's general ISMS — which is exactly
what the scope rule in `criteria.md` exists to prevent. It has not: every criterion
behind these numbers is still one of the 27 AI-specific checks, carrying only a
secondary cross-reference to a control number for a certification effort. Say that
plainly next to the group, not as a footnote — "not a legal requirement, and not an
audit of your general security setup" is the sentence that has to survive a skim.

**There is no `practice` group any more, and nothing here may carry OWASP or NIST.**
A ratio over "criteria that happen to cite this document" is not interpretable: with
three citations it renders `0 of 3`, which a reader takes for "three of ten
categories". OWASP goes in `risks[]` below, by name. NIST is a process framework, not
a threat list, and appears in no criterion — see `criteria.md`. Putting either beside
"9 of 12 AI Act" would read as an equivalent shortfall, and it is not one.

At `quick`, list the `law` group only — mapping 20 ISO controls is not worth the run
time when nothing else was asked either. At `standard` and `extensive`, list both.

### `risks` — the OWASP categories, by name

An array, one entry per category `criteria.md` maps to this catalogue — eight of the
ten. This is what tile 4 counts and what replaces a practice bar.

| Field | Content |
|---|---|
| `id` | `"LLM01"` … `"LLM10"`, the **2026** numbering |
| `name` | the category in plain words — "Instructions hidden in processed content", not "Prompt Injection", where the plain phrasing is clearer |
| `status` | `"ok"` every mapped criterion reaches level ≥ 4 · `"partial"` at least one does · `"gap"` none does · `"na"` the profile rules it out |
| `refs` | the criterion IDs behind the verdict, e.g. `"USE-01"` — without this the status is an assertion |
| `note` | one sentence: for `gap` and `partial`, what is missing; for `na`, why it does not apply |

Two rules:

1. **Also list the two categories this catalogue does not check** — `LLM06`
   Unbounded Consumption and `LLM08` Hidden Context Exposure — with `status: "gap"`,
   `refs: null` and a note saying no criterion covers it. Omitting them would make
   eight of ten look like ten of ten. The template renders them in a separate
   "not checked here" group.
2. **`na` needs a profile reason, not a judgement.** "You do not train models, so
   training-data poisoning does not apply to you" is valid. "Unlikely in practice" is
   not.

### `na`

An array of `id` and `reason`. Criteria that do not apply count towards nothing, but
they are disclosed. Quietly shortening the catalogue reads like full coverage.

## What does not get touched

**The palette.** The values in `:root` are validated against colour vision
deficiency (deltaE 8.3 deutan, 20.4 normal vision, both PASS). A different hue breaks
that without it being visible on screen.

**Filled versus hollow.** `gap` and `strict` share the hue on purpose — the palette
has only two reliably distinguishable chromatic poles. Filled versus hollow plus the
label is what separates them, and it survives greyscale printing. Do not add a third
hue, and do not add glyphs back into the matrix cells.

**The renderers.** Sorting, filters and escaping are part of the statement, not the
layout.

## File name and classification

```
[YYYY-MM-DD]_AI-Policy-Check_<company>_DRAFT.html
```

Client documents and the report stay local. Nothing is uploaded or shared without
explicit clearance. Default classification: **Confidential** — it travels with the
file, in the badge and in the footer.

## Checklist before handing over

- [ ] `{{CLIENT}}` in the `<title>` replaced
- [ ] no example value left — "Example Group", the example IDs, the example quotes
- [ ] every finding above level 1 carries a section reference and a real quote from
      the document
- [ ] `findings[].group` values all appear in the filter chips, and every chip
      returns rows
- [ ] `duties.met` plus `duties.open.length` is consistent with `duties.total`
- [ ] the matrix counts add up to the number of findings
- [ ] every finding's `type` agrees with its position: `strict` sits below the
      diagonal band (strictness clearly above risk), `gap` above it — the template
      colours the cell from `type`, so a mismatch here renders visibly wrong, not
      just inconsistently
- [ ] `risk` and `strictness` use the whole 1-5 range, not just 4 and 5
- [ ] exactly five tiles, in the prescribed order, tiles 2 and 3 carrying `segments`
- [ ] tile 4's unit says "of N checked", and N matches the non-`na` entries in
      `risks` that carry `refs`
- [ ] `risks` lists all ten categories — the eight checked, plus `LLM06` and `LLM08`
      with `refs: null`
- [ ] every `risks` entry above `na` names its criteria in `refs`
- [ ] no `norms` entry carries OWASP or NIST, and there is no `practice` group
- [ ] `meta.legal_asof` is read from `laws/README.md`, not set to today's date
- [ ] `alerts`, `latitude` and `na` empty where they do not apply — no empty box
- [ ] `meta.depth` set, and at `quick` nothing in the report asserts a high-risk
      classification or NIS2 applicability that was never asked about
- [ ] `meta.brief` reads as a profile of this company, not as a list of intake labels
- [ ] every `latitude` row names a norm, or says plainly that none applies, and none
      claims freedom where the duty is absolute
- [ ] all three tabs reachable, and printing shows all three parts
- [ ] **every recommendation read back against the scope rule**: would following it
      copy content an information security policy already carries? If yes, rewrite it
      as the missing connection (`criteria.md` § "Scope")
- [ ] no defect reported twice under two criteria
- [ ] read the report as a managing director would: is there a sentence that would
      survive unchanged in a report about a different company? Cut it
