# Sector-specific acts — DORA, CRA, MDR

> **Paraphrase, not wording.** Article numbers and substance are the working
> reference; the text is a summary, never a quote. Official sources are linked per
> act; none is stored verbatim, because the environment's network policy blocks
> `eur-lex.europa.eu`.

Read only the section that the intake activates. For most profiles this whole file
stays closed.

---

## DORA — Regulation (EU) 2022/2554

> **Verified 2026-08-06.** The articles behind every row in the table below —
> Art. 6, 19, 24, 26, 28, 30, 31 — were checked against the official text (OJ L
> 333, 27.12.2022), pasted in by the user and compared line by line — network
> access to `eur-lex.europa.eu` is still blocked from this environment, so this
> was not fetched by the skill itself. The two articles the catalog actually
> cites (Art. 19, Art. 28) were confirmed correct; the others were added because
> this file's table already described them, not because the catalog cites them —
> see [Verbatim text](#dora-verbatim-text) below. The applicability date (17
> January 2025) was confirmed against Art. 64.

Official text: `https://eur-lex.europa.eu/eli/reg/2022/2554/oj`
Applies from **17 January 2025** to financial entities: banks, insurers, investment
firms, payment institutions, crypto-asset service providers, and others.

| Area | Substance | Where it bites in an AI policy |
|---|---|---|
| ICT risk management | a framework covering the full ICT estate | an AI system is ICT; a separate AI governance track that does not connect to it creates two frameworks and one gap |
| **Third-party risk** | contractual requirements, a register of information on all ICT third-party arrangements, exit strategies | a model provider is an ICT third party. The register is the item most often missing |
| Critical providers | tighter regime for providers designated critical | relevant for large cloud and model providers |
| Incident reporting | classification and reporting of major ICT-related incidents | same point as NIS2: one path, not two |
| Resilience testing | including threat-led penetration testing for significant entities | prompt injection testing belongs in this programme, not beside it |

**Assessment note.** For a financial entity, the concentration risk criterion stops
being good practice and becomes a supervisory expectation. The exit strategy is the
question a supervisor asks first and a policy answers least often.

### DORA verbatim text

Pasted from the official text and checked against the articles named above. Quotes
are excerpts — the operative sentence(s) behind each table row, not the full
article.

**Art. 6(1) — ICT risk management framework**

verbatim:
> "Financial entities shall have a sound, comprehensive and well-documented ICT
> risk management framework as part of their overall risk management system,
> which enables them to address ICT risk quickly, efficiently and
> comprehensively and to ensure a high level of digital operational
> resilience."

**Art. 19(1) — Reporting of major ICT-related incidents**

verbatim:
> "Financial entities shall report major ICT-related incidents to the relevant
> competent authority as referred to in Article 46 in accordance with paragraph
> 4 of this Article."

**Art. 24(1) — Digital operational resilience testing**

verbatim:
> "financial entities, other than microenterprises, shall, taking into account
> the criteria set out in Article 4(2), establish, maintain and review a sound
> and comprehensive digital operational resilience testing programme as an
> integral part of the ICT risk-management framework referred to in Article 6."

**Art. 26(1) — Threat-led penetration testing**

verbatim:
> "Financial entities, other than entities referred to in Article 16(1), first
> subparagraph, and other than microenterprises, which are identified in
> accordance with paragraph 8, third subparagraph, of this Article, shall carry
> out at least every 3 years advanced testing by means of TLPT."

**Art. 28(1), (3) and (8) — ICT third-party risk, register, exit strategies**

verbatim:
> "Financial entities shall manage ICT third-party risk as an integral
> component of ICT risk within their ICT risk management framework as referred
> to in Article 6(1) […] financial entities that have in place contractual
> arrangements for the use of ICT services to run their business operations
> shall, at all times, remain fully responsible for compliance with, and the
> discharge of, all obligations under this Regulation […]" […] "financial
> entities shall maintain and update at entity level, and at sub-consolidated
> and consolidated levels, a register of information in relation to all
> contractual arrangements on the use of ICT services provided by ICT
> third-party service providers." […] "For ICT services supporting critical or
> important functions, financial entities shall put in place exit strategies."

