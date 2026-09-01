<!-- Loaded across steps 1-3. See SKILL.md. Verbatim article text: references/laws/ -->

# Method — depth, intake, legal frame, scoring

Four things in one file, because they are one chain: the depth decides how much you
ask, the answers decide which laws apply, the laws decide which criteria are duties,
and the scoring turns that into findings.

---

## 1 · Depth — ask this first

The only question asked before the policy is read. Three options, **Standard**
recommended.

> How much should I ask you up front? More questions mean a sharper report, fewer
> mean you are done faster.

| | Depth | Questions | What you get, and what you give up |
|---|---|---|---|
| **1** | **Quick** | none | 15 core criteria, the 10 most serious findings, coverage of the legal duties. I take everything from the document and default the rest. What I cannot settle is whether a use case is high-risk or whether NIS2 applies — both stay marked "to be checked", and the recommendations stay generic |
| **2** | **Standard** *(default)* | one message, five items | all 27 criteria, up to 18 findings, high-risk screening, and recommendations that can name your workflows |
| **3** | **Extensive** | one message, then a short second one | every finding, plus: whether a rule can work at all given what exists today, whether a delegation lands anywhere, NIS2 settled rather than flagged, and the standards mapping |

→ `profile.depth` = `quick` · `standard` · `extensive`

Record it. The report states which depth ran, because a reader has to know whether
"to be checked" means "we looked and it is open" or "we did not ask".

**At `quick`, ask nothing further.** Not one clarifying question. The client chose
speed; honour it and disclose the consequence in the report.

### What each depth costs in work

Budgets, so a run does not quietly grow into the next tier:

| | Criteria | Findings reported | Law files opened | Latitude rows | Risk categories | ISO mapping |
|---|---|---|---|---|---|---|
| `quick` | the 15 marked `quick: yes` | 10 | AI Act + GDPR only | 3 | yes, from the criteria assessed | no |
| `standard` | all 27 | 18 | max 4, those triggered | 4-6 | yes | yes |
| `extensive` | all 27 | all | all triggered | 6-8 | yes | yes |

The risk categories cost nothing extra at any depth: they are derived from criteria
already assessed, not from a separate pass. At `quick` the coverage is thinner because
fewer criteria ran, and the report says which categories had no criterion behind
them.

---

## 2 · Intake — `standard` and `extensive`

