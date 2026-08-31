<!-- Loaded in step 3a. Evaluated against the intake profile. See SKILL.md. -->

# Criteria — 27 checks

Five groups: **Data · Models · Use · Infrastructure** along the processing path, and
**Governance** across all four. Groups one to four feed the information security
coverage figure, governance feeds its own — see `method.md` § 5.8.

**Every criterion is activated against the profile.** One that is not activated is
not applicable, and is reported as not applicable, never as a gap. Quietly dropping
it reads like full coverage.

Field meanings:

| Field | Meaning |
|---|---|
| `quick` | part of the 15-criterion set that `quick` runs |
| `weight` | 1 supplementary · 2 important · 3 load-bearing. Weights the coverage mean |
| `nature` | `duty` · `duty_conditional` · `choice` — see `method.md` § 4.6 |
| `when` | activation condition against the profile. `always` = always active |
| `duty_when` | only for `duty_conditional`: when it becomes a duty |
| `norms` | reference norms for the coverage chart |
| `delta` | present where the *topic* is owned by another policy: what has to be in the AI policy as opposed to what the general document already carries. See § "Scope" below |
| `hints` | search terms for finding the citation. **Starting points, not a closed list** |
| `needs` | a precondition outside the document. Missing → the cannot-work note, `method.md` § 5.6 |
| `strict if` | wording that answers flatly where the law grades → finding type `strict` |

**When the policy is written in another language, translate the hints before
searching.** A German policy says "Klassifizierung", "Freigabe", "Protokollierung",
and none of the hints will match literally. The report itself is always written in
English.

**Liability exposure per act**, for the tone of duty findings (`method.md` § 4.6):

| Act | If unmet |
|---|---|
| EU AI Act | supervisory measures and fines; prohibition for prohibited practices |
| GDPR | fines up to 4 % of group turnover, damages under Art. 82 |
| NIS2 | fines and personal accountability at management level |
| DORA | supervisory measures |
| GeschGehG | loss of trade secret protection where reasonable measures are missing |
| BetrVG / ArbVG | injunctive relief; a rollout without staff involvement stays contestable |
| CRA / MDR | restriction of market access |

**Norm groups for the coverage chart.** Two groups only, and a gap means something
different in each:

- `law` — EU AI Act, GDPR, NIS2, DORA, CRA, MDR, BetrVG, ArbVG, GeschGehG → a legal
  shortfall
- `standard` — ISO/IEC 27001, 27017, 27701, 42001 → relevant where there is a
  certification goal, otherwise a benchmark

**OWASP is not in that chart, and neither is NIST.** A ratio over "criteria that
happen to cite this document" is not interpretable — with three citations it reads
`0 of 3`, and a reader takes that for "three of ten categories", which it is not.
The OWASP categories are reported **by name with a status each** instead, as
`risks[]` in the report (`report.md`), so a reader can see which threat was checked
and which was not.

**NIST AI RMF appears in no criterion at all.** It is a process framework organised
in four functions (Govern, Map, Measure, Manage), not a list of threats — citing a
function as if it were an attack path is a category error, and one citation cannot
carry a coverage figure either. Its one useful observation stays in
`laws/standards.md`: "Measure" is the function most policies have nothing under, and
that is worth saying in a governance finding without a bar to back it.

### Which OWASP category each criterion covers

Eight of the ten 2026 categories map onto this catalogue. The mapping is what
`risks[]` is built from:

| Category | Criteria |
|---|---|
| **LLM01** Prompt Injection | `USE-01` |
| **LLM02** Sensitive Information Disclosure | `DATA-01` · `DATA-04` · `USE-02` |
| **LLM03** Excessive Agency | `USE-03` · `USE-04` |
| **LLM04** Supply Chain | `MODEL-01` · `MODEL-05` · `INFRA-07` |
| **LLM05** Data and Model Poisoning | `MODEL-03` · `INFRA-03` |
| **LLM07** Misinformation | `USE-09` |
| **LLM09** Vector and Embedding Weaknesses | `INFRA-03` |
| **LLM10** Improper Output Handling | `USE-09` |

