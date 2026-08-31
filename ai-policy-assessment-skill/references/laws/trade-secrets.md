# Trade secrets — GeschGehG (Germany), Directive (EU) 2016/943

> **Paraphrase, not wording, except where marked.** Section numbers and
> substance are the working reference; the text is a summary, never a quote —
> unless a `verbatim:` block says otherwise.
>
> Official text (GeschGehG): `https://www.gesetze-im-internet.de/geschgehg/`
> Official text (Directive): `https://eur-lex.europa.eu/eli/dir/2016/943/oj`
> Outbound fetches to these hosts are blocked by the environment's network
> policy, so neither was fetched by the skill itself.

> **Verified 2026-08-06.** The provisions discussed below — § 2 no. 1
> (definition), § 4 (prohibited acts), § 6 (injunctive relief), § 7
> (destruction/surrender/recall), § 8 (information claims), and § 23
> (criminal liability) — were checked against the official text (BGBl. I S.
> 466, 18.4.2019), pasted in by the user and compared line by line. The
> catalog cites only the bare acronym `GeschGehG`, no specific section, so
> this verification covers what this file already described rather than
> closing a catalog gap — see [Verbatim text](#geschgehg-verbatim-text)
> below. **Directive (EU) 2016/943 — the EU instrument GeschGehG
> transposes, named in this file's title — was not pasted and remains
> unverified.** Everything discussed in this file is GeschGehG's own,
> national-law wording; the Directive is background context only.

## The one provision that matters here

**GeschGehG § 2 no. 1** defines a trade secret. Protection requires, among other
things, that the information is **subject to appropriate confidentiality measures**
(*angemessene Geheimhaltungsmaßnahmen*). This is constitutive, not decorative: without
such measures the information is not a trade secret, and the protection is gone.

The consequence for an AI policy is direct and often missed. Pasting design data,
source code or a costing model into a tool whose terms permit the provider to use
inputs for training can amount to a failure of appropriate confidentiality measures.
The loss is not a fine — it is that the information stops being protectable, and with
it the ability to act against a competitor who ends up with it.

Related: **§ 4** prohibited acts, **§ 6 to § 8** injunctive relief, damages and
information claims, **§ 23** criminal liability. See
[Verbatim text](#geschgehg-verbatim-text) below for the pasted wording of each.

### GeschGehG verbatim text

Pasted from the official text and checked against the provisions named above.
Quotes are excerpts — the operative sentence(s) behind each provision, not the
full section.

**§ 2 no. 1 — Definition of a trade secret**

verbatim:
> "eine Information a) die weder insgesamt noch in der genauen Anordnung und
> Zusammensetzung ihrer Bestandteile den Personen in den Kreisen, die
> üblicherweise mit dieser Art von Informationen umgehen, allgemein bekannt
> oder ohne Weiteres zugänglich ist und daher von wirtschaftlichem Wert ist
> und b) die Gegenstand von den Umständen nach angemessenen
> Geheimhaltungsmaßnahmen durch ihren rechtmäßigen Inhaber ist und c) bei der
> ein berechtigtes Interesse an der Geheimhaltung besteht[…]"

**§ 4(1) and (2) — Prohibited acts**

verbatim:
> "(1) Ein Geschäftsgeheimnis darf nicht erlangt werden durch 1. unbefugten
> Zugang zu, unbefugte Aneignung oder unbefugtes Kopieren von Dokumenten,
> Gegenständen, Materialien, Stoffen oder elektronischen Dateien, die der
> rechtmäßigen Kontrolle des Inhabers des Geschäftsgeheimnisses unterliegen
> und die das Geschäftsgeheimnis enthalten oder aus denen sich das
> Geschäftsgeheimnis ableiten lässt, oder 2. jedes sonstige Verhalten, das
> unter den jeweiligen Umständen nicht dem Grundsatz von Treu und Glauben
> unter Berücksichtigung der anständigen Marktgepflogenheit entspricht. (2)
> Ein Geschäftsgeheimnis darf nicht nutzen oder offenlegen, wer 1. das
> Geschäftsgeheimnis durch eine eigene Handlung nach Absatz 1 Nummer 1 oder
> Nummer 2 erlangt hat, 2. gegen eine Verpflichtung zur Beschränkung der
> Nutzung des Geschäftsgeheimnisses verstößt oder 3. gegen eine Verpflichtung
> verstößt, das Geschäftsgeheimnis nicht offenzulegen."