**Art. 30(1) — Key contractual provisions**

verbatim:
> "The rights and obligations of the financial entity and of the ICT
> third-party service provider shall be clearly allocated and set out in
> writing."

**Art. 31(1)(a) — Designation of critical ICT third-party service providers**

verbatim:
> "The ESAs, through the Joint Committee and upon recommendation from the
> Oversight Forum established pursuant to Article 32(1), shall: (a) designate
> the ICT third-party service providers that are critical for financial
> entities, following an assessment that takes into account the criteria
> specified in paragraph 2[…]"

---

## CRA — Cyber Resilience Act, Regulation (EU) 2024/2847

> **Verified 2026-08-06.** The provisions behind every row in the table below —
> Annex I Part I (essential requirements), Annex I Part II (vulnerability
> handling), Art. 13(8) (support period), Art. 14 (reporting) — were checked
> against the official text (OJ L, 2024/2847, 20.11.2024), pasted in by the user
> and compared line by line — network access to `eur-lex.europa.eu` is still
> blocked from this environment, so this was not fetched by the skill itself.
> The catalog cites only the bare acronym `CRA`, no specific article, so this
> verification covers what this table already described rather than closing a
> catalog gap — see [Verbatim text](#cra-verbatim-text) below. The three
> applicability dates were confirmed against Art. 71: the main obligations from
> 11 December 2027, Art. 14 (reporting) from 11 September 2026, and — not
> previously noted in this file — Chapter IV (notification of conformity
> assessment bodies, Art. 35–51) from 11 June 2026.

Official text: `https://eur-lex.europa.eu/eli/reg/2024/2847/oj`
Applies to **products with digital elements** placed on the EU market. Reporting
obligations from **11 September 2026**, the main obligations from **11 December 2027**.

| Area | Substance | Where it bites in an AI policy |
|---|---|---|
| Essential requirements | security by design and by default, secure configuration, no known exploitable vulnerabilities at release | where the company ships software or connected products, an AI feature inside them inherits this |
| Vulnerability handling | coordinated disclosure, an SBOM, security updates for the support period | a model integrated into a shipped product becomes a component to be tracked |
| Reporting | actively exploited vulnerabilities and severe incidents reported to ENISA and the national CSIRT | a short clock, and a separate AI incident path will miss it |

**Assessment note.** Activate where `profile.role` is provider or both **and** the
company ships products. A company that only uses AI internally is out of scope. Where
it does ship, the AI policy and the product security process have to reference each
other, and usually do not.

### CRA verbatim text

Pasted from the official text and checked against the provisions named above.
Quotes are excerpts — the operative sentence(s) behind each table row, not the
full annex or article.

**Annex I, Part I, points 1 and 2(a)-(b) — Essential requirements**

verbatim:
> "Products with digital elements shall be designed, developed and produced in
> such a way that they ensure an appropriate level of cybersecurity based on
> the risks." […] products with digital elements shall: "(a) be made available
> on the market without known exploitable vulnerabilities; (b) be made
> available on the market with a secure by default configuration, unless
> otherwise agreed between manufacturer and business user in relation to a
> tailor-made product with digital elements, including the possibility to
> reset the product to its original state[…]"

**Annex I, Part II, points 1, 5 and 8 — Vulnerability handling**

verbatim:
> "identify and document vulnerabilities and components contained in products
> with digital elements, including by drawing up a software bill of materials
> in a commonly used and machine-readable format covering at the very least
> the top-level dependencies of the products[…]" […] "put in place and enforce
> a policy on coordinated vulnerability disclosure[…]" […] "ensure that, where
> security updates are available to address identified security issues, they
> are disseminated without delay and […] free of charge, accompanied by
> advisory messages providing users with the relevant information, including
> on potential action to be taken."

**Art. 13(8), third subparagraph — Support period**

verbatim:
> "Without prejudice to the second subparagraph, the support period shall be
> at least five years. Where the product with digital elements is expected to
> be in use for less than five years, the support period shall correspond to
> the expected use time."

**Art. 14(1) and (3) — Reporting obligations**

verbatim:
> "A manufacturer shall notify any actively exploited vulnerability contained
> in the product with digital elements that it becomes aware of simultaneously
> to the CSIRT designated as coordinator […] and to ENISA." […] "A
> manufacturer shall notify any severe incident having an impact on the
> security of the product with digital elements that it becomes aware of
> simultaneously to the CSIRT designated as coordinator […] and to ENISA."

---

## MDR — Regulation (EU) 2017/745

> **Verified 2026-08-06.** The provisions behind every row in the table below —
> Annex I §17.2 and §17.4 (software lifecycle and IT security), Annex VIII §6.3
> Rule 11 (classification), Art. 61(1) (clinical evaluation), Art. 83(1) and
> Art. 87(1) (post-market surveillance and vigilance reporting) — were checked
> against the official text (OJ L 117, 5.5.2017), pasted in by the user and
> compared line by line — network access to `eur-lex.europa.eu` is still
> blocked from this environment, so this was not fetched by the skill itself.
> The catalog cites only the bare acronym `MDR`, no specific article, so this
> verification covers what this table already described rather than closing a
> catalog gap — see [Verbatim text](#mdr-verbatim-text) below. This completes
> verification of all three acts in this file: DORA, CRA and MDR.

Official text: `https://eur-lex.europa.eu/eli/reg/2017/745/oj`
Applies to medical devices, including **software as a medical device**.

| Area | Substance |
|---|---|
| Annex I | general safety and performance requirements, including for software lifecycle and IT security |
| Classification | Annex VIII, **Rule 11** for software — decision-support software reaches class IIa or higher quickly |
| Clinical evaluation | evidence of performance for the intended purpose |
| Post-market surveillance | ongoing monitoring, vigilance reporting |

**Assessment note.** Where a medical device is in scope, the MDR and the AI Act stack:
a high-risk AI system that is also a medical device carries both regimes, and the
conformity assessment runs through the notified body. This is beyond what a policy
review can settle — name it in `alerts` and route it to regulatory affairs. Do not
attempt a classification here.

### MDR verbatim text

Pasted from the official text and checked against the provisions named above.
Quotes are excerpts — the operative sentence(s) behind each table row, not the
full annex or article.

**Annex I, §17.2 and §17.4 — General safety and performance requirements (software lifecycle and IT security)**

verbatim:
> "For devices that incorporate software or for software that are devices in
> themselves, the software shall be developed and manufactured in accordance
> with the state of the art taking into account the principles of development
> life cycle, risk management, including information security, verification
> and validation." […] "Manufacturers shall set out minimum requirements
> concerning hardware, IT networks characteristics and IT security measures,
> including protection against unauthorised access, necessary to run the
> software as intended."

**Annex VIII, §6.3, Rule 11 — Classification of software**

verbatim:
> "Software intended to provide information which is used to take decisions
> with diagnosis or therapeutic purposes is classified as class IIa, except if
> such decisions have an impact that may cause: — death or an irreversible
> deterioration of a person's state of health, in which case it is in class
> III; or — a serious deterioration of a person's state of health or a
> surgical intervention, in which case it is classified as class IIb. […] All
> other software is classified as class I."

**Art. 61(1) — Clinical evaluation**

verbatim:
> "Confirmation of conformity with relevant general safety and performance
> requirements set out in Annex I under the normal conditions of the intended
> use of the device, and the evaluation of the undesirable side-effects and of
> the acceptability of the benefit-risk-ratio referred to in Sections 1 and 8
> of Annex I, shall be based on clinical data providing sufficient clinical
> evidence, including where applicable relevant data as referred to in Annex
> III."

**Art. 83(1) and Art. 87(1) — Post-market surveillance and vigilance reporting**

verbatim:
> "For each device, manufacturers shall plan, establish, document, implement,
> maintain and update a post-market surveillance system in a manner that is
> proportionate to the risk class and appropriate for the type of device."
> […] "Manufacturers of devices made available on the Union market, other
> than investigational devices, shall report, to the relevant competent
> authorities, in accordance with Articles 92(5) and (7), […] any serious
> incident involving devices made available on the Union market […] any field
> safety corrective action in respect of devices made available on the Union
> market[…]"
