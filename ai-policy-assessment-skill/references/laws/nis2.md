# NIS2 — Directive (EU) 2022/2555

> **Verified 2026-08-06.** The 7 articles in the table below, plus Art. 2 (added
> to [Verbatim text](#verbatim-text) to check the size-threshold mechanism even
> though it isn't a catalog citation), were checked against the official text (OJ
> L 333, 27.12.2022), pasted in by the user and compared line by line — network
> access to `eur-lex.europa.eu` is still blocked from this environment, so this
> was not fetched by the skill itself. All article numbers were confirmed
> correct, and the Annex I/II sector lists in this file's Applicability section
> matched the pasted text exactly. One finding: **the numeric size thresholds in
> this file (50 staff, EUR 10m turnover, 250 staff, EUR 50m) are not themselves in
> the Directive's text.** Art. 2(1) only references "medium-sized enterprises
> under Article 2 of the Annex to Recommendation 2003/361/EC" — the actual
> figures live in that separate Recommendation, which has not been pasted here.
> Confirming the reference mechanism is not the same as confirming the numbers;
> treat those specific figures as still unverified pending that other text.
>
> Official text: `https://eur-lex.europa.eu/eli/dir/2022/2555/oj`

**A directive, not a regulation.** It binds through national transposition, so the
operative text is the national act, not the directive. The transposition status
differs by member state and moves; where it matters for a finding, say which national
act you are relying on and flag that the status should be confirmed.

| State | Transposing act |
|---|---|
| Germany | NIS2UmsuCG, amending the BSIG |
| Austria | NISG |

## Applicability — the part the intake decides

Two gates, both of which have to be crossed:

1. **Sector** — Annex I (energy, transport, banking, financial market
   infrastructure, health, drinking water, waste water, digital infrastructure, ICT
   service management, public administration, space) or Annex II (postal services,
   waste management, chemicals, food, manufacturing including machinery and
   equipment, digital providers, research).
2. **Size** — medium-sized from 50 staff or EUR 10m turnover and balance sheet;
   large from 250 staff or EUR 50m turnover. Below that, generally out of scope,
   with exceptions for critical providers regardless of size.

Manufacturing sits in Annex II, which is why a mechanical engineering group above the
size threshold is usually in scope — and why the intake asks for staff count and
sector separately. Where the sector assignment is genuinely open, the report says
"applicability to be checked" rather than asserting either answer.

## Articles the criteria catalog cites

| Article | Substance | Where it bites in an AI policy |
|---|---|---|
| **Art. 20** | management bodies approve the risk-management measures and oversee their implementation; members are trained | AI governance without a named accountable body fails here, and the liability is personal |
| **Art. 21** | ten minimum measures: risk analysis and information security policy, incident handling, business continuity, **supply chain security**, security in acquisition and development, procedures to assess effectiveness, cyber hygiene and training, cryptography, access control and asset management, multi-factor authentication | the supply chain measure is the one AI procurement runs into: a model provider is a supplier |
| **Art. 23** | incident reporting: early warning within 24 hours, notification within 72 hours, final report within one month | an AI-specific incident path that does not connect to this timetable is a separate process that will miss the deadline |
| **Art. 24** | certification schemes may be required | relevant only where a scheme is named |
| **Art. 32 · 33** | supervisory measures, including binding instructions and, for essential entities, temporary suspension of management functions | the enforcement side of Art. 20 |
| **Art. 34** | fines up to EUR 10m or 2% of worldwide turnover for essential entities, EUR 7m or 1.4% for important entities | the number that turns Art. 20's personal accountability from a governance nicety into exposure |

## What this means for the assessment

1. **NIS2 is what makes AI governance a management duty rather than an IT topic.**
   Art. 20 is the reference for the governance criteria — approval, oversight,
   training — and it is the one that carries personal liability.
2. **The supply chain measure covers model providers.** A policy that governs
   internal use but says nothing about assessing the provider has a gap under
   Art. 21, not merely a procurement inconvenience.
3. **Do not build a second incident process.** Where a policy defines AI incident
   handling without reference to the existing NIS2 reporting path, the finding is
   about the connection, not about the absence of a process.
4. **Where applicability is open, say so once and move on.** An unresolved sector
   assignment is a note in the legal frame, not a finding repeated across ten
   criteria.
5. **The size thresholds are a separate-instrument question.** Where a client's
   in-scope status turns on the exact staff/turnover numbers rather than on the
   sector or on obvious scale, say that the numbers themselves rest on
   Recommendation 2003/361/EC, not on NIS2's own text, and that this file has not
   verified that Recommendation.

## Verbatim text

Pasted from the official text and checked against the article numbers above.
Quotes are excerpts — the operative sentence(s) behind the citation, not the full
article.

**Art. 2(1) — Scope, the size-cap reference**

verbatim:
> "This Directive applies to public or private entities of a type referred to in
> Annex I or II which qualify as medium-sized enterprises under Article 2 of the
> Annex to Recommendation 2003/361/EC, or exceed the ceilings for medium-sized
> enterprises provided for in paragraph 1 of that Article, and which provide
> their services or carry out their activities within the Union."

**Art. 20(1) — Governance**

verbatim:
> "Member States shall ensure that the management bodies of essential and
> important entities approve the cybersecurity risk-management measures taken by
> those entities in order to comply with Article 21, oversee its implementation
> and can be held liable for infringements by the entities of that Article."

**Art. 21(1)-(2) — Cybersecurity risk-management measures**

verbatim:
> "Member States shall ensure that essential and important entities take
> appropriate and proportionate technical, operational and organisational
> measures to manage the risks posed to the security of network and information
> systems […] The measures […] shall be based on an all-hazards approach […] and
> shall include at least the following: (a) policies on risk analysis and
> information system security; (b) incident handling; (c) business continuity
> […]; (d) supply chain security, including security-related aspects concerning
> the relationships between each entity and its direct suppliers or service
> providers […]"

**Art. 23(1) and (4) — Reporting obligations**

verbatim:
> "Each Member State shall ensure that essential and important entities notify,
> without undue delay, its CSIRT or, where applicable, its competent authority
> […] of any incident that has a significant impact on the provision of their
> services […] (significant incident)." […] "(a) without undue delay and in any
> event within 24 hours of becoming aware of the significant incident, an early
> warning […]; (b) without undue delay and in any event within 72 hours of
> becoming aware of the significant incident, an incident notification […]; (d)
> a final report not later than one month after the submission of the incident
> notification under point (b) […]"

**Art. 24(1) — Use of European cybersecurity certification schemes**

verbatim:
> "In order to demonstrate compliance with particular requirements of Article 21,
> Member States may require essential and important entities to use particular
> ICT products, ICT services and ICT processes […] that are certified under
> European cybersecurity certification schemes adopted pursuant to Article 49 of
> Regulation (EU) 2019/881."

**Art. 32(5) — Enforcement, essential entities**

verbatim:
> "Member States shall ensure that their competent authorities have the power
> to: (a) suspend temporarily […] a certification or authorisation concerning
> part or all of the relevant services provided or activities carried out by the
> essential entity; (b) request that the relevant bodies, courts or tribunals […]
> prohibit temporarily any natural person who is responsible for discharging
> managerial responsibilities at chief executive officer or legal representative
> level in the essential entity from exercising managerial functions in that
> entity."

**Art. 33(1) — Enforcement, important entities**

verbatim:
> "When provided with evidence, indication or information that an important
> entity allegedly does not comply with this Directive, in particular Articles 21
> and 23 thereof, Member States shall ensure that the competent authorities take
> action, where necessary, through ex post supervisory measures."

**Art. 34(4) — Administrative fines**

verbatim:
> "Member States shall ensure that where they infringe Article 21 or 23,
> essential entities are subject […] to administrative fines of a maximum of at
> least EUR 10 000 000 or of a maximum of at least 2 % of the total worldwide
> annual turnover in the preceding financial year of the undertaking to which the
> essential entity belongs, whichever is higher."