**§ 6 — Injunctive relief**

verbatim:
> "Der Inhaber des Geschäftsgeheimnisses kann den Rechtsverletzer auf
> Beseitigung der Beeinträchtigung und bei Wiederholungsgefahr auch auf
> Unterlassung in Anspruch nehmen. Der Anspruch auf Unterlassung besteht auch
> dann, wenn eine Rechtsverletzung erstmalig droht."

**§ 7 — Destruction, surrender, recall**

verbatim:
> "Der Inhaber des Geschäftsgeheimnisses kann den Rechtsverletzer auch in
> Anspruch nehmen auf 1. Vernichtung oder Herausgabe der im Besitz oder
> Eigentum des Rechtsverletzers stehenden Dokumente, Gegenstände, Materialien,
> Stoffe oder elektronischen Dateien, die das Geschäftsgeheimnis enthalten
> oder verkörpern, 2. Rückruf des rechtsverletzenden Produkts[…]"

**§ 8(1) — Information claims**

verbatim:
> "Der Inhaber des Geschäftsgeheimnisses kann vom Rechtsverletzer Auskunft
> über Folgendes verlangen: 1. Name und Anschrift der Hersteller, Lieferanten
> und anderer Vorbesitzer der rechtsverletzenden Produkte sowie der
> gewerblichen Abnehmer und Verkaufsstellen, für die sie bestimmt waren[…]"

**§ 23(1) — Criminal liability**

verbatim:
> "Mit Freiheitsstrafe bis zu drei Jahren oder mit Geldstrafe wird bestraft,
> wer zur Förderung des eigenen oder fremden Wettbewerbs, aus Eigennutz,
> zugunsten eines Dritten oder in der Absicht, dem Inhaber eines Unternehmens
> Schaden zuzufügen, 1. entgegen § 4 Absatz 1 Nummer 1 ein Geschäftsgeheimnis
> erlangt, 2. entgegen § 4 Absatz 2 Nummer 1 Buchstabe a ein
> Geschäftsgeheimnis nutzt oder offenlegt oder 3. entgegen § 4 Absatz 2
> Nummer 3 als eine bei einem Unternehmen beschäftigte Person ein
> Geschäftsgeheimnis, das ihr im Rahmen des Beschäftigungsverhältnisses
> anvertraut worden oder zugänglich geworden ist, während der Geltungsdauer
> des Beschäftigungsverhältnisses offenlegt."

## What this means for the assessment

1. **This is why "which tools may be used" is not merely an IT question.** A
   positive list with checked terms of use is a confidentiality measure. An informal
   tolerance of whatever staff have installed is the opposite, and it is visible in
   the policy or not at all.
2. **Activate on data types, not on sector.** Where `profile.data_types` includes
   design data, source code, or customer data under NDA, the criteria that reference
   this act become duties. A mechanical engineering group with CAD data is the
   textbook case.
3. **Customer data under NDA carries a second duty.** Beyond the statute there is the
   contract. A policy that permits customer data in a tool whose terms allow training
   may breach an NDA independently of the GeschGehG, and that is a contractual
   exposure the report should name separately.
4. **The finding is about evidence of measures, not about strictness.** A graduated
   rule — this class of data in a contractually secured tenant, that class nowhere —
   is a *better* confidentiality measure than a blanket ban nobody follows, because
   it is the one that survives contact with the working day.
