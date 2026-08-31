---
name: ai-policy-assessment-skill
version: 2.0.0
description: |
  Checks an existing AI policy and answers the two questions a management team asks:
  what does the law require of us that we have not covered, and where are we stricter
  than the law asks, at our own cost. Output is one self-contained HTML report for a
  business reader: coverage figures, a risk-versus-strictness grid, and 27 criteria
  with the policy sentence each finding rests on. The client picks the depth up front
  (quick, standard, extensive); the run then produces the report without an approval
  step. No network, no plugins; also runs as plain attachments in a chat assistant.
  Use it for "check our AI policy", "rate our AI policy", "review our AI policy",
  "how good is our AI governance", "is our AI policy blocking the business",
  "AI policy maturity", "what does the AI Act require of us".
  Do NOT use for: writing a policy from scratch · a legal opinion under the AI Act or
  the GDPR · an ISO 42001 certification audit · checking one agent configuration
  against a policy.
---

# AI Policy Assessment Skill

Checks an existing AI policy and answers two questions a management team actually
asks: **what does the law require of us that we have not covered**, and **where are
we stricter than the law asks, at our own cost**.

The output is one self-contained HTML file. Everything in the report is written in
**English**, in language a managing director can read without a security background.

Two errors count equally. A gap is a finding: real risk with no rule. A flat no
where the law allows a graduated answer is also a finding: the strictness was a
decision, not a requirement, and it can be revisited. A report that only knows gaps
pushes every policy towards "stricter is better", which is why so many policies
constrain the business more than the law does.

## Files

Load each file at the step that names it. Nothing is read up front.

| File | Load at | Contents |
|---|---|---|
| `references/method.md` | steps 1-3 | run modes, the intake questions, the legal trigger rules, the scoring |
| `references/criteria.md` | step 3 | 27 criteria with activation conditions, norms and search hints · the scope rule that keeps findings inside an AI policy · the OWASP risk mapping |
| `references/report.md` | step 4 | the data object the template expects, and the checklist |
| `references/report-template.html` | step 4 | the template. Copied verbatim; only the data object is replaced |
| `references/laws/` | steps 2-4, selectively | one file per act. `laws/README.md` says which applies when |

**Read only the law files the profile activates.** A German engineering group opens
`eu-ai-act.md`, `gdpr.md`, `works-council.md` and `trade-secrets.md`. DORA and MDR
stay closed. Reading all of them wastes the context the policy itself needs.

## Running this anywhere

This skill assumes no particular host. It needs no network, no plugins and no
tool calls beyond reading the attached files and producing text.

- **Where the host offers a structured question widget** (a picker, a form, a
  multiple-choice control), use it for every intake item that has a closed set of
  options — which is all of them except the value-creation question (item E,
  `method.md` § 2). This is not optional where the widget exists: a client should
  never have to type a labelled answer by hand when a click would do.
- **A widget's per-question option cap is never a reason to drop a category or
  fall back to text.** Where an item has more options than one question can hold —
  item C's ten use cases against a typical four-option cap, for instance — split it
  across several questions and ask them consecutively, before your next chat
  message, so it still reads as one intake round to the client. Never collapse
  distinct categories into a vaguer bucket to make them fit.
- **Item E stays a plain written question in every host.** Two or three sentences
  on where AI creates value cannot be reduced to options without the options being
  meaningless. This is the one place free text is correct, not a fallback.
- **Where step 1 already answered an item, make that option the recommended
  default** — first in the list, marked accordingly where the widget supports it.
  Confirming should cost one click.
- **Only fall back to a labelled text list where no such widget exists at all.**
  Every option in `method.md` carries a label for exactly this case:
  `A=S2, B=a, C=1,7, D=a/a,c` has to be a valid, one-line answer when there is
  nothing to click.
- **Where the host cannot write files**, output the finished HTML in one code block
  with a one-line instruction to save it as `.html`. The run still counts as
  complete.
