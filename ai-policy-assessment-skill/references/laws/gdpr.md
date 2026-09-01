# GDPR — Regulation (EU) 2016/679

> **Verified 2026-08-06.** The 17 articles in the table below and in
> [Verbatim text](#verbatim-text) were checked against the official text (OJ L 119,
> 4.5.2016), pasted in by the user and compared line by line — network access to
> `eur-lex.europa.eu` is still blocked from this environment, so this was not
> fetched by the skill itself. All article numbers were confirmed correct. The same
> check found that this table was missing two articles the catalog cites directly
> (Art. 33, Art. 82) — added below.
>
> Official text: `https://eur-lex.europa.eu/eli/reg/2016/679/oj`

Applies as soon as personal data is processed, which for an AI policy means: nearly
always. Employee data counts. Data in prompts counts. Data in logs counts, and logs
are where policies forget it.

## Articles the criteria catalog cites

| Article | Substance | Where it bites in an AI policy |
|---|---|---|
| **Art. 5** | principles: lawfulness, purpose limitation, data minimisation, accuracy, storage limitation, integrity, accountability | purpose limitation is the one AI use breaks: data collected for order processing is not thereby available for model training |
| **Art. 6** | a legal basis is required for every processing operation | "we use AI for it" is not a legal basis |
| **Art. 9** | special categories — health, biometrics, union membership, and others — prohibited unless an exception applies | health data in a support ticket is Art. 9 data, whatever the ticket system is called |
| **Art. 13 · 14** | information duties towards data subjects | a chatbot that processes customer data needs this, and Art. 50 of the AI Act does not replace it |
| **Art. 15 · 17** | access and erasure | erasure from a fine-tuned model is not resolved by deleting the training file; a policy that promises it is making a promise it cannot keep |
| **Art. 22** | automated individual decisions with legal effect or similar significant effect require a human decision, and the data subject can demand one | this, not the AI Act, is what makes a human decision mandatory in recruiting and credit |
| **Art. 25** | data protection by design and by default | the point at which "we will configure it later" stops being sufficient |
| **Art. 28** | processor duties, in writing | the API provider is a processor; without a contract the processing has no basis |
| **Art. 30** | records of processing activities | a new AI tool is a new processing activity, and the record is where shadow AI becomes visible |
| **Art. 32** | security of processing appropriate to the risk | the anchor for the technical criteria: access control, encryption, tenancy |
| **Art. 33** | notification of a personal data breach to the supervisory authority, in principle within 72 hours | the deadline the incident criterion (`GOV-07`) has to be built around, not a design choice |
| **Art. 35** | data protection impact assessment for high-risk processing | frequently triggered by AI, and frequently the reason a rollout stalls |
| **Art. 44 to 49** | transfers to third countries | the practical question for every US model provider: which mechanism, and is it in the contract |
| **Art. 82** | right to compensation for material or non-material damage from an infringement | the individual's claim, distinct from and additional to the fine in Art. 83 |
| **Art. 83** | fines up to 4% of worldwide annual turnover | the number a management board reacts to |

## What this means for the assessment

1. **Art. 6 and Art. 32 are the pair that carries most latitude findings.** The
   GDPR asks for a legal basis and for protection appropriate to the risk. It
   nowhere requires a blanket ban on personal data in AI systems. A policy that
   writes one has made a decision — a defensible one, but a decision — and the
   latitude section says so with these two articles as the reference.
2. **Art. 22 is a hard floor, not latitude.** Where an automated decision has legal
   or similarly significant effect, a human decides. Where a policy mandates that,
   it is meeting a duty, and the report must not read it as over-strictness.
3. **Art. 9 changes the answer, not just the paperwork.** Where the intake reports
   special categories, criteria that would otherwise be design questions become
   duties. The activation conditions in the catalog do this automatically; the
   report should still say why.
4. **Logs are processing.** Art. 5 storage limitation and Art. 32 apply to the audit
   trail an AI policy mandates. A policy that requires audit-proof logging of all
   interactions without a retention period has created a data protection problem
   while solving a governance one.
5. **Art. 33's 72 hours is a deadline, not an aspiration.** An AI incident that
   exposes personal data is a data breach under Art. 33 regardless of whether it is
   also an AI Act incident under Art. 73. Where a policy's escalation path cannot
   plausibly notify the supervisory authority inside 72 hours of becoming aware, the
   duty is unmet, not merely under-resourced.

## Verbatim text

Pasted from the official text and checked against the article numbers above. Quotes
are excerpts — the operative sentence(s) behind the citation, not the full article.

**Art. 5(1)(b) — Purpose limitation**

