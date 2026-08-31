# Legal references

One file per act. **Loaded on demand, never up front.** `method.md` § 4 decides which
acts apply to the profile; only those files get opened. A run against a German
engineering group touches `eu-ai-act.md`, `gdpr.md`, `works-council.md` and
`trade-secrets.md`. DORA and MDR stay closed.

| File | Act | Read it when |
|---|---|---|
| `eu-ai-act.md` | Regulation (EU) 2024/1689 | always, unless there is no activity in the EU |
| `gdpr.md` | Regulation (EU) 2016/679 | personal data is in scope, which is nearly always |
| `nis2.md` | Directive (EU) 2022/2555 + national transposition | size and sector cross the threshold |
| `sector-acts.md` | DORA · CRA · MDR | financial entity · product with digital elements · medical device |
| `works-council.md` | BetrVG · ArbVG | employees in Germany or Austria |
| `trade-secrets.md` | GeschGehG · Directive (EU) 2016/943 | design data, source code, customer data under NDA |
| `standards.md` | ISO/IEC 27001, 27017, 27701, 42001 · NIST AI RMF · OWASP LLM Top 10 | `extensive` runs, and where a certification goal exists |

## What these files are

They carry **article numbers and the substance of each obligation** — enough to decide
whether a criterion is a duty for this profile and to name the reference in the
report. That is their job.

**`verbatim:` is the one convention that matters.** A block under an article's heading
means that article's official text was pasted in and can be quoted. Everything without
one is a paraphrase with a citation, and a paraphrase is never presented as wording.

So there is exactly one rule for citing law:

> **Cite the article. Quote only from a `verbatim:` block. Never quote a statute from
> memory.**

A statute paraphrased and labelled as a paraphrase is useful. A statute quoted from
memory and presented as the wording is a liability — someone may put it in front of a
client's legal department.

### Current state

Verbatim blocks exist for: **EU AI Act** (24 articles) · **GDPR** (17) · **NIS2** (8) ·
**DORA** (7) · **CRA** (4 provisions) · **MDR** (4) · **BetrVG** (6) · **ArbVG** (4) ·
**GeschGehG** (6) · **OWASP LLM Top 10** (5 of 10 categories: LLM01, LLM03, LLM05,
LLM06, LLM10). Each file's own banner lists exactly which.

Not pasted, therefore paraphrase only: **ISO/IEC**, **NIST AI RMF**, the other five
OWASP categories, and **Directive (EU) 2016/943** (the EU instrument GeschGehG
transposes).

**Do not generalise from an act to its articles.** A citation outside the lists above
is a paraphrase like any other, even where the rest of that act is pasted in. Check
the file, do not assume.

Two act-specific caveats worth carrying into a report:

- **NIS2** — the Directive's own text is pasted for those 8 articles, but the numeric
  size thresholds in Art. 2 point to Recommendation 2003/361/EC, a separate instrument
  that is not stored here. Treat those figures as unverified regardless.
- **ISO** — beyond the paraphrase question, the control numbers are mapping aids
  against a licensed standard that cannot be stored here at all. Anyone who needs a
  certification statement has to check against the purchased text. That sentence
  belongs in the report.

### Adding verified text

Copy the article from the official source linked at the top of the relevant file,
paste it under its heading, mark the block `verbatim:`, and update that file's banner
and the list above. Note that fetching these texts from a sandboxed environment has
failed in the past — eur-lex, gesetze-im-internet, ris.bka.gv.at, nist.gov and
owasp.org all returned policy denials — so in practice a human pastes the text in.
Check again rather than assuming; environments change.

## The rule that overrides everything in this folder

These files structure the conversation with legal and data protection. **They are not
legal advice.** Nothing produced from them — a duty classification, a citation, a
recommendation — substitutes for a lawyer reading the actual document. Where an act's
applicability depends on a classification the intake cannot settle (a high-risk
classification under Annex III, a sector assignment under NIS2), the report names it
as a question for legal, not as a finding.