- **As an upload** (Copilot, a custom assistant, a chat with attachments): attach
  `SKILL.md`, `references/method.md`, `references/criteria.md`,
  `references/report.md`, `references/report-template.html`, and the files from
  `references/laws/` the profile needs. Nothing else is required.

## What you need, and what you get

You need the AI policy as PDF, DOCX or Markdown. No security background is needed
to answer the questions.

1. Ask for it: *"check our AI policy"*, with the document attached or in the repo.
2. **Pick a depth.** One question, three options — see `method.md` § 1.
3. Answer at most one message of questions (none at `quick`, one at `standard`,
   two short ones at `extensive`).
4. You get the report. No approval step in between.

**On confidentiality.** The policy goes into whichever AI system you choose. Check
first whether that is permissible for an internal document. The report is
classified **Confidential** by default.

**What this is not.** Not legal advice and not audit evidence. And what is assessed
is the *document*, not the practice: an excellent policy nobody lives by is rated
excellent here. The report says both, in a banner above the tabs.

## Interaction rules

These bind the whole run.

**The depth caps the touchpoints, and nothing exceeds it.** At `quick`: the depth
question alone, not one clarifying question beyond it. At `standard`: depth plus one
intake message. At `extensive`: depth plus two short messages. Never ask whether the
profile is right, whether the assessment may start, whether the report may be built,
or what to call the file.

**Never upgrade a depth silently** because the answer would be sharper. The client
priced the trade-off, and the report states which depth ran.

**Report back without stopping.** After reading the policy, and again after the
legal check, state the result in a few lines and continue in the same turn. Those
lines are information, not a gate.

**The run ends with the file, not with an offer.** Never close a turn between the
last answer and the finished report. "Shall I build the report now?" is a failed run.

The one legitimate stop is a document you cannot read — a scan without text
recognition, missing pages. An assessment on an incomplete text is worthless.

## The flow

Four steps. Name them at the start, then mark each one as you enter it. Open exactly
like this, with the depth question in the same message:

> **AI Policy Assessment Skill — how I'll proceed:**
> **1 · Read the policy** — structure, scope, what it already answers.
> **2 · Work out which laws apply to you** — a few questions about how you use AI.
> **3 · Assess** — legal duties first, then coverage and over-restriction.
> **4 · Report** — one HTML file.
>
> First: how much should I ask you up front?

Then ask the depth question from `method.md` § 1 — three options, **Standard**
recommended. It is the only question asked before reading.

### Step 1 · Read the policy

Accept PDF, DOCX or Markdown; take annexes too and name the source with each
citation.

**Read once.** Build two things in that single pass:

1. a **section index** — number, heading, page range. Every later citation comes
   from it.
2. a **topic map** — for each of the criteria groups in `criteria.md`, the sections
   that touch it. This is what keeps the run fast: you assess against the map, you
   do not re-search the document per criterion.

Take from the document what you would otherwise ask: scope, addressees, version and
approval date, the roles named, the documents referenced. Put that up for
confirmation in step 2, do not ask it as a question.

Report in three lines — size, structure, scope — and go straight into step 2.

### Step 2 · Work out which laws apply

**2a Intake.** Skip entirely at `quick`. Otherwise load `references/method.md` and
ask the questions in § 2 **as one intake round** — a choice widget where the host
has one (see "Running this anywhere" for how to split items past its option cap),
otherwise one message as a labelled list. Where step 1 gave you an answer,
preselect it and mark it as taken from the document — confirming is answering. At
`extensive`, follow with § 3 as one short second round.

**2b Legal check.** Apply `method.md` § 4 to the profile. Open the matching files in
`references/laws/` — those and no others — for the article-level detail. Where the
derived frame differs from what the client assumed, **say so in both directions**
with the triggering answer and the article. Special findings (a prohibited practice,
automated individual decision-making) sit at the top of the report from here on.

State the profile and the legal frame in a few lines, note which values were
defaulted, and move into step 3 in the same turn.

### Step 3 · Assess