verbatim:
> "collected for specified, explicit and legitimate purposes and not further
> processed in a manner that is incompatible with those purposes […] ('purpose
> limitation')"

**Art. 5(2) — Accountability**

verbatim:
> "The controller shall be responsible for, and be able to demonstrate compliance
> with, paragraph 1 ('accountability')."

**Art. 6(1) — Lawfulness of processing**

verbatim:
> "Processing shall be lawful only if and to the extent that at least one of the
> following applies: (a) the data subject has given consent […]; (b) processing is
> necessary for the performance of a contract […]; (c) processing is necessary for
> compliance with a legal obligation […]"

**Art. 9(1) — Special categories**

verbatim:
> "Processing of personal data revealing racial or ethnic origin, political
> opinions, religious or philosophical beliefs, or trade union membership, and the
> processing of genetic data, biometric data for the purpose of uniquely
> identifying a natural person, data concerning health or data concerning a natural
> person's sex life or sexual orientation shall be prohibited."

**Art. 13(1) — Information duty, data collected from the subject**

verbatim:
> "Where personal data relating to a data subject are collected from the data
> subject, the controller shall, at the time when personal data are obtained,
> provide the data subject with all of the following information: (a) the identity
> and the contact details of the controller […]"

**Art. 14(1) — Information duty, data not obtained from the subject**

verbatim:
> "Where personal data have not been obtained from the data subject, the controller
> shall provide the data subject with the following information: (a) the identity
> and the contact details of the controller […]"

**Art. 15(1) — Right of access**

verbatim:
> "The data subject shall have the right to obtain from the controller confirmation
> as to whether or not personal data concerning him or her are being processed,
> and, where that is the case, access to the personal data and the following
> information […]"

**Art. 17(1) — Right to erasure**

verbatim:
> "The data subject shall have the right to obtain from the controller the erasure
> of personal data concerning him or her without undue delay and the controller
> shall have the obligation to erase personal data without undue delay where one of
> the following grounds applies […]"

**Art. 22(1) — Automated individual decision-making**

verbatim:
> "The data subject shall have the right not to be subject to a decision based
> solely on automated processing, including profiling, which produces legal
> effects concerning him or her or similarly significantly affects him or her."

**Art. 25(1) — Data protection by design**

verbatim:
> "the controller shall, both at the time of the determination of the means for
> processing and at the time of the processing itself, implement appropriate
> technical and organisational measures, such as pseudonymisation, which are
> designed to implement data-protection principles, such as data minimisation, in
> an effective manner and to integrate the necessary safeguards into the
> processing"

**Art. 28(3) — Processor contract**

verbatim:
> "Processing by a processor shall be governed by a contract or other legal act
> under Union or Member State law, that is binding on the processor with regard to
> the controller and that sets out the subject-matter and duration of the
> processing, the nature and purpose of the processing, the type of personal data
> and categories of data subjects and the obligations and rights of the
> controller."

**Art. 30(1) — Records of processing activities**

verbatim:
> "Each controller and, where applicable, the controller's representative, shall
> maintain a record of processing activities under its responsibility."

**Art. 32(1) — Security of processing**

verbatim:
> "the controller and the processor shall implement appropriate technical and
> organisational measures to ensure a level of security appropriate to the risk,
> including inter alia as appropriate: (a) the pseudonymisation and encryption of
> personal data; (b) the ability to ensure the ongoing confidentiality, integrity,
> availability and resilience of processing systems and services […]"

**Art. 33(1) — Breach notification to the supervisory authority**

verbatim:
> "In the case of a personal data breach, the controller shall without undue delay
> and, where feasible, not later than 72 hours after having become aware of it,
> notify the personal data breach to the supervisory authority […] unless the
> personal data breach is unlikely to result in a risk to the rights and freedoms
> of natural persons."

**Art. 35(1) — Data protection impact assessment**

verbatim:
> "Where a type of processing in particular using new technologies, and taking
> into account the nature, scope, context and purposes of the processing, is
> likely to result in a high risk to the rights and freedoms of natural persons,
> the controller shall, prior to the processing, carry out an assessment of the
> impact of the envisaged processing operations on the protection of personal
> data."

**Art. 44 — General principle for transfers**

verbatim:
> "Any transfer of personal data which are undergoing processing or are intended
> for processing after transfer to a third country or to an international
> organisation shall take place only if, subject to the other provisions of this
> Regulation, the conditions laid down in this Chapter are complied with by the
> controller and processor […]"

**Art. 82(1) — Right to compensation**

verbatim:
> "Any person who has suffered material or non-material damage as a result of an
> infringement of this Regulation shall have the right to receive compensation
> from the controller or processor for the damage suffered."

**Art. 83(5) — Administrative fines, upper tier**

verbatim:
> "Infringements of the following provisions shall, in accordance with paragraph 2,
> be subject to administrative fines up to 20 000 000 EUR, or in the case of an
> undertaking, up to 4 % of the total worldwide annual turnover of the preceding
> financial year, whichever is higher: (a) the basic principles for processing,
> including conditions for consent, pursuant to Articles 5, 6, 7 and 9 […]"