**One round, five items.** Not two rounds. With a choice widget, render this as
consecutive picker questions — split any item past the widget's per-question option
cap (C's ten use cases are the one that usually needs it) rather than merging
categories or dropping to text; see `SKILL.md` § "Running this anywhere". Without a
widget, every option below carries a label so the whole thing fits in one line of
reply: `A=S2, B=a, C=1,7, D=a/a,c`.

Where the document already answers an item, **preselect it and say so**. Confirming
is answering.

### A · Scope and where you operate

> Who does this policy apply to, and where do you operate?

| | Level | Typical |
|---|---|---|
| **S1** | Group | several legal entities, several countries |
| **S2** | Single company | one legal entity |
| **S3** | Function or division | IT, HR, engineering |
| **S4** | One use case | one concrete system |

Plus in the same item: **active in the EU** yes/no, **employees in Germany or
Austria** yes/no. *Default: S2, EU yes, DE/AT yes.*

→ `profile.scope`, `profile.scope_text`, `profile.jurisdiction`

**With a choice widget this is two questions:** the scope table above as one
single-select question (4 options), then a second multi-select question with
`Active in the EU` and `Staff in Germany or Austria` as the two options — selecting
neither is a valid, meaningful answer here, unlike in C.

Scope calibrates every level in the report (§ 5.3) and is usually **stated in the
document** — propose it from the section index. EU activity decides the AI Act and
the GDPR. Employees in DE or AT decide co-determination, which in the DACH region is
what stops rollouts.

### B · Your role

> Do you only use AI built by others, or do you also put AI on the market yourselves
> — in your own products or under your own name?

**a** user only · **b** we place AI on the market · **c** both — *default: a*

→ `profile.role` = `deployer` · `provider` · `both`

The single most consequential answer. A pure deployer is not assessed against
conformity assessment at all. Note that fine-tuning a model and shipping the result
makes you a provider — see `laws/eu-ai-act.md`.

### C · What you use AI for

> Does any of this apply? Several answers possible, "none" is valid.

**1** recruiting, applicant screening, performance or conduct assessment
**2** creditworthiness, insurance risk or pricing for individuals
**3** access to education, grading of exams
**4** operating critical infrastructure
**5** law enforcement, migration, border control, justice
**6** biometrics, emotion recognition, categorising people
**7** direct interaction with customers or staff (chatbot, assistant)
**8** producing published text, images, audio or video
**9** software development, coding assistants
**0** none of these — *default: 0*

→ `profile.use_cases`

**Ten options, so a 4-option choice widget needs three questions to cover it
without dropping any.** A tested split that keeps every category: `{1,2,3,4}`,
`{5,6,7,8}`, `{9,0}` — three multi-select questions asked back to back, still one
intake round. The grouping is only an input convenience; it has no legal meaning,
unlike the 1–6 / 7–8 / 9 split described below.

**This is the cross-check that catches the most common mistake in practice** — a
company saying "the AI Act does not concern us, we only use Copilot" while running a
tool that pre-screens job applications. That is Annex III. 1-6 decide high risk and
prohibited practices; 7 and 8 decide the Art. 50 transparency duties; 9 only
activates the source-code criterion and carries no legal consequence.

### D · How you get AI, what data goes through it, and what it may do

Three sub-items, one line:

- **Sourcing** (several): **a** SaaS chat · **b** API platform · **c** self-hosted ·
  **d** own fine-tuning — *default: a*
- **Data** (several): **a** personal · **b** special categories (health, biometrics,
  union membership) · **c** trade secrets and IP · **d** customer data under NDA ·
  **e** regulated data — *default: a*
- **What the systems may do** (one): **a** read only · **b** write — tickets,
  documents, code · **c** transact — orders, payments, production data —
  *default: a*

→ `profile.sourcing`, `profile.data`, `profile.actions`

**With a choice widget this is four questions, not three:** sourcing (4 options,
fits one question), data split `{a,b,c,d}` + `{e}` (five options need two
questions — add "none of these" as the second option's counterpart so the widget's
2-option minimum is met), then actions (3 options, one question).

The three heaviest levers in the catalog. Sourcing decides whether the model
criteria are assessed at all. Data types activate the GDPR and trade-secret duties.
Actions decide how far a failure reaches.

### E · Where AI is meant to pay off — free text, no default

> What are your two or three core value streams, and where is the AI leverage?

→ `profile.value_streams`

**This is the one item with no default, and the reason is worth stating to the
client:** it does not change a single score. It changes whether a recommendation can
say "tie the sign-off duty to the class of action so the service desk is not held
up" instead of "consider differentiating". Without it the recommendations stay
generic, which is the most common way a report like this ends up unused.

No judgement about what a rule *costs* the business is derived from it — that would
need the systems and the strategy, and neither is in the document.

---

## 3 · Second round — `extensive` only

One short message. At `standard`, ask **only** the single item that would flip a
specific finding, with the trigger visible:

> "Section 4.2 allows only classified data to be processed. Is there a
> classification scheme? Without one the rule is formally present but has no effect."

At `quick`, never.

### F · What already exists?

**1** ISMS to ISO 27001 · **2** data classification scheme · **3** DLP · **4**
central login (SSO/IdP) · **5** log evaluation covering AI systems · **6** use-case
inventory · **7** exception process · **8** AI board · **9** works agreement ·
**0** none

→ `profile.has` — feeds the **cannot-work check** (§ 5.6) and prevents duplicate
findings against an existing ISMS. The one optional answer that changes findings
rather than sharpening them.

**Same ten-option case as C.** Split `{1,2,3,4}`, `{5,6,7,8}`, `{9,0}` for a
4-option widget — same grouping, no legal meaning attached here either.

### G · Downstream documents — S1 and S2 only

> The policy delegates detail to entity-level procedures. Do those exist?

→ `profile.downstream` = `yes` · `no` · `unknown`. At S1 this decides whether a
delegation counts as sufficient or as a rule that cannot work (§ 5.3).

### H · Size and sector

> Roughly how many employees and what revenue? Which sector?

→ `profile.size`, `profile.sector`. **Only NIS2 depends on this.** Without it the
report says "NIS2 applicability to be checked", which is an honest state and not a
gap.

---

## 4 · Legal frame — derive it, do not ask for it

Runs after the intake and before the assessment. Each rule: a condition from the
profile → the norm → the criteria it turns into duties.

> **Not legal advice.** This structures the conversation with legal and data
> protection; it is not a defensible conclusion. Every triggering condition is named
> in the report with its basis so it can be checked. AI Act deadlines and dates of
> application should be verified against the current state — there has been movement
> there.

### EU AI Act

| Condition | Consequence | Criteria |
|---|---|---|
| active in the EU | applicable in principle | `GOV-03` |
| `use_cases` has biometrics or emotion recognition **and** use at work or in education | **prohibited practice** (Art. 5) — a stop topic, not a compliance topic | special finding, § 4.5 |
| `use_cases` has recruiting, credit, education access, critical infrastructure or law enforcement | **high risk** (Annex III) | `MODEL-04`, `USE-04`, `USE-11`, `GOV-02` become duties |
| high risk **and** role = deployer | Art. 26: use per instructions, oversight by competent people, keep logs, inform staff | `GOV-01`, `USE-04`, `USE-11`, `GOV-10` |
| high risk **and** role = provider | full provider set: risk management, data governance, technical documentation, conformity assessment, registration | `MODEL-04`, `GOV-02` |
| `use_cases` has customer interaction | Art. 50: people must know they are talking to an AI | `GOV-08` becomes a duty |
| `use_cases` has published synthetic content | Art. 50 marking duty | `GOV-08` becomes a duty |
| always | Art. 4 AI literacy of the people operating the system | `GOV-09` is a duty regardless of risk class |

### GDPR

| Condition | Consequence | Criteria |
|---|---|---|
| `data` has personal | principles, legal basis, storage limitation, accountability | `DATA-02`, `DATA-05`, `GOV-01` |
| `sourcing` has SaaS chat or API platform | processing on behalf: instruction-bound processing, processor agreement required | `DATA-04`, `INFRA-07` |
| `data` has special categories **or** `use_cases` has recruiting | a data protection impact assessment is regularly required | `DATA-02` |
| recruiting or credit **and** the decision is taken without a human | automated individual decision-making — prohibited in principle, exceptions need safeguards | `USE-04` becomes a duty, special finding |
| processing outside the EU/EEA | a transfer basis is needed | `INFRA-07` |

### NIS2

| Condition | Consequence |
|---|---|
| sector in Annex I or II **and** (>50 staff **or** >EUR 10m revenue) | essential or important entity: risk management, supply chain security, reporting duties, management accountability |
| below the thresholds but in Annex I or II | applicability to be checked case by case — the thresholds have exceptions |

→ turns `INFRA-07` and `GOV-07` into duties. Transposition is national: report it as
"to be checked", not as settled. Without answer H, always report it as to be checked.

### Others

| Condition | Norm | Criteria |
|---|---|---|
| financial sector | DORA — ICT third-party risk, register, exit strategies | `INFRA-07`, `GOV-07` |
| places a product with digital elements on the market | CRA — security across the lifecycle | `MODEL-01` |
| medical device | MDR with AI Act Art. 6(1) | `MODEL-04`, `GOV-02` |
| `data` has trade secrets or IP | GeschGehG — protection exists **only** where reasonable secrecy measures do. Without them it lapses | `DATA-07` |
| employees in Germany **and** the AI use makes performance or conduct measurable | BetrVG § 87(1) no. 6 — enforceable co-determination | `GOV-10` becomes a duty |
| employees in Austria, same condition | ArbVG § 96a | `GOV-10` |

**On co-determination:** "makes measurable" is broad. An assistant that logs
invocations regularly meets it. In doubt treat it as applicable and say that you
did — the error the other way is more expensive, because a rollout without staff
involvement stays contestable.

### 4.4 Report divergence, in both directions

Compare the derived frame against what the client assumed. Where they differ, **say
so, do not silently overwrite**:

> **Note on the legal frame.** You named no sector regulation. From answer C
> ("recruiting, applicant screening") it follows that the system is high risk under
> Annex III of the AI Act, which makes four further criteria mandatory. Basis: Annex
> III no. 4 (employment). Please cross-check with legal — I have activated those
> criteria as duties.

- **Under-captured** — the situation triggers more than was assumed. Activate the
  criteria and report it.
- **Over-captured** — a norm was named whose conditions are not evidently met. The
  criteria **stay active** (the self-assessment wins), but the report notes that
  applicability does not follow from the answers. That is itself a finding: a policy
  aligned to a norm that does not apply is a common source of over-restriction.

### 4.5 Special findings — they go above everything else

Two cases are not questions of maturity but immediate findings, in their own section
at the top of the report:

**Prohibited practice.** Emotion recognition at work or in education, biometric
categorisation by protected characteristics, untargeted scraping of facial images.
The question is not how well the policy governs it but whether the use is permitted
at all. Statement: *"Settle whether this use is lawful before any policy question."*

**Automated individual decision-making.** A decision with legal effect or a
significant adverse impact, taken without a human. Statement: *"A human final
decision is not a design option here, it is a precondition."*

### 4.6 Duty versus own choice

Every criterion in `criteria.md` carries a `nature`:

| Value | Meaning | If unmet |
|---|---|---|
| `duty` | follows directly from applicable law | breach of law; liability and fine exposure |
| `duty_conditional` | a duty only where `duty_when` is met | as above, once the condition applies |
| `choice` | good practice, state of the art | no immediate breach, but organisational and due-diligence exposure; in a damage case, the question of adequacy |

This drives three things. **The legal-duties figure** is all active `duty` criteria
plus the `duty_conditional` ones whose condition applies — the number a management
board has to see. **Sorting**: unmet duties come before everything else, whatever
their level. **Tone**: for duties, name the exposure ("fine exposure", "injunctive
relief", "loss of trade secret protection"). For own choices, do not — there the
question is adequacy, not breach.

### 4.7 Source basis — one sentence, not a system

Cite the article. Quote a statute **only** from a `verbatim:` block in
`references/laws/`; those blocks were pasted from the official text. Everything else
in those files is a paraphrase with a citation, and a paraphrase never gets
presented as wording.

**State the date the stored texts were checked.** `laws/README.md` carries it; read
it and put it in `meta.legal_asof`. It is not the report's generation date, and the
two must not be conflated: a report generated today from texts verified two weeks ago
tells the reader to check for amendments since that earlier date, not since today.
Where a cited act has no stored text at all, the date does not cover it — say which
in the footer sentence.

For the report this collapses to **one footer sentence plus a clause in the banner**:
which acts were cited, that article wording was taken from the stored official text
where available and otherwise paraphrased, and that the ISO control numbers are
mapping aids against a licensed standard nobody can store here — anyone needing a certification statement checks
against the purchased text. **No per-norm marks, no badges on findings.** The
distinction matters for how much weight a statement carries; it must not drown out
the statement.

---

## 5 · Scoring

### 5.1 Evidence first — the precondition for everything else

Every assessment above level 1 **must** carry a citation: section number or heading
plus a verbatim quote of at most two sentences.

**Without a citation the finding reads "not addressed", not "poor".** This is the
central safeguard against invented findings. A policy that governs something well
which you failed to find must not appear as a gap — and an invented quote is the
worse error, because it disqualifies the whole report.

### 5.1b Scope — is this a finding for an AI policy at all?

Before scoring, check the criterion's `delta` field in `criteria.md`. Where one is
present, the topic is owned by another document and **only the delta is assessed**.
Where the AI policy neither states the delta nor routes to a specifically named
document, the finding is about the missing connection, never about the general topic.

The test that catches a violation: read your own recommendation back and ask whether
following it would copy content an information security policy already carries. If it
would, the finding is wrong as written. See `criteria.md` § "Scope".

This is not a courtesy to the client's existing documents. A recommendation to
duplicate generic content actively damages the policy set, because the copy and the
original drift apart and nobody knows which one binds.

### 5.2 Usability — the one level, 1 to 5

One question: **can someone act on this rule?**

| Level | Meaning |
|---|---|
| 1 | not addressed |
| 2 | mentioned, but no obligation — a statement of intent |
| 3 | governed but not actionable: no role, no threshold, no process |
| 4 | governed and actionable: role named, trigger clear, process described |
| 5 | governed, actionable and checkable: with a control, evidence or a metric |

**Level 3 is where most real policies sit**, and it is the main reason policies are
formally green and practically without effect. Saying so plainly is one of the more
useful things this report does.

### 5.3 Calibration by scope

A group policy legitimately says "each entity shall establish appropriate access
controls". A use-case policy has to say "agents may not write to the CRM without the
department head's approval". Against the same criterion the group policy always
loses, wrongly.

The ladder is not loosened, it is read at the right level:

| Scope | Level 4 requires | Level 5 additionally |
|---|---|---|
| **S1** group | requirement + addressee + **a mandate to specify, with a deadline and evidence** | central follow-up that it happened |
| **S2** company | requirement + accountable person + process **or** a specific reference to a binding document | a control or a metric |
| **S3** function | as S2, plus thresholds for the frequent cases | as S2 |
| **S4** use case | the **concrete control**: threshold, system name, who approves | evidence that it works |

**The ability to delegate decreases with scope.** At S1, delegation is sufficient,
but only with a named outcome and a deadline — "the entities shall regulate the
details" without a hook stays at **level 3**, and that is the real failure mode of
group policies. At S2 and S3, delegation to an existing, specifically named document
is sufficient; "the applicable rules" is not. At S4, delegation is never sufficient —
there is nobody left to delegate to.

**Met by reference counts at every level.** A criterion met by a specific reference
to another binding document (an ISMS, a works agreement, a group security policy) is
met. The condition is that the reference names the document. This prevents duplicate
findings against an existing ISMS and rewards the right practice over the redundant
one.

Put the calibration rule that applied into `meta.scope_note`. Without it every
framework policy reads like a bad use-case policy.

### 5.4 Risk and strictness — the two matrix axes

Two independent whole numbers, 1 to 5, per finding. They are **not** derived from the
level: the matrix asks whether the depth of regulation matches the risk, the level
asks how well the rule is made. A finding can be level 5 and still be too strict.

- **`risk`** — how high the risk really is in *this* business, given the profile.
  The CISO question. A read-only chat assistant handling public marketing copy is a
  1; an unattended agent with write access to production is a 5.
- **`strictness`** — how strictly the policy governs it. The CIO question. 1 is
  silence, 3 is a proportionate rule, 5 is a flat prohibition or a blanket approval
  duty.

**Spread both honestly across the scale.** If everything lands on 4 and 5 the matrix
says nothing. Rules within one step of the risk count as matched — only a gap of two
or more is a mismatch, which is what the matrix colours.

### 5.5 Finding type — three, and no symbols

| Type | `type` | Condition | Rendering |
|---|---|---|---|
| **On point** | `ok` | proportionate to the risk, level ≥ 4 | teal, filled |
| **Gap** | `gap` | the risk is not covered, or level ≤ 2 where risk ≥ 4 | magenta, filled |
| **Too strict** | `strict` | a flat answer where the norm behind it allows steps, **or** an approval duty with no threshold, **or** a prohibition with no way to request an exception | magenta, hollow |
| not applicable | — | `when` not met | listed separately, counts towards nothing |

Filled versus hollow, not hue, separates *Gap* from *Too strict*: the palette has
only two reliably distinguishable chromatic poles, and the distinction has to survive
greyscale printing and red-green deficiency. The label carries the rest. **No glyphs,
no marks inside the matrix cells.**

**A shortfall against the legal minimum is a `gap`, never `strict`.** The two never
apply to the same rule. And where the law itself is absolute — a human decides, full
stop — "a human always decides" is the requirement, not an over-reach. The
over-restriction finding exists only where the law grades and the policy does not.

### 5.6 Cannot work yet — a note, not a fourth type

The policy requires something whose precondition does not exist per `profile.has`: a
classification rule with no classification scheme, a logging duty with no system that
evaluates logs, a recertification of service accounts with no central login.

Formally present, practically without effect. Where this applies, **cap the level at
3 and add one sentence to the finding** naming what is missing:

> "The rule needs a data classification scheme, which does not exist here — so it
> is formally met and has no effect in practice."

It stays a `gap` or `strict` by its own logic. This mechanism only works with the
answers from § 3 F, which is why `extensive` finds things the other depths cannot.
Where `profile.has` is unknown, do not guess — score normally and disclose the
assumption.

### 5.7 Too strict — test against the norm, not the business

A rule answers flatly where the norm behind it grades. Example: "no customer data in
AI systems", where the GDPR asks for a legal basis and protection appropriate to the
data, and says nothing about a blanket ban.

The test is the norm: name the minimum the law sets, name what it leaves open, and
show the sentence in the policy that closes it. That holds without knowing the
client's systems.

**Do not rank these by business impact.** What an over-strict rule costs depends on
volumes, processes and strategy, none of which are in the document. Say that it is a
decision that can be revisited, and what the graduated version would look like.

### 5.8 Aggregation

- **Legal duties met** — count of active duties at level ≥ 4, over the total. A
  ratio, not a percentage.
- **Information security coverage** — the weighted mean of the usability levels
  across the data, model, use and infrastructure criteria, one decimal. Weight 3
  counts triple, weight 2 double, weight 1 once. N/A criteria count in neither the
  numerator nor the denominator.
- **AI governance coverage** — the same across the governance criteria. Kept
  separate on purpose: in practice the two diverge widely, and the gap is itself a
  statement.
- **Too strict** — the count of `strict` findings. Not weighted and not ranked.
- **Coverage per document** — per norm in the `law` and `standard` groups, the share
  of active criteria carrying that norm that reach level ≥ 4. Orientation, explicitly
  not a certification statement.
- **AI-specific risks covered** — of the OWASP categories this catalogue checks
  (`criteria.md` § "Which OWASP category each criterion covers"), how many are
  addressed. A category counts as **covered** where every criterion mapped to it
  reaches level ≥ 4, **partly** where at least one does, and **open** otherwise. Mark
  it `na` where the profile rules it out. The figure is `covered / (checked − na)`.

  **Why this one is reported by name and not as a bar.** OWASP is a community list of
  attack paths, not an obligation — nothing follows from a gap in law. A bar reading
  "1 of 3" next to "9 of 12 legal duties" invites the reader to treat them as the same
  kind of shortfall, and a denominator of 3 does not even describe the list it claims
  to. Naming each category with a status is both honest and more useful: a reader sees
  that prompt injection was checked and is not covered, which is actionable, instead
  of a ratio that is neither.

**No overall score in percent, and no single overall maturity number.** Two coverage
figures and a duty ratio say more than one blended number, which would only hide
the divergence that matters.

Translate each coverage figure into one word for the tile: **weak** below 2.5,
**partial** from 2.5 to 3.4, **solid** from 3.5 to 4.4, **strong** from 4.5.