**Two categories this catalogue does not check, and the report says so rather than
implying full coverage:**

- **LLM06** Unbounded Consumption — cost and rate limiting, and model extraction
  through volume. No criterion covers it; it is an operations and commercial control
  more than a policy statement, and a policy that omits it is not obviously wrong.
- **LLM08** Hidden Context Exposure — system prompt and context leakage. Genuinely a
  gap in this catalogue: it matters where a company builds its own assistant, and the
  criterion that used to carry it was cut when the catalogue was reduced.

Where the profile makes a category inapplicable, mark it `na` with the reason — a
pure SaaS user cannot poison a model it does not train.

---

## Scope — this assesses an AI policy, not a policy set

**Assume the company has other policies.** An information security policy exists in
almost every organisation this runs for, and a data protection policy, a retention
standard and a supplier standard usually do too. A finding that belongs in one of
those is not a finding here — it is noise, and acting on it makes the AI policy worse,
because duplicated rules drift apart from the originals over time.

So the boundary is drawn **inside each criterion, not by asking what else exists.**
Every criterion whose topic a general document would own carries a `delta` field
saying what has to be in the AI policy instead. Assess that, and only that.

This is why the boundary does not depend on knowing the company's document set. A
binary "yes, we have an ISMS" would not tell you whether that ISMS covers outbound
traffic from an agent runtime — and an ISMS does not carry the AI delta in any case,
by definition. Asking would buy weak evidence for a strong conclusion.

Three legitimate outcomes per criterion carrying a `delta`:

| The AI policy… | Verdict |
|---|---|
| states the AI delta itself | assess normally against the levels |
| routes to a **specifically named** existing document, and the delta is either in that reference or not needed | **met** — see `method.md` § 5.3. "The applicable rules" is not a named document |
| neither states the delta nor routes anywhere | a finding — but about the **missing connection**, not about the general topic |

**The rule that makes this testable, and it is absolute:** never write a finding whose
fix would be to copy generic content into the AI policy. Read every recommendation
back and ask whether following it would duplicate something an information security
policy already says. If yes, the finding is wrong — rewrite it as the handoff it
actually is:

> Not "retention periods are not defined" but "the policy does not say that prompts
> and chat logs fall under your retention standard, so nobody applies it to them."

**One defect, one finding.** Several criteria can touch the same weakness — `USE-11`
and `GOV-07` both bear on whether an incident can be reconstructed. Report it once,
under the criterion that fits it best, and let the other one carry its own distinct
aspect or nothing at all. Two findings for one defect makes the report look longer
and the reader trust it less.

---

## Data

### DATA-01 · Which data may go into which system
`quick: yes` · `weight: 3` · `nature: choice` · `when: always`
- **ask** Does the policy say which class of data may go into which AI system — as a
  matrix, rather than a blanket ban?
- **why** The central steering rule. Without it every other data rule is
  indeterminate; where it is blanket, it usually blocks exactly the workflows that
  create the value.
- **norms** OWASP LLM02 · GDPR Art. 5 · ISO 27001 A.5.12 · ISO 42001 B.7.2
- **hints** classification, confidential, internal, public, approval, data category
- **needs** a data classification scheme (`profile.has` includes classification)
- **strict if** whole data classes banned without differentiating by system — "no
  internal data in AI systems"

### DATA-02 · Personal data: legal basis, purpose, minimisation
`quick: yes` · `weight: 3` · `nature: duty` · `when: 'personal' in profile.data`
- **ask** Does the policy govern legal basis, purpose limitation and data
  minimisation specifically for AI processing, and does it say when an impact
  assessment is needed?
- **why** In data protection terms AI processing is not a special case, but it is
  regularly treated as one and therefore skipped.
- **delta** The data protection policy owns lawful bases and impact assessments as
  such. What belongs here is that AI processing is recognised as processing at all —
  and which of your AI uses need their own basis or assessment.
