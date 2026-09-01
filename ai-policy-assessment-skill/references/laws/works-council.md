# Works council law — BetrVG (Germany), ArbVG (Austria)

> **Paraphrase, not wording, except where marked.** Section numbers and substance
> are the working reference; the text is a summary, never a quote — unless a
> `verbatim:` block says otherwise.
>
> Official text (BetrVG): `https://www.gesetze-im-internet.de/betrvg/`
> Official text (ArbVG): `https://www.ris.bka.gv.at/`
> The environment's network policy blocks outbound fetches to these hosts, so
> neither was fetched by the skill itself. **Both were pasted in by the user
> and are verified** — BetrVG for the 6 provisions listed in its section below,
> ArbVG for the 4 provisions listed in its section below — see
> [BetrVG verbatim text](#betrvg-verbatim-text) and
> [ArbVG verbatim text](#arbvg-verbatim-text). This file is now fully
> verified end to end.

**In the DACH region this is what stops rollouts.** Not the AI Act, not the GDPR —
those produce findings and deadlines. A missing works council agreement produces an
injunction, and the rollout is contestable regardless of how good the security is.
Activate whenever `profile.jurisdiction` includes Germany or Austria and there are
employees.

## Germany — BetrVG

> **Verified 2026-08-06.** The provisions behind every row in the table below —
> § 87(1) no. 1 and no. 6, § 90, § 92, § 95, § 80(2) — were checked against the
> official consolidated text (Bekanntmachung vom 25.9.2001, last amended by
> Gesetz vom 19.7.2024), pasted in by the user and compared line by line —
> network access to `gesetze-im-internet.de` is still blocked from this
> environment, so this was not fetched by the skill itself. The catalog cites
> `BetrVG § 87`, which matches the two existing § 87 rows exactly, so this
> closes no gap beyond confirming them — see
> [Verbatim text](#betrvg-verbatim-text) below. The Austria (ArbVG) section
> below is verified separately — see its own banner.

| Section | Substance | Trigger in an AI policy |
|---|---|---|
| **§ 87(1) no. 6** | co-determination on the introduction and use of technical devices **designed to monitor** the behaviour or performance of employees | the load-bearing one. "Designed to" is objective: a system that *can* monitor is enough, intent is not required. Logging of AI interactions per user falls under it |
| **§ 87(1) no. 1** | co-determination on rules of conduct in the establishment | an AI policy that tells employees how to work is itself a matter for co-determination |
| **§ 90** | information and consultation on planning of technical plant, procedures and workflows, in good time — since the 2024 amendment, the statute names the use of AI explicitly as part of what must be planned and disclosed | applies **before** the rollout, not after. Skipping it is the most common procedural defect |
| **§ 92** | information on personnel planning | AI in workforce planning |
| **§ 95** | selection guidelines for hiring, transfer and dismissal require consent — since the 2024 amendment, consent is required by name when AI is used to draw up those guidelines | AI-supported applicant screening produces a selection guideline in substance, whatever it is called internally |
| **§ 80(2)** | works council information rights, including access to expertise — § 80(3) now deems an expert necessary by name whenever the works council must assess the introduction or use of AI | the basis for the questions the works council will ask about the model |

**2024 amendment note.** The Gesetz vom 19. Juli 2024 inserted three explicit
references to "Künstliche Intelligenz" into BetrVG that were not there before:
§ 90(1) no. 3 (the planning-information duty now names AI by name among
"Arbeitsverfahren und Arbeitsabläufen"), § 95(2a) (selection-guideline consent
applies "wenn bei der Aufstellung der Richtlinien... Künstliche Intelligenz
zum Einsatz kommt"), and § 80(3) sentence 2 (an expert is deemed necessary
whenever the works council must assess "die Einführung oder Anwendung von
Künstlicher Intelligenz"). Before this amendment, BetrVG's application to AI
rested entirely on interpreting "designed to" monitor; three of the six rows
above are now anchored to AI by name in the statute itself, not just by
inference.

### BetrVG verbatim text

Pasted from the official text and checked against the provisions named above.
Quotes are excerpts — the operative sentence(s) behind each table row, not the
full section.

**§ 87(1), introductory clause and no. 6 — Co-determination on monitoring technology**

verbatim:
> "Der Betriebsrat hat, soweit eine gesetzliche oder tarifliche Regelung nicht
> besteht, in folgenden Angelegenheiten mitzubestimmen: […] 6. Einführung und
> Anwendung von technischen Einrichtungen, die dazu bestimmt sind, das
> Verhalten oder die Leistung der Arbeitnehmer zu überwachen[…]"

**§ 87(1) no. 1 — Co-determination on rules of conduct**

verbatim:
> "1. Fragen der Ordnung des Betriebs und des Verhaltens der Arbeitnehmer im
> Betrieb;"

**§ 90(1) and (2) — Information and consultation on planning, including AI**

verbatim:
> "(1) Der Arbeitgeber hat den Betriebsrat über die Planung […] 3. von
> Arbeitsverfahren und Arbeitsabläufen einschließlich des Einsatzes von
> Künstlicher Intelligenz oder […] rechtzeitig unter Vorlage der erforderlichen
> Unterlagen zu unterrichten. (2) Der Arbeitgeber hat mit dem Betriebsrat die
> vorgesehenen Maßnahmen und ihre Auswirkungen auf die Arbeitnehmer […] so
> rechtzeitig zu beraten, dass Vorschläge und Bedenken des Betriebsrats bei der
> Planung berücksichtigt werden können."

**§ 92(1) — Information on personnel planning**

verbatim:
> "Der Arbeitgeber hat den Betriebsrat über die Personalplanung, insbesondere
> über den gegenwärtigen und künftigen Personalbedarf sowie über die sich
> daraus ergebenden personellen Maßnahmen […] anhand von Unterlagen rechtzeitig
> und umfassend zu unterrichten. Er hat mit dem Betriebsrat über Art und Umfang
> der erforderlichen Maßnahmen und über die Vermeidung von Härten zu beraten."

**§ 95(1) and (2a) — Selection guidelines, including where AI draws them up**

verbatim:
> "(1) Richtlinien über die personelle Auswahl bei Einstellungen, Versetzungen,
> Umgruppierungen und Kündigungen bedürfen der Zustimmung des Betriebsrats.
> […] (2a) Die Absätze 1 und 2 finden auch dann Anwendung, wenn bei der
> Aufstellung der Richtlinien nach diesen Absätzen Künstliche Intelligenz zum
> Einsatz kommt."

**§ 80(2) and (3) — Information rights and access to expertise, including on AI**

verbatim:
> "(2) Zur Durchführung seiner Aufgaben nach diesem Gesetz ist der Betriebsrat
> rechtzeitig und umfassend vom Arbeitgeber zu unterrichten […] Dem Betriebsrat
> sind auf Verlangen jederzeit die zur Durchführung seiner Aufgaben
> erforderlichen Unterlagen zur Verfügung zu stellen[…] (3) Der Betriebsrat
> kann bei der Durchführung seiner Aufgaben nach näherer Vereinbarung mit dem
> Arbeitgeber Sachverständige hinzuziehen, soweit dies zur ordnungsgemäßen
> Erfüllung seiner Aufgaben erforderlich ist. Muss der Betriebsrat zur
> Durchführung seiner Aufgaben die Einführung oder Anwendung von Künstlicher
> Intelligenz beurteilen, gilt insoweit die Hinzuziehung eines Sachverständigen
> als erforderlich."

## Austria — ArbVG

> **Verified 2026-08-06.** The provisions behind every row in the table below —
> § 96(1) Z 3, § 96a(1) Z 1, § 91, § 92a — were checked against the official
> consolidated text (Fassung vom 06.08.2026), pasted in by the user and
> compared line by line — network access to `ris.bka.gv.at` is still blocked
> from this environment, so this was not fetched by the skill itself. The
> catalog cites `ArbVG § 96a`, which matches the existing § 96a(1) Z 1 row
> exactly, so this closes no gap — see
> [Verbatim text](#arbvg-verbatim-text) below. **A distinction worth
> flagging: § 96(1) Z 3's consent is absolute** — the text gives the works
> council no override mechanism, so "without agreement the measure is
> impermissible" holds exactly as this file already said. **§ 96a is
> explicitly titled "Ersetzbare Zustimmung" (replaceable consent)** — § 96a(2)
> states the Schlichtungsstelle (arbitration board) can substitute its own
> decision for the works council's withheld consent. The two rows are not the
> same strength of instrument, and the table's wording did not previously
> distinguish them. Unlike BetrVG, this consolidated text names no
> "Künstliche Intelligenz" anywhere — ArbVG's connection to AI rests entirely
> on interpretation ("technical systems," "new technologies"), the same
> position BetrVG was in before its 2024 amendment. **The Germany (BetrVG)
> section above is unaffected by this and remains independently verified.**

| Section | Substance |
|---|---|
| **§ 96(1) Z 3** | control measures and technical systems touching human dignity require the works council's **consent, with no override** — a stronger instrument than the German co-determination right: without agreement the measure is impermissible |
| **§ 96a(1) Z 1** | personal data systems going beyond general job data require consent — but this consent is explicitly **replaceable** by the Schlichtungsstelle (§ 96a is titled "Ersetzbare Zustimmung"), unlike § 96(1) Z 3's absolute consent |
| **§ 91** | information rights, including disclosure of what personal employee data is processed automatically and how |
| **§ 92a** | consultation on the introduction of new technologies and their effects on safety and health, including workplace design |

### ArbVG verbatim text

Pasted from the official text and checked against the provisions named above.
Quotes are excerpts — the operative sentence(s) behind each table row, not the
full section.

**§ 96(1) Z 3 — Consent for control measures touching human dignity**

verbatim:
> "Folgende Maßnahmen des Betriebsinhabers bedürfen zu ihrer Rechtswirksamkeit
> der Zustimmung des Betriebsrates: […] 3. die Einführung von
> Kontrollmaßnahmen und technischen Systemen zur Kontrolle der Arbeitnehmer,
> sofern diese Maßnahmen (Systeme) die Menschenwürde berühren[…]"

**§ 96a(1) Z 1 and (2) — Replaceable consent for personal data systems**

verbatim:
> "Folgende Maßnahmen des Betriebsinhabers bedürfen zu ihrer Rechtswirksamkeit
> der Zustimmung des Betriebsrates: 1. Die Einführung von Systemen zur
> automationsunterstützten Ermittlung, Verarbeitung und Übermittlung von
> personenbezogenen Daten des Arbeitnehmers, die über die Ermittlung von
> allgemeinen Angaben zur Person und fachlichen Voraussetzungen
> hinausgehen[…] (2) Die Zustimmung des Betriebsrates gemäß Abs. 1 kann durch
> Entscheidung der Schlichtungsstelle ersetzt werden."

**§ 91(1) and (2) — Information rights, including on automated data processing**

verbatim:
> "(1) Der Betriebsinhaber ist verpflichtet, dem Betriebsrat über alle
> Angelegenheiten, welche die wirtschaftlichen, sozialen, gesundheitlichen
> oder kulturellen Interessen der Arbeitnehmer des Betriebes berühren,
> Auskunft zu erteilen. (2) Der Betriebsinhaber hat dem Betriebsrat Mitteilung
> zu machen, welche Arten von personenbezogenen Arbeitnehmerdaten er
> automationsunterstützt aufzeichnet und welche Verarbeitungen und
> Übermittlungen er vorsieht. Dem Betriebsrat ist auf Verlangen die
> Überprüfung der Grundlagen für die Verarbeitung und Übermittlung zu
> ermöglichen."

**§ 92a(1) — Consultation on new technologies and workplace design**

verbatim:
> "Der Betriebsinhaber hat den Betriebsrat in allen Angelegenheiten der
> Sicherheit und des Gesundheitsschutzes rechtzeitig anzuhören und mit ihm
> darüber zu beraten. Der Betriebsinhaber ist insbesondere verpflichtet, 1.
> den Betriebsrat bei der Planung und Einführung neuer Technologien zu den
> Auswirkungen zu hören, die die Auswahl der Arbeitsmittel oder Arbeitsstoffe,
> die Gestaltung der Arbeitsbedingungen und die Einwirkung der Umwelt auf den
> Arbeitsplatz für die Sicherheit und Gesundheit der Arbeitnehmer haben[…]"

## The AI Act connection

Art. 26(7) of the AI Act requires deployers who are employers to inform workers'
representatives and affected workers **before** putting a high-risk AI system into use
at the workplace. That is an information duty layered on top of national
co-determination, not a substitute for it. A policy that mentions neither has two
findings, not one; a policy that mentions only Art. 26(7) has met the smaller of the
two duties.

## What this means for the assessment

1. **This is a duty, never a design question.** Where employees are in scope, a
   missing works council path is `duty` in the catalog and appears among the
   statutory minimum requirements.
2. **Per-user logging is the usual trigger.** Where a policy mandates audit-proof
   logging of AI interactions and says nothing about co-determination, name the
   connection explicitly — the logging requirement created the obligation.
3. **Timing is the finding, not just presence.** § 90 is about being informed in
   good time. A policy that involves the works council after rollout decisions have
   been taken satisfies the letter and loses the injunction.
4. **Do not draft the agreement.** The report names the gap and the section. What the
   agreement should say is the next engagement, and outside what a document review
   can responsibly claim.
