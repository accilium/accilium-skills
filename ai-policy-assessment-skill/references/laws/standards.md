# Standards and good practice — ISO/IEC, NIST, OWASP

Not law. This is the group the coverage chart labels *standards, certifiable* and
*good practice*, and the distinction is load-bearing: a gap against ISO matters where
there is a certification goal, a gap against OWASP is a hint about attack paths, and
neither is a legal shortfall. See `references/report.md` on `norms[].kind`.

These are **secondary references** in the assessment: the mapping was made against
control titles and published summaries, not against the licensed standard text, and
the report says so in its footnote. ISO standards are not freely available; the text
cannot be stored here for licensing reasons, quite apart from network access.

## ISO/IEC 27001:2022 — information security management

Annex A carries 93 controls in four themes: organisational, people, physical,
technological. The ones this catalog maps to most often:

| Control | Topic |
|---|---|
| A.5.1 | policies for information security |
| A.5.7 | threat intelligence |
| A.5.19 to A.5.23 | supplier relationships, including cloud services |
| A.5.35 | independent review of information security |
| A.8.2 · A.8.3 | privileged access, information access restriction |
| A.8.16 | monitoring activities |
| A.8.25 to A.8.28 | secure development lifecycle, secure coding |

**Assessment note.** Where a company is already certified, the AI policy does not
need to restate these controls — it needs to say which of them AI use falls under.
Fulfilment by reference is explicitly allowed; see `references/method.md` § 5.3.

## ISO/IEC 42001:2023 — AI management system

The certifiable AI management standard. Annex A controls cover AI policy, roles and
responsibilities, impact assessment, lifecycle management, data governance,
third-party relationships, and information for users. Annex B gives implementation
guidance.

**Assessment note.** This is the standard a certification goal usually means when a
client says "we want to be ISO-certified for AI". The goal does not change how a rule
is scored here — the levels in `references/method.md` § 5.2 stay as they are. What it
changes is which gaps matter to the client: an auditor needs evidence, so for a
certification goal the interesting shortfall is every load-bearing rule sitting at
level 4 rather than 5. Say that in the finding; do not re-score for it.

## ISO/IEC 27090 — pending, metadata only

**Not integrated into the criteria catalog.** As of 2026-08-06, `iso.org` is
blocked from this environment like every other source tested so far (confirmed
directly: `CONNECT` to `www.iso.org` returns a 403 policy denial, the same result
as `eur-lex.europa.eu`, `nist.gov` and the rest — see `laws/README.md`). That is
not the operative limit here, though: the standard's own text has not been
publicly released yet, so even a human pasting it in would only be able to paste
what is itself pre-publication project metadata, not the operative wording — the
same situation as an EU regulation still under trilogue, except that here there is
no verbatim text to add even once someone has access, only a description of scope.

What can be said at that level, without a confirmed source, and to be checked
before being relied on in a report:

- Working title along the lines of "Cybersecurity, privacy and AI — Guidance for
  addressing security threats and failures in artificial intelligence systems" —
  treat the exact wording as unconfirmed.
- Developed by ISO/IEC JTC 1/SC 27, the same subcommittee behind ISO/IEC 42001 and
  ISO/IEC 23894 (AI risk management) — positioned as security-specific guidance in
  that family, closer in intent to the OWASP LLM Top 10 above than to 42001's
  management-system scope.
- Development stage and target publication date not confirmed as current — check
  the ISO catalogue directly, or paste project-page metadata into the
  conversation, before citing either.

**Do not add a `norms:` citation to any criterion in `criteria.md` for
this standard until the above is confirmed against a real source.** A `norms:`
citation implies something a report can point to and a client can check; nothing
here is checkable yet. Once the text — or at minimum a confirmed clause structure
— is available, treat it exactly like the other ISO entries above: control-title
mapping in this file, never verbatim, footnoted in the report as a secondary
reference like the rest of this group.

## ISO/IEC 27017 and 27701

- **27017** — cloud-specific guidance on top of 27002, relevant where the sourcing is
  SaaS or a hosted API.
- **27701** — privacy information management, the bridge between 27001 and the GDPR.
  Relevant where personal data is in scope and a certification goal exists.

## NIST AI RMF 1.0

A voluntary framework, not certifiable, organised in four functions: **Govern, Map,
Measure, Manage**. Useful as a vocabulary for structuring an AI governance programme,
and as a cross-reference where a US parent company already uses it.

**Not in the coverage chart, and no criterion cites it.** The RMF is a process
framework in four functions, not a list of threats — citing a function as if it were
an attack path is a category error, and a coverage bar over one citation says nothing.
For threats, `criteria.md` uses the OWASP categories, reported by name.

**Assessment note.** Never report a NIST gap as an obligation. Its one durable value
here is the observation that **"Measure" is the function most policies have nothing
under** — no metrics, no evaluation, no review trigger. That belongs in a governance
finding as a sentence, not as a bar.

## OWASP LLM Top 10 (2026)

A community-maintained list of the most common weaknesses in LLM applications. Not a
norm, and nothing follows from a gap in law. It earns its place because it is the only
one of these references written from the attacker's side.