- **norms** GDPR Art. 5 · GDPR Art. 6 · GDPR Art. 35 · ISO 27701
- **hints** personal data, legal basis, purpose limitation, DPIA, impact assessment,
  minimisation

### DATA-04 · The vendor contract rules out training on your data
`weight: 3` · `nature: duty_conditional` · `when: 'saas_chat' or 'api_platform' in profile.sourcing`
- **duty_when** processing on behalf applies — SaaS or API with personal data
- **ask** Does the policy require a contractual ban on the vendor using submitted
  data to train its models, and does it name who verifies that?
- **why** The single most effective measure against uncontrolled data outflow in SaaS
  use, and a contract question rather than a technical problem.
- **norms** OWASP LLM02 · GDPR Art. 28 · ISO 27001 A.5.20
- **hints** training, reuse, opt-out, processor, processing on behalf, contract

### DATA-05 · Retention and deletion of prompts, outputs and logs
`quick: yes` · `weight: 2` · `nature: duty` · `when: always`
- **ask** Are there retention periods and named owners for deleting conversation
  data, prompt histories and interaction logs — including deletion requests reaching
  search indexes and logs?
- **why** Conversation data is a data holding of its own, usually ungoverned, with a
  high density of accumulated detail. A deletion request has to reach the search
  index and the logs too, and almost no policy follows that path to the end.
- **delta** The retention policy owns periods and deletion procedures. What belongs
  here is naming prompts, outputs and chat logs as a data holding it applies to —
  including that a deletion request has to reach the search index.
- **norms** GDPR Art. 5 · GDPR Art. 17 · ISO 27001 A.5.33
- **hints** retention, deletion period, history, log, archiving, erasure, data
  subject rights

### DATA-07 · Trade secrets, IP and customer data under NDA
`weight: 3` · `nature: duty_conditional` · `when: 'ip' or 'nda_customer' in profile.data`
- **duty_when** `'ip' in profile.data` (GeschGehG) or `'nda_customer'` (contractual duty)
- **ask** Does the policy explicitly address trade secrets and restrictions coming
  from customer contracts — NDAs, bans on processing in third-party systems?
- **why** Many enterprise contracts implicitly prohibit processing in third-party
  systems, and trade secret protection exists only where reasonable secrecy measures
  do. The breach usually surfaces in an audit or a dispute.
- **delta** Confidentiality classes and NDA handling are owned elsewhere. What
  belongs here is whether entering such material into an AI system counts as a
  disclosure, and under which conditions it does not.
- **norms** GeschGehG · ISO 27001 A.5.20
- **hints** trade secret, NDA, customer data, confidentiality agreement, IP

---

## Models

### MODEL-01 · Approved models, and a way to get a new one approved
`quick: yes` · `weight: 3` · `nature: choice` · `when: always`
- **ask** Does the policy hold a list of approved models and vendors, and describe
  how a new one gets admitted?
- **why** Without an admission route every approved list is out of date within a
  quarter, and then it is a reason to work around the policy rather than follow it.
- **norms** OWASP LLM04 · ISO 42001 B.6.2 · ISO 27001 A.5.19 · AI Act Art. 53 · CRA
- **hints** approved, permitted, vendor, model list, authorisation
- **strict if** an approved list with no admission route, or an approval path the
  policy itself does not describe

### MODEL-03 · Who may fine-tune, with what data
`weight: 3` · `nature: choice` · `when: 'fine_tuning' in profile.sourcing`
- **ask** Is it governed who may fine-tune, with which data, and how the result is
  approved and documented — including where the training data came from and what
  rights exist in it?
- **why** A fine-tuned model can reproduce its training data, which makes data
  classification a property of the model. It is also what turns a user into a
  provider under the AI Act.
- **norms** OWASP LLM05 · AI Act Art. 10 · ISO 42001 B.7
- **hints** fine-tuning, training, adaptation, customisation, training data,
  provenance, rights

