# EU AI Act — Regulation (EU) 2024/1689

> **Verified 2026-08-06.** The 24 articles in the table below and in
> [Verbatim text](#verbatim-text) were checked against the official consolidated
> text (OJ L, 2024/1689, 12.7.2024), pasted in by the user and compared line by
> line — network access to `eur-lex.europa.eu` is still blocked from this
> environment, so this was not fetched by the skill itself. All article numbers
> were confirmed correct, including the two paragraph numbers this file had
> flagged as at risk of trilogue-era renumbering (Art. 26(6), Art. 26(7)) — neither
> had shifted. The same check found that this table was missing six articles the
> catalog cites directly (Art. 3, 16, 19, 49, 72, 73) — added below, alongside a
> real distinction between Art. 12 (the system's logging *capability*), Art. 19
> (the provider's log *retention* duty) and Art. 26(6) (the deployer's mirror of
> that retention duty), which an earlier version of this file had run together.
>
> Everything in the tables below this notice is still paraphrase, not wording — the
> **substance** and **applies to** columns are summaries. Only the blocks under
> [Verbatim text](#verbatim-text) are the Act's actual wording. Any article number
> **not** in that list (elsewhere in this file, or a future addition) is unverified
> until it gets the same treatment.
>
> Official text: `https://eur-lex.europa.eu/eli/reg/2024/1689/oj`

## Who the Act speaks to

The obligations differ by role, and the role is the first thing the intake settles
(`profile.role`). Getting this wrong invalidates most of the assessment.

| Role | Meaning | Weight of obligations |
|---|---|---|
| **Deployer** (`deployer`) | uses an AI system under its own authority | moderate — Art. 26, plus Art. 4 and Art. 50 |
| **Provider** (`provider`) | develops a system, or puts one on the market under its own name | heavy — Art. 9 to Art. 17 for high risk |
| **Both** (`both`) | e.g. fine-tunes a model and ships it to customers | provider obligations apply |

A deployer becomes a provider by putting its name on a system, by substantially
modifying one, or by changing the intended purpose of a high-risk system (Art. 25).
Fine-tuning a model and shipping the result to customers is the common trigger in
practice, and the one most often missed.

## Risk classes

| Class | Where it comes from | Consequence |
|---|---|---|
| **Prohibited** | Art. 5 | not permissible at all — social scoring, emotion recognition at the workplace and in education, untargeted scraping of facial images, and others |
| **High risk** | Art. 6 with Annex I (product safety) and Annex III (use cases) | the full obligation set, Art. 9 to Art. 15 for providers, Art. 26 for deployers |
| **Transparency** | Art. 50 | disclosure duties: a chatbot says it is one, synthetic content is marked, deepfakes are labelled |
| **GPAI** | Art. 53, Art. 55 | model providers: documentation, copyright policy, training-data summary; with systemic risk, more |
| Everything else | — | no obligations under the Act; other law still applies |

**Annex III no. 4 is the one that catches ordinary companies:** employment and
worker management, including recruitment and applicant selection, decisions on
promotion and termination, task allocation, and monitoring or evaluation of
performance. Pre-screening job applications with AI falls under it. This is why the
intake asks about applicant screening (`profile.usecase_flags`).

Annex III also covers education, access to essential services, credit scoring,
insurance pricing, law enforcement, migration, and administration of justice.

## Articles relevant to the assessment

**This table is a summary of the Act, not of `criteria.md`.** It deliberately
covers more articles than the criteria cite, so a duty can be looked up here even
where no criterion carries it. Where the two diverge, the catalog's `norms:` field
is the one that actually drives a finding.

| Article | Substance | Applies to |
|---|---|---|
| **Art. 3** | definitions, in particular 'provider' and 'deployer' | everyone — the definitions decide which duties attach |
| **Art. 4** | staff and operators have sufficient AI literacy for their role | everyone, provider and deployer alike |
| **Art. 5** | prohibited practices | everyone |
| **Art. 6 · Annex III** | classification as high risk | everyone — the classification itself is the duty |
| **Art. 9** | risk management system across the lifecycle | providers, high risk |
| **Art. 10** | data and data governance: training, validation and test data quality | providers, high risk |
| **Art. 11 · Annex IV** | technical documentation | providers, high risk |
| **Art. 12** | the system must technically allow automatic recording of events (logs) | providers, high risk — a capability duty, not a retention duty |
| **Art. 13** | transparency and information for deployers | providers, high risk |
| **Art. 14** | human oversight: a natural person can understand, monitor, override and stop the system | providers, high risk |
| **Art. 15** | accuracy, robustness and cybersecurity | providers, high risk |
| **Art. 16** | the provider's full obligation list (a)–(l) — compliance, documentation, CE marking, registration, corrective action, and more | providers, high risk — the catch-all article the specific duties hang off |
| **Art. 17** | quality management system | providers, high risk |
| **Art. 19** | keep the logs the system generates, at least six months | providers, high risk — the retention duty paired with Art. 12's capability duty |
| **Art. 25** — *Responsibilities along the AI value chain* | when a deployer becomes a provider | deployers |
| **Art. 26** | deployer duties: use per instructions, assign competent human oversight, monitor operation | deployers, high risk |
| **Art. 26(6)** | keep the logs the system generates, for an appropriate period, at least six months | deployers, high risk — the deployer-side mirror of Art. 19 |
| **Art. 26(7)** | inform workers' representatives and affected workers before putting a high-risk system into use at the workplace | deployers who are employers |
| **Art. 27** | fundamental rights impact assessment | public bodies and certain private deployers, high risk |
| **Art. 49** | register the system in the EU database before placing on the market or putting into service | providers of Annex III high-risk systems |
| **Art. 50** | transparency for systems interacting with people, and marking of synthetic content | providers and deployers |
| **Art. 53** | GPAI model providers: technical documentation, copyright policy, training content summary | model providers |
| **Art. 55** | additional duties for GPAI models with systemic risk | model providers |
| **Art. 72** | post-market monitoring system, collecting performance data throughout the system's lifetime | providers, high risk |
| **Art. 73** | reporting a serious incident to the market surveillance authority, within 15 days as the general rule | providers, high risk |
| **Art. 99** | penalties | everyone |

## Verbatim text

The operative sentence for each cited article, not the whole article — a full quote
would include sub-clauses no criterion here relies on. Quoted from Regulation (EU)
2024/1689 (OJ L, 2024/1689, 12.7.2024), pasted in and checked 2026-08-06.

**Art. 4 — AI literacy**

verbatim:
> "Providers and deployers of AI systems shall take measures to ensure, to their
> best extent, a sufficient level of AI literacy of their staff and other persons
> dealing with the operation and use of AI systems on their behalf, taking into
> account their technical knowledge, experience, education and training and the
> context the AI systems are to be used in, and considering the persons or groups
> of persons on whom the AI systems are to be used."

**Art. 3, points (3) and (4) — Definitions of 'provider' and 'deployer'**

verbatim:
> "'provider' means a natural or legal person, public authority, agency or other
> body that develops an AI system or a general-purpose AI model or that has an AI
> system or a general-purpose AI model developed and places it on the market or
> puts the AI system into service under its own name or trademark, whether for
> payment or free of charge; [...] 'deployer' means a natural or legal person,
> public authority, agency or other body using an AI system under its authority
> except where the AI system is used in the course of a personal non-professional
> activity."

**Art. 5(1) — Prohibited AI practices**

verbatim:
> "The following AI practices shall be prohibited: (a) the placing on the market,
> the putting into service or the use of an AI system that deploys subliminal
> techniques beyond a person's consciousness or purposefully manipulative or
> deceptive techniques [...] (b) [...] that exploits any of the vulnerabilities of
> a natural person or a specific group of persons due to their age, disability or a
> specific social or economic situation [...] (c) [...] AI systems for the
> evaluation or classification of natural persons or groups of persons over a
> certain period of time based on their social behaviour or known, inferred or
> predicted personal or personality characteristics, with the social score leading
> to [...] detrimental or unfavourable treatment [...] (d) [...] for making risk
> assessments of natural persons in order to assess or predict the risk of a
> natural person committing a criminal offence, based solely on the profiling of a
> natural person or on assessing their personality traits and characteristics [...]
> (e) [...] AI systems that create or expand facial recognition databases through
> the untargeted scraping of facial images from the internet or CCTV footage; (f)
> [...] AI systems to infer emotions of a natural person in the areas of workplace
> and education institutions, except where the use [...] is intended [...] for
> medical or safety reasons; (g) [...] biometric categorisation systems that
> categorise individually natural persons based on their biometric data to deduce
> or infer their race, political opinions, trade union membership, religious or
> philosophical beliefs, sex life or sexual orientation [...]; (h) the use of
> 'real-time' remote biometric identification systems in publicly accessible
> spaces for the purposes of law enforcement, unless and in so far as such use is
> strictly necessary for one of the following objectives: (i) the targeted search
> for specific victims [...] (ii) the prevention of a specific, substantial and
> imminent threat to the life or physical safety of natural persons or [...] a
> terrorist attack; (iii) the localisation or identification of a person suspected
> of having committed a criminal offence [...]"

**Art. 6(1)-(2) — Classification rules for high-risk AI systems**

verbatim:
> "Irrespective of whether an AI system is placed on the market or put into
> service independently of the products referred to in points (a) and (b), that AI
> system shall be considered to be high-risk where both of the following
> conditions are fulfilled: (a) the AI system is intended to be used as a safety
> component of a product, or the AI system is itself a product, covered by the
> Union harmonisation legislation listed in Annex I; (b) the product [...] is
> required to undergo a third-party conformity assessment [...]. In addition to
> the high-risk AI systems referred to in paragraph 1, AI systems referred to in
> Annex III shall be considered to be high-risk."

**Art. 9(2) — Risk management system**

verbatim:
> "The risk management system shall be understood as a continuous iterative
> process planned and run throughout the entire lifecycle of a high-risk AI
> system, requiring regular systematic review and updating. It shall comprise the
> following steps: (a) the identification and analysis of the known and the
> reasonably foreseeable risks [...] (b) the estimation and evaluation of the
> risks that may emerge when the high-risk AI system is used in accordance with
> its intended purpose, and under conditions of reasonably foreseeable misuse; (c)
> the evaluation of other risks possibly arising, based on the analysis of data
> gathered from the post-market monitoring system [...]; (d) the adoption of
> appropriate and targeted risk management measures [...]"

**Art. 10(3) — Data and data governance**

verbatim:
> "Training, validation and testing data sets shall be relevant, sufficiently
> representative, and to the best extent possible, free of errors and complete in
> view of the intended purpose."

**Art. 11(1) — Technical documentation**

verbatim:
> "The technical documentation of a high-risk AI system shall be drawn up before
> that system is placed on the market or put into service and shall be kept
> up-to date. The technical documentation shall be drawn up in such a way as to
> demonstrate that the high-risk AI system complies with the requirements set out
> in this Section and to provide national competent authorities and notified
> bodies with the necessary information in a clear and comprehensive form to
> assess the compliance of the AI system with those requirements."

**Art. 12(1) — Record-keeping**

verbatim:
> "High-risk AI systems shall technically allow for the automatic recording of
> events (logs) over the lifetime of the system."

**Art. 13(1) — Transparency and provision of information to deployers**

verbatim:
> "High-risk AI systems shall be designed and developed in such a way as to
> ensure that their operation is sufficiently transparent to enable deployers to
> interpret a system's output and use it appropriately."

**Art. 14(1) — Human oversight**

verbatim:
> "High-risk AI systems shall be designed and developed in such a way, including
> with appropriate human-machine interface tools, that they can be effectively
> overseen by natural persons during the period in which they are in use."

**Art. 15(1) — Accuracy, robustness and cybersecurity**

verbatim:
> "High-risk AI systems shall be designed and developed in such a way that they
> achieve an appropriate level of accuracy, robustness, and cybersecurity, and
> that they perform consistently in those respects throughout their lifecycle."

**Art. 16, chapeau and point (a) — Obligations of providers of high-risk AI systems**

verbatim:
> "Providers of high-risk AI systems shall: (a) ensure that their high-risk AI
> systems are compliant with the requirements set out in Section 2; [...]"
(points (b) to (l) list the rest — indication of identity, quality management
system, documentation, log-keeping, conformity assessment, CE marking,
registration, corrective action, cooperation with authorities, accessibility —
not quoted here, this catalog's criteria cite the specific provisions instead.)

**Art. 17(1) — Quality management system**

verbatim:
> "Providers of high-risk AI systems shall put a quality management system in
> place that ensures compliance with this Regulation. That system shall be
> documented in a systematic and orderly manner in the form of written policies,
> procedures and instructions [...]"
(followed by points (a) to (m), the full list of what the QMS must cover — not
quoted here, none of the criteria in this catalog cite a specific point.)

**Art. 19(1) — Automatically generated logs (provider's retention duty)**

verbatim:
> "Providers of high-risk AI systems shall keep the logs referred to in Article
> 12(1), automatically generated by their high-risk AI systems, to the extent
> such logs are under their control. [...] the logs shall be kept for a period
> appropriate to the intended purpose of the high-risk AI system, of at least six
> months, unless provided otherwise in the applicable Union or national law, in
> particular in Union law on the protection of personal data."

**Art. 25(1)(b) — Responsibilities along the AI value chain**

verbatim:
> "Any distributor, importer, deployer or other third-party shall be considered
> to be a provider of a high-risk AI system for the purposes of this Regulation
> and shall be subject to the obligations of the provider under Article 16, in any
> of the following circumstances: [...] (b) they make a substantial modification
> to a high-risk AI system that has already been placed on the market or has
> already been put into service in such a way that it remains a high-risk AI
> system pursuant to Article 6 [...]"

**Art. 26(6) — Obligations of deployers of high-risk AI systems: log retention**

verbatim:
> "Deployers of high-risk AI systems shall keep the logs automatically generated
> by that high-risk AI system to the extent such logs are under their control, for
> a period appropriate to the intended purpose of the high-risk AI system, of at
> least six months, unless provided otherwise in applicable Union or national law,
> in particular in Union law on the protection of personal data."

**Art. 26(7) — Obligations of deployers of high-risk AI systems: informing workers**

verbatim:
> "Before putting into service or using a high-risk AI system at the workplace,
> deployers who are employers shall inform workers' representatives and the
> affected workers that they will be subject to the use of the high-risk AI
> system. This information shall be provided, where applicable, in accordance
> with the rules and procedures laid down in Union and national law and practice
> on information of workers and their representatives."

**Art. 49(1) — Registration**

verbatim:
> "Before placing on the market or putting into service a high-risk AI system
> listed in Annex III, with the exception of high-risk AI systems referred to in
> point 2 of Annex III, the provider or, where applicable, the authorised
> representative shall register themselves and their system in the EU database
> referred to in Article 71."

**Art. 27(1) — Fundamental rights impact assessment for high-risk AI systems**

verbatim:
> "Prior to deploying a high-risk AI system referred to in Article 6(2), with the
> exception of high-risk AI systems intended to be used in the area listed in
> point 2 of Annex III, deployers that are bodies governed by public law, or are
> private entities providing public services, and deployers of high-risk AI
> systems referred to in points 5(b) and (c) of Annex III, shall perform an
> assessment of the impact on fundamental rights that the use of such system may
> produce."

**Art. 50(1), (2) and (4) — Transparency obligations**

verbatim:
> "Providers shall ensure that AI systems intended to interact directly with
> natural persons are designed and developed in such a way that the natural
> persons concerned are informed that they are interacting with an AI system,
> unless this is obvious from the point of view of a natural person who is
> reasonably well-informed, observant and circumspect, taking into account the
> circumstances and the context of use. [...] Providers of AI systems, including
> general-purpose AI systems, generating synthetic audio, image, video or text
> content, shall ensure that the outputs of the AI system are marked in a
> machine-readable format and detectable as artificially generated or
> manipulated. [...] Deployers of an AI system that generates or manipulates
> image, audio or video content constituting a deep fake, shall disclose that the
> content has been artificially generated or manipulated."

**Art. 72(1)-(2) — Post-market monitoring by providers**

verbatim:
> "Providers shall establish and document a post-market monitoring system in a
> manner that is proportionate to the nature of the AI technologies and the risks
> of the high-risk AI system. The post-market monitoring system shall actively
> and systematically collect, document and analyse relevant data which may be
> provided by deployers or which may be collected through other sources on the
> performance of high-risk AI systems throughout their lifetime [...]"

**Art. 73(1)-(2) — Reporting of serious incidents**

verbatim:
> "Providers of high-risk AI systems placed on the Union market shall report any
> serious incident to the market surveillance authorities of the Member States
> where that incident occurred. [...] not later than 15 days after the provider
> or, where applicable, the deployer, becomes aware of the serious incident."

**Art. 53(1)(d) — Obligations for providers of general-purpose AI models**

verbatim:
> "Providers of general-purpose AI models shall: [...] (d) draw up and make
> publicly available a sufficiently detailed summary about the content used for
> training of the general-purpose AI model, according to a template provided by
> the AI Office."

**Art. 55(1) — Obligations of providers of general-purpose AI models with systemic risk**

verbatim:
> "In addition to the obligations listed in Articles 53 and 54, providers of
> general-purpose AI models with systemic risk shall: (a) perform model
> evaluation in accordance with standardised protocols and tools reflecting the
> state of the art, including conducting and documenting adversarial testing of
> the model with a view to identifying and mitigating systemic risks; (b) assess
> and mitigate possible systemic risks at Union level [...]"

**Art. 99(3) — Penalties**

verbatim:
> "Non-compliance with the prohibition of the AI practices referred to in Article
> 5 shall be subject to administrative fines of up to EUR 35 000 000 or, if the
> offender is an undertaking, up to 7 % of its total worldwide annual turnover for
> the preceding financial year, whichever is higher."

## Dates

Staged application. A finding is not "already breached" if its date has not arrived —
say which date it lands on.

| From | What applies |
|---|---|
| 1 Aug 2024 | entry into force |
| 2 Feb 2025 | prohibited practices (Art. 5) and AI literacy (Art. 4) |
| 2 Aug 2025 | GPAI obligations, governance structure, penalties |
| 2 Aug 2026 | the bulk of the Act, including Annex III high-risk obligations |
| 2 Aug 2027 | high-risk systems that are safety components of products under Annex I |

## What this means for the assessment

1. **Classification comes before everything.** Where the intake suggests a
   high-risk use case but nothing in the policy classifies it, that is not one
   finding among many — it is a precondition, and it belongs in `alerts`.
2. **Art. 14 is graduated, and this is where policies overshoot most often.**
   Human oversight is required *for high-risk systems*. A blanket "every AI output
   is reviewed in full by a human" is a decision, not the Act's requirement — the
   latitude section is where that gets said.
3. **Three separate log duties, not one.** Art. 12 requires the system to be
   *capable* of recording events; Art. 19 requires the provider to *keep* those
   logs for at least six months; Art. 26(6) requires the deployer to do the same
   on their side. All three are about keeping logs, not about evaluating them — a
   policy that mandates audit-proof logging without naming a system that evaluates
   the logs meets the duty on paper and typed `cantwork` in the report.
4. **Art. 4 is cheap to meet and almost always missing.** It applies regardless of
   risk class, and a policy that says nothing about competence fails it.
5. **Art. 26(7) intersects with works council law.** See `works-council.md` — in
   Germany the two together are what stops rollouts, not either one alone.