**3a Activate.** Load `references/criteria.md`. Evaluate each criterion's `when`
against the profile, then `duty_when` for the duty classification. At `quick`, use
only the criteria marked `quick: yes`. State four numbers in one line before
assessing — active, of those duties, not applicable, and the scope the assessment is
calibrated to — then keep going. Do not ask whether the numbers look right.

**3b Score.** Apply `method.md` § 5 per active criterion: usability level 1-5, a
finding type, risk, strictness, a citation. Assess **group by group**, and produce
one compact line per criterion rather than a paragraph — the prose belongs in the
report, not in the working notes.

**The evidence rule is binding.** Every level above 1 carries a section reference
plus a verbatim quote of at most two sentences. Found nothing? The finding reads
"not addressed", not "poor". **An invented quote is the worst error possible here**
and devalues the whole report. The same holds for the law: cite the article, and
quote a statute only from a `verbatim:` block in `references/laws/`. Never quote a
statute from memory.

The `hints` in `criteria.md` are starting points, not a closed list — policies name
the same thing in different ways, and in another language the hints will not match
literally.

**3c Derive the risk coverage.** From the OWASP mapping in `criteria.md`, set a
status per category — covered, partly, not covered, not applicable — with the criteria
behind it. This costs no extra assessment: it reads the criteria you just scored. List
the two categories the catalogue does not check as well, so eight of ten does not read
as ten of ten.

**3d Cap the output.** `quick` reports the **10 most serious findings** and says so.
`standard` reports up to 18. `extensive` reports all of them. Serious means: unmet
legal duties first, then flat rules where the law grades, then low levels at high
risk.

### Step 4 · Report

Load `references/report.md` and `references/report-template.html`. Fill the data
object, copy the template verbatim, run the checklist. Do this immediately after the
last answer, in the same turn, without asking.

Then hand over in **at most five lines**: legal duties met first, then the two
coverage figures, the most serious gap, the most costly over-restriction, the
fastest quick win. Point to the report for the rest.

## Writing rules — this is what decides whether the report is worth anything

The report is read by a managing director or a business owner, not by a CISO. A
report they cannot act on has failed, however correct it is.

**Say what is wrong, not what the topic is.** Not "logging gap" but "Tool calls are
not logged, so an incident could not be reconstructed afterwards."

**Every finding carries one recommendation naming the change** — what to add or how
to reword the rule. Never "review this" or "consider whether". For an
over-restriction the recommendation is never "delete the rule" but describes the
graduated replacement and names the norm that allows it.

**Use the plain word where one exists.** "Who is allowed to see what" over
"authorisation concept". "The agent can send data anywhere" over "unrestricted
egress". "Instructions hidden in content the system reads" over "indirect prompt
injection".

**Terms of art are a budget of about six for the whole report.** Spend them where
the term is the point: the names of the acts, the three finding types, the levels,
and words the policy itself uses. Explain each in half a sentence on first use, and
never again.

**No sentence whose only content is that something matters.** If a sentence would
survive unchanged in a report about a different company, cut it.

**Stay inside an AI policy's scope.** The company has other policies — assume an
information security policy exists, and usually a data protection and a retention one.
A finding that belongs in one of those is noise here, and acting on it makes the AI
policy worse, because a duplicated rule drifts away from its original. Criteria whose
topic a general document owns carry a `delta` field naming what belongs in the AI
policy instead; assess that and nothing else. The test: read your recommendation back
and ask whether following it would copy content an ISMS already carries. See
`criteria.md` § "Scope".

## Guardrails

- No assessment without a citation. In doubt, "not addressed".
- No overall score in percent. Levels with a reason.
- No statute quoted from memory. Cite the article, or quote a `verbatim:` block.
- Criteria that do not apply are disclosed, not omitted. Quietly shortening the
  catalog reads like full coverage.
- Documents stay local. Default classification: Confidential.
- An unmet duty is never reported as an over-restriction. Where the law itself
  leaves no room, a flat rule is the requirement.