### MODEL-04 · Testing before go-live
`quick: yes` · `weight: 3` · `nature: duty_conditional` · `when: always`
- **duty_when** high-risk classification — AI Act Art. 9 and Art. 17 for providers,
  Art. 26 for deployers
- **ask** Does the policy require an evaluation against defined criteria before a
  system goes live, including adversarial testing?
- **why** Without a test criterion every approval is an opinion. For high-risk
  systems the assessment is a duty, not an option.
- **delta** Release and change management owns the gate itself. What belongs here is
  what an AI system has to be tested *for* — including behaviour under adversarial
  input, which a functional test suite does not cover.
- **norms** AI Act Art. 9 · AI Act Art. 15 · MDR · ISO 42001 B.6.2
- **hints** test, evaluation, red team, acceptance, approval, quality criterion

### MODEL-05 · What happens when the vendor changes the model
`weight: 2` · `nature: choice` · `when: always`
- **ask** Does the policy say what happens when the vendor changes the model or its
  version — retest, re-approval, rollback?
- **why** With SaaS the vendor changes the model without the customer doing anything.
  Yesterday's approval then applies to a different system. Almost no policy covers
  this, and it is cheap to fix.
- **norms** OWASP LLM04 · ISO 27001 A.8.32 · ISO 42001 B.6.2
- **hints** version, change, rollback, model change, release, deprecation

---

## Use

### USE-01 · Instructions hidden in content the system reads
`quick: yes` · `weight: 3` · `nature: choice` · `when: always`
- **ask** Does the policy name prompt injection as a risk, and does it distinguish
  what a user types from instructions that arrive inside processed content — mail,
  documents, web pages?
- **why** The indirect path is the more relevant one and the one policies almost
  never mention. A rule that only covers what users type misses the actual attack.
- **norms** OWASP LLM01 · AI Act Art. 15 · ISO 42001 B.6.2
- **hints** prompt injection, manipulation, input, untrusted, third-party content

### USE-02 · Limiting where data can flow out to
`weight: 3` · `nature: choice` · `when: profile.actions in ['write','transact']`
- **ask** Does the policy treat the environment AI systems run in as a network zone
  of its own — with outbound destinations restricted and not changeable from inside —
  or does it point to the network standard that governs that?
- **why** Manipulation through processed content cannot be reliably prevented, so the
  outflow path is the control that matters. The AI-specific point is that this is a
  **new zone** a company's existing network rules were not written for: they govern
  users and servers, not a system that composes its own outbound requests.
- **delta** A general network policy owns allowlisting as a technique. What belongs
  here is that the AI environment is in scope of it at all.
- **norms** OWASP LLM02 · ISO 27001 A.8.20 · ISO 27001 A.8.22
- **hints** egress, outbound, proxy, allowlist, network access, exfiltration

### USE-03 · Different rules for reading, writing and transacting
`weight: 3` · `nature: choice` · `when: profile.actions in ['write','transact']`
- **ask** Does the policy distinguish reading, writing and transacting actions and
  attach different requirements to each — including whether the system acts as the
  user or under an identity of its own?
- **why** Without gradation you get one of two failures: the strictness needed for a
  payment applies to everything, which blocks the business, or the looseness of
  reading applies to everything, which is negligent. And where a system can act
  unattended, attributability breaks at exactly that boundary.
- **norms** OWASP LLM03 · AI Act Art. 14 · ISO 42001 B.9.2 · ISO 27001 A.5.16
- **hints** autonomy, action, execute, write, permission, agent, on behalf of,
  service account
- **strict if** all automated actions need approval across the board, regardless of
  effect

### USE-04 · Which actions need a human sign-off
`quick: yes` · `weight: 3` · `nature: duty_conditional` · `when: always`
- **duty_when** high-risk classification (AI Act Art. 14) or automated individual
  decision-making (GDPR Art. 22)
- **ask** Is it named concretely which actions need a human sign-off, with thresholds
  rather than a blanket formula, and who gives it?
- **why** "Human in the loop" without saying what for is not actionable. In practice
  it is either ignored or it turns into an emergency brake on everything.