> **Verified 2026-08-06, and a renumbering, not just a verification.** The 2026
> edition (OWASP GenAI Security Project) was pasted in by the user and compared
> line by line — network access to `genai.owasp.org` is still blocked from this
> environment, so this was not fetched by the skill itself. Every category
> moved or was renamed relative to the 2025 edition this table previously
> carried (below), and the catalog's five `OWASP LLMnn` citations were written
> against the **old** 2025 numbers. Left alone, those citations would now point
> silently at the wrong risk once this table changed — this is a correctness
> fix, not just an addition. Verified: **LLM01** (Prompt Injection), **LLM03**
> (Excessive Agency), **LLM05** (Data and Model Poisoning), **LLM06**
> (Unbounded Consumption, which folds in model extraction/theft), and **LLM10**
> (Improper Output Handling) — see
> [Verbatim text](#owasp-llm-top-10-verbatim-text) below. The other five
> categories (LLM02, LLM04, LLM07, LLM08, LLM09) are described here from the
> pasted text but carry no catalog citation to verify against, so treat their
> table entries as paraphrase like the rest of this file.

| ID (2026) | Weakness | ID (2025) |
|---|---|---|
| LLM01 | Prompt Injection | LLM01 (unchanged) |
| LLM02 | Sensitive Information Disclosure | LLM02 (unchanged) |
| LLM03 | Excessive Agency | was LLM06 |
| LLM04 | Supply Chain | was LLM03 ("supply chain vulnerabilities") |
| LLM05 | Data and Model Poisoning | was LLM04 |
| LLM06 | Unbounded Consumption (now includes model extraction/theft) | was LLM10 |
| LLM07 | Misinformation | was LLM09 |
| LLM08 | Hidden Context Exposure (renamed and broadened from "System Prompt Leakage") | was LLM07 |
| LLM09 | Vector and Embedding Weaknesses | LLM08 (unchanged number in substance, shifted by the list) |
| LLM10 | Improper Output Handling | was LLM05 |

**Which criteria cite which category.** `criteria.md` carries three OWASP
citations, all against the 2026 numbers in the table above: `USE-01` → **LLM01**
(prompt injection), `INFRA-03` → **LLM05** (data and model poisoning), `USE-09` →
**LLM10** (improper output handling). The verbatim text below additionally covers
**LLM03** and **LLM06**, which no criterion currently cites — kept because they are
already checked and because an agentic profile makes them the obvious next
additions.

**Read the 2025 column before importing any older mapping.** Every category moved
or was renamed between the 2025 and 2026 editions, so a citation carried over from
an older document points at the wrong risk unless it is translated through that
table.

**Assessment note.** LLM01 and LLM03 are the two that matter most for an agentic
setup, and the two that policies address least: indirect prompt injection through
ingested content, and an agent holding more authority than the task needs. Where the
intake reports write or transact actions, these stop being theoretical.

### OWASP LLM Top 10 verbatim text

Pasted from the official 2026 text and checked against the five categories the
catalog cites. Quotes are excerpts — the defining sentence(s) of each entry's
Description, not the full entry.

**LLM01:2026 Prompt Injection**

verbatim:
> "A prompt-injection vulnerability occurs when input to a large language model
> (LLM), whether direct user input, retrieved content, tool output, image,
> audio, or video content, intermediate reasoning, or persistent memory,
> alters the model's behavior in ways the application developer did not
> intend. LLMs make no architectural distinction between 'instructions' and
> 'data' (both are tokens on the same stream), so there is no clean equivalent
> to parameterized queries (NCSC, 2025)."

**LLM03:2026 Excessive Agency**

verbatim:
> "Excessive Agency is the vulnerability that enables damaging actions to be
> performed in response to unexpected, ambiguous or manipulated outputs from
> an LLM, regardless of what is causing the LLM to malfunction. […] The root
> cause of Excessive Agency is typically one or more of: excessive
> functionality, excessive permissions, excessive autonomy."

**LLM05:2026 Data and Model Poisoning**

verbatim:
> "Data and Model Poisoning describes a class of attacks and failures where an
> adversary (or unsafe process) manipulates data or model artifacts to embed
> harmful behavior, bias, or exploitable weaknesses into an AI system. […] Data
> poisoning occurs when pre-training, fine-tuning, or embedding data is
> tampered with to introduce vulnerabilities, backdoors, or biases."

**LLM06:2026 Unbounded Consumption (including model extraction and theft)**

verbatim:
> "Unbounded Consumption occurs when an LLM application allows excessive and
> uncontrolled inferences, enabling attackers to disrupt service availability,
> inflict unsustainable financial costs, or steal intellectual property
> through model cloning, all by exploiting a common class of vulnerability:
> the absence of adequate controls over how resources are consumed." […]
> "Model Extraction and Distillation Theft: Attackers query the model API with
> crafted inputs to collect sufficient outputs to replicate a partial model or
> fine-tune a functional equivalent."

**LLM10:2026 Improper Output Handling**

verbatim:
> "Improper Output Handling refers specifically to insufficient validation,
> sanitization, and handling of the outputs generated by large language
> models before they are passed downstream to other components and systems."