- **norms** OWASP LLM03 · AI Act Art. 14 · AI Act Art. 22 (GDPR) · ISO 42001 B.9.2
- **hints** approval, authorisation, dual control, human in the loop, threshold,
  sign-off
- **strict if** an approval duty with no threshold, or with no named approving role

### USE-09 · Checking outputs before they are used
`quick: yes` · `weight: 3` · `nature: choice` · `when: always`
- **ask** Does the policy say when a result has to be checked, and how its onward use
  in other systems is handled?
- **why** The damage rarely happens in the chat. It happens where the output is
  executed, sent or published unchecked.
- **norms** OWASP LLM07 · OWASP LLM10 · AI Act Art. 14
- **hints** result, output, review, responsibility, hallucination, verification
- **strict if** a full manual review duty for every output regardless of risk — it
  cancels the efficiency gain entirely

### USE-11 · Logging an incident could be reconstructed from
`quick: yes` · `weight: 3` · `nature: duty_conditional` · `when: always`
- **duty_when** high-risk classification (AI Act Art. 12, Art. 26(6))
- **ask** Does the policy require logging of what the system did — tool calls,
  automated approvals, messages between systems — in a place where the logs are
  actually looked at?
- **why** Without that trail no incident can be explained afterwards and no duty of
  oversight can be evidenced.
- **delta** The logging standard owns retention, protection and who reviews logs.
  What belongs here is *which events are worth logging* for an AI system — the tool
  call, the target system, the identity that triggered it, the approval — none of
  which an application-logging standard anticipates.
- **norms** AI Act Art. 12 · AI Act Art. 19 · ISO 27001 A.8.15
- **hints** log, logging, traceability, SIEM, audit trail, monitoring
- **needs** log evaluation covering AI systems (`profile.has`)

### USE-12 · Which tools are allowed, and how to ask for another
`quick: yes` · `weight: 3` · `nature: choice` · `when: always`
- **ask** Does the policy name the permitted tools, and does it describe how someone
  requests a tool that is not on the list?
- **why** A ban with no request route produces shadow AI instead of preventing it,
  and moves the risk to where nobody can see it. This is the most reliable
  over-restriction finding in the whole catalog.
- **norms** ISO 27001 A.5.19 · ISO 42001 B.6.2
- **hints** permitted tools, private use, request, prohibition, tool, shadow IT
- **strict if** a ban list with no request route, or a request route the policy does
  not describe

---

## Infrastructure

### INFRA-01 · Separate, disposable environments
`weight: 3` · `nature: choice` · `when: profile.actions in ['write','transact']`
- **ask** Does the policy say that systems acting on their own get their own runtime,
  separate from production credentials and discarded after use — or does it place them
  under the existing hardening standard by name?
- **why** Decides whether a successful attack reaches one session or the whole
  environment. The AI-specific point is that an agent runtime is a **new kind of
  workload**: it is neither a user's device nor a release-managed service, so an
  existing hardening standard usually has no category for it.
- **delta** Separation and ephemerality are general infrastructure practice. What
  belongs here is that agent runtimes are named as workloads it applies to.
- **norms** ISO 27001 A.8.31 · ISO 27001 A.8.22 · NIS2 Art. 21
- **hints** sandbox, isolation, container, execution environment, segmentation,
  production system

### INFRA-03 · Permissions enforced inside the search index
`weight: 3` · `nature: choice` · `when: 'api_platform' or 'self_hosted' in profile.sourcing`
- **ask** Does the policy require access rights to hold at the level of the
  individual document in a search index, not only at system level — and does it say
  who may put content into that index?
- **why** The most common silent data outflow path when a company builds its own
  assistant: the index does not carry the access rights of the systems the content
  came from. And whoever can write to the index steers the answer.
- **norms** OWASP LLM05 · OWASP LLM09 · ISO 27001 A.5.15 · ISO 27001 A.8.3 ·
  ISO 27001 A.8.28
- **hints** vector, index, knowledge base, permission, access filter, RAG, curation

### INFRA-07 · Vendor risk and a way out
`quick: yes` · `weight: 2` · `nature: duty_conditional` · `when: always`
- **duty_when** `'personal' in profile.data` (GDPR Art. 28) or NIS2 or DORA applies,
  or processing happens outside the EU/EEA (transfer basis needed)
- **ask** Does the policy name the questions an AI vendor has to answer **beyond** a
  normal supplier assessment — may the vendor change the model, may it train on your
  submitted data, where is the processing done, and what happens to prompts, outputs
  and fine-tunes when the contract ends?
- **why** Every company already assesses suppliers. None of those questionnaires ask
  whether the product will quietly become a different product next quarter, which is
  the normal case here.
- **delta** General third-party risk management owns assessment, sub-processors and
  exit as a process. What belongs here are the four AI-specific questions it does not
  contain.
- **norms** OWASP LLM04 · GDPR Art. 28 · GDPR Art. 32 · GDPR Art. 44 · DORA Art. 28 ·
  NIS2 Art. 21 · ISO 27017
- **hints** vendor, service provider, sub-processor, exit, processor, region,
  storage location, tenant

---

## Governance

### GOV-01 · Named roles, and someone who decides
`quick: yes` · `weight: 3` · `nature: duty` · `when: always`
- **ask** Does the policy name who is accountable — an owner per use case, security,
  data protection, legal, the business — and a body that decides?
- **why** A policy with no named decision-makers produces escalations with no
  addressee, and therefore standstill.
- **delta** The organisational model owns roles and escalation paths. What belongs
  here is who owns an individual AI use case and who admits a model — two
  accountabilities no existing role description contains.
- **norms** ISO 42001 B.5 · AI Act Art. 26 · ISO 27001 A.5.2
- **hints** responsibility, role, owner, committee, board, accountable

### GOV-02 · A list of AI use cases with a risk rating
`quick: yes` · `weight: 3` · `nature: duty_conditional` · `when: always`
- **duty_when** high-risk classification (AI Act Art. 49) or `'personal' in
  profile.data` (GDPR Art. 30)
- **ask** Does the policy require a central list of all AI use cases with a risk
  rating, and a duty to keep it current?
- **why** Without the list no statement about the current state is possible, and none
  of the duties that follow from a risk rating can be met.
- **norms** AI Act Art. 6 · AI Act Art. 49 · GDPR Art. 30 · ISO 42001 B.6.1
- **hints** inventory, register, record, use case, classification
- **needs** a use-case inventory (`profile.has`)

### GOV-03 · Which role you are in under the AI Act
`weight: 3` · `nature: duty_conditional` · `when: profile.jurisdiction includes the EU`
- **duty_when** EU activity — the role assignment determines the whole set of duties
  (AI Act Art. 25)
- **ask** Does the policy make clear, per use case, whether you are a user or a
  provider of the system, and does it derive the concrete duties from that?
- **why** The role determines the entire duty set. A company that has not settled it
  either does too much or does the wrong things. Fine-tuning a model and shipping the
  result makes you a provider, which is the case most often missed.
- **norms** AI Act Art. 3 · AI Act Art. 16 · AI Act Art. 25 · AI Act Art. 26
- **hints** provider, deployer, operator, role, placing on the market, own name

### GOV-05 · How to get an exception
`quick: yes` · `weight: 3` · `nature: choice` · `when: always`
- **ask** Does the policy say who decides an AI-specific deviation and on what basis
  — or does it route to the company's existing exception process by name, with the AI
  competence added to it?
- **why** The single most important enabling mechanism in any policy. Without it every
  strict rule becomes either a blocker or something people quietly break, and both are
  worse than a documented exception. The AI-specific point is competence: a general
  risk-acceptance body cannot judge whether an agent's write access is acceptable.
- **delta** A general exception process owns the request, the time limit and the
  record. What belongs here is who is competent to judge an AI deviation.
- **norms** ISO 27001 A.5.1 · ISO 42001 B.6.1
- **hints** exception, deviation, risk acceptance, request, time-limited, waiver
- **needs** an exception process (`profile.has`)

### GOV-07 · Incidents, and who has to be told
`quick: yes` · `weight: 3` · `nature: duty` · `when: always`
- **ask** Does the policy define what counts as an AI incident, how it is reported
  internally, which external deadlines apply, and who can switch a system off?
- **why** AI incidents rarely fit existing categories. Without a definition nothing
  gets reported, because nobody realises something was reportable. And the ability to
  switch off is the only control that takes effect immediately in an unclear
  incident — it has to be named before the incident, not during it.
- **delta** Incident management owns triage, escalation and the reporting deadlines.
  What belongs here is **what counts as an AI incident** — a wrong output acted on, an
  agent exceeding its scope — because none of those match an existing category, and
  who can switch a system off.
- **norms** AI Act Art. 73 · GDPR Art. 33 · NIS2 Art. 23 · DORA Art. 19 · ISO 27001
  A.5.29
- **hints** incident, report, escalation, deadline, notification, shutdown, kill
  switch, deactivation

### GOV-08 · Telling people it is AI
`weight: 2` · `nature: duty_conditional` · `when: always`
- **duty_when** `'customer_interaction'` or `'synthetic_content'` in
  `profile.use_cases` (AI Act Art. 50)
- **ask** Does the policy govern the marking of AI-generated content and telling
  people when they are interacting with an AI system?
- **why** A directly applicable duty with external effect, and a reputational topic
  long before it becomes a fine topic.
- **norms** AI Act Art. 50
- **hints** marking, transparency, notice, disclose, AI-generated, labelling

### GOV-09 · Training, and evidence that it happened
`weight: 2` · `nature: duty` · `when: always`
- **ask** Does the policy require a level of training appropriate to the role, and
  does it evidence that level?
- **why** A directly applicable duty since February 2025 under AI Act Art. 4, and in
  practice the precondition for the policy being lived at all.
- **delta** Security awareness training is owned elsewhere and does not cover this.
  What belongs here is competence to judge an AI output — which is a different skill
  from recognising a phishing mail.
- **norms** AI Act Art. 4 · ISO 42001 B.7.2
- **hints** training, competence, awareness, literacy, staff training, onboarding

### GOV-10 · Involving the works council
`weight: 3` · `nature: duty_conditional` · `when: profile.jurisdiction includes DE or AT`
- **duty_when** employees in DE or AT **and** the AI use makes performance or conduct
  measurable
- **ask** Does the policy address involving employee representatives where AI systems
  make performance or conduct measurable?
- **why** In the DACH region this is what stops rollouts. Without involvement the
  rollout stays contestable, however good the security is. BetrVG § 87(1) no. 6 gives
  an enforceable right, and since the 2024 amendment BetrVG names AI explicitly in
  §§ 90, 95 and 80.
- **norms** BetrVG § 87 · ArbVG § 96a
- **hints** works council, co-determination, works agreement, employee
  representatives, staff council
- **needs** a works agreement (`profile.has`)

---

## Which 15 `quick` runs

`DATA-01` · `DATA-02` · `DATA-05` · `MODEL-01` · `MODEL-04` · `USE-01` · `USE-04` ·
`USE-09` · `USE-11` · `USE-12` · `INFRA-07` · `GOV-01` · `GOV-02` · `GOV-05` ·
`GOV-07`

All of these are `when: always` or activate on the default data type, so `quick`
never depends on an answer it did not ask for. `GOV-03` is deliberately **not** in
the set: settling which AI Act role you are in needs intake answer B, and asserting
it without that answer would be exactly the kind of confident guess this skill is
built to avoid. The report says so instead.

The other 13 criteria are not "extras" — they cover fine-tuning, agents acting on
their own, self-built assistants, trade secrets and the works council. If any of
those apply to the client, `quick` is the wrong depth and the report says which
criteria were left out.
