# Workflow 6 — Lint

Goal: run a periodic hygiene pass over the Cortex to catch
contradictions, staleness, broken pointers, aged TODOs, and orphan
files **before** they corrode trust in the artifact. Lint is
diagnostic — it reports, it does not silently fix.

---

## 6.1 — What to check

Run the checks below. Produce one finding per issue, not one
finding per category. Categorise each finding by severity:

For mature Cortexes, run lint in chunks rather than one giant pass:

1. structural file/tree checks;
2. frontmatter and provenance checks;
3. link/index/orphan checks;
4. staleness, confidentiality, and derived-artifact checks;
5. semantic checks such as contradiction and routing.

After each chunk, keep a short scratch list of findings and continue.
For very large Cortexes, pause after each chunk and show counts by
severity before continuing. Use code execution helpers for mechanical
checks such as hashes, YAML parsing, duplicate pointer IDs, local path
existence, and markdown link validation.

- **blocker** — the Cortex is actively misleading (contradiction
  between Layer 1 files, a Layer 3 artifact contradicts current
  Layer 1, a pointer references a resource that no longer exists,
  two pages contain incompatible facts about the same thing).
- **warning** — the Cortex is stale or inconsistent but not
  actively wrong (Layer 3 artifact whose input hashes have
  changed; TODO older than 90 days; an open question older than
  60 days that has not been touched; a concept page that has no
  Description filled in).
- **nit** — style or hygiene issues (missing change-log entry on
  a modified Layer 1 file; missing `description` on a Layer 4
  pointer; date format deviations; file with no inbound links
  from anywhere; concept page with no cross-links).

### Per-layer checks

**Layer 1 — skeleton files (`identity.md`, `scope.md`,
`context.md`)**

- Every skeleton file has a `## Change Log` section.
- Each claim in a skeleton file either (a) has a pointer
  reference, (b) links to an entity or concept page, or (c)
  carries a `TODO:` marker. No bare claim without provenance or
  TODO.
- No TODO marker older than 90 days. TODOs should use
  `TODO(YYYY-MM-DD): ...`; undated TODOs are nits because they cannot
  be aged reliably.
- No open question from `02-working-memory/open-questions.md` has
  silently become a Layer 1 fact without an explicit `[resolved
  YYYY-MM-DD: ...]` entry in the open-questions file.
- Skeleton files do not contain rich entity or concept blurbs that
  should have been their own pages. If a skeleton file has more
  than ~3 sentences about a named entity or named mechanism, flag
  as **warning: content in skeleton — promote to
  `entities/{slug}.md` or `concepts/{slug}.md`**.

**Layer 1 — entity pages (`01-canonical/entities/*.md`)**

- Every entity page has valid frontmatter (`kind: entity`,
  `entity_type` one of the allowed enum, `first_seen`, `sources`).
  Missing or invalid frontmatter → **blocker**.
- Every entity page has a non-empty identity-facts section with at
  least one identity fact (role, registration number, location,
  ticker, employee-id — varies by entity_type). Empty identity
  facts → **warning**.
- Every entity page has at least one outbound cross-link (to
  another entity, a concept, or a skeleton file). Zero
  cross-links → **nit: likely orphan entity**.
- No duplicate entity pages (e.g. `acme-corp.md` and
  `acmecorp.md` for the same firm). Use `aliases:` to declare
  alternative names; lint flags duplicate aliases pointing at
  different files as **blocker**.
- Entity slug stability: if the Change Log shows the slug was
  renamed, flag as **nit** unless `aliases:` carries the prior
  slug.
- An entity that has not been touched in 365 days and is not
  marked `status: archived` → **nit: stale entity, consider
  archiving**.

**Layer 1 — concept pages (`01-canonical/concepts/*.md`)**

- Every concept page has valid frontmatter (`kind: concept`,
  `first_seen`, `sources`).
- Every concept page has a non-empty Description section. An
  empty Description is a **warning**.
- Every concept page has at least one outbound cross-link.
  Zero → **nit: likely orphan**.
- No duplicate concept pages describing the same thing without
  one redirecting to the other.
- Every concept page that names a non-trivial design choice
  should have a Trade-offs section. Missing on a clearly
  design-bearing concept → **nit**.

**Layer 1 — spine files (`overview.md`, `synthesis.md`,
`index.md`)**

- All three files exist. Missing → **blocker** (the Cortex was
  not initialised correctly or someone deleted them).
- `index.md` lists every entity page under
  `01-canonical/entities/`, every concept page under
  `01-canonical/concepts/`, and every active source summary
  under `01-canonical/sources/`. Entity, concept, or source
  files not appearing in `index.md` → **warning: missing from
  index**. Index entries pointing to files that no longer exist
  → **blocker: broken index entry**.
- **Synthesis material-staleness check.** Compute content hashes
  of all entity and concept pages whose `Change Log` shows a
  material edit since `synthesis.md`'s last Change Log entry.
  If any of those pages reference design choices, parameter
  calibrations, or risks that `synthesis.md` does not currently
  acknowledge, flag as **warning: stale synthesis — material
  changes since last synthesis update**. Do **not** flag based
  on mtime alone — `synthesis.md` is allowed to be untouched if
  its content is still accurate.
- `overview.md` references all currently in-scope skeleton
  files and the most prominent concept clusters. Pointers to
  files that no longer exist → **blocker**.

**Layer 1 — source summaries (`01-canonical/sources/*.md`)**

- Every Ingest log entry in `02-working-memory/log/` has a
  matching source summary in `01-canonical/sources/`. Ingest
  with no summary → **warning: missing source summary**.
- Every source summary has frontmatter pointing back to a Layer
  4 pointer via `sources:` and lists generated pages under
  Generated entity pages and Generated concept pages sections.
  Legacy `source_path:` (pre-1.0) is accepted but flagged as
  **warning: legacy source_path key — migrate to sources list** for
  one skill version; it becomes a blocker in the next major bump.
- Source summaries that list zero generated entity *and* concept
  pages → **warning: under-ingested** (see also fan-out sanity
  below).
- Source summaries referencing entity or concept pages that no
  longer exist → **blocker: broken source-to-page link**.

**Case root — `CLAUDE.md`**

- File exists at the case root. Missing → **blocker** (the
  Cortex was not initialised correctly; the LLM has no per-case
  operating manual).
- Has all eleven sections from the template (Purpose, Pointer to
  generic schema, Language convention, Domain conventions,
  Workflow tweaks, Jurisdictional defaults, Tone and bias, Open
  items, Source isolation reminder, Concurrency and Git, Change Log). Missing
  sections → **nit**, except Change Log missing → **warning**.
- The Change Log section has at least one entry. Empty → **nit**.
- Conventions stated in `CLAUDE.md` are not silently
  contradicted by practice in the Cortex (best-effort heuristic
  — e.g. if section 3 says "this Cortex is in German" but half
  the entity pages are in English, flag as **warning:
  convention drift between CLAUDE.md and pages**).

**Layer 2 (working memory)**

- `decisions.md` is append-only for substantive content. If a
  git history is available, check no prior decision blocks have
  been removed. If git is not available, the check is best-effort
  and noted in "Not checked".
- `open-questions.md` contains no duplicate questions.
- Every log file in `02-working-memory/log/` follows
  `YYYY-MM-DD-{slug}.md`.
- No log entry older than 180 days that still contains an open
  next-step without a follow-up log referencing it.

**Layer 3 (derived)**

- Every artifact has the provenance frontmatter
  (`generated_at`, `generator`, `inputs`, `kind`).
- For each input listed, **re-compute the input file's current
  hash** using the stored `hash_mode` and compare against the stored
  hash in the artifact's frontmatter. If a `material-v1` hash differs,
  flag the artifact as **warning: stale** and list the changed inputs.
  If a `raw` hash differs, flag **warning: conservative raw-hash stale
  check** and note that non-substantive edits may be the cause.
  Missing `hash_mode` is treated as `raw` for backward compatibility.
- If neither content hash nor commit hash is available (the
  artifact was generated under the date-only fallback), note
  this in "Not checked" rather than firing a false warning.
- No artifact directly contradicts current Layer 1 (cross-check
  claims on a best-effort basis).
- Declared artifact confidentiality is at least as strict as the
  strictest listed input. The exception is a redacted downgrade:
  - If declared confidentiality is below the strictest input **and**
    `redaction: applied` is set with non-empty `redaction_notes`, flag
    as **warning: confidentiality downgrade with redaction — confirm
    the redaction is sufficient** (so a reviewer signs off, but it is
    not blocking).
  - If declared confidentiality is below the strictest input **and**
    `redaction:` is missing/`none`, flag **blocker: confidentiality
    downgrade**.
  - If `redaction: applied` but `redaction_notes` is missing or empty,
    flag **warning: redaction applied without notes**.
- Artifacts in `_archive/` are not lint-checked for staleness
  (they are by definition superseded).

**Layer 4 (pointers)**

- Every pointer has an `id`, a `url` (or equivalent locator),
  and a `description`.
- Every pointer `id` is unique.
- Where the pointer is a local path, the path exists.
- For remote pointers, do not HTTP-check by default; flag only
  if the user asks for a network lint.

### Cross-cutting checks

- **Source-isolation check** — every entity page, concept page,
  and source summary must trace its content to either a Layer 4
  pointer or a dated Layer 2 log entry in its `sources:` frontmatter.
  Layer 4 pointers must correspond to something the user actually
  provided in a conversation (a document path, a URL, connected tool
  resource). Layer 2 log entries are valid only when they record an
  explicit user assertion. Flag any of the following as **blocker**:
  - Entity or concept page with empty `sources:` frontmatter and
    no `TODO: source` marker on the page itself.
  - Page citing a source pointer-id that does not exist in
    `04-pointers/`, or a user-assertion log path that does not exist
    in `02-working-memory/log/`.
  - Pointer entry with a `description` that suggests it was
    inferred or borrowed from outside the case (e.g. references a
    document the user never named, references a tool the user
    never connected, references a system the case has not
    explicitly engaged).
  - Specific named entities or KPIs on Layer 1 pages that have
    *no* corresponding source — i.e. a content fact that was
    "just written" rather than ingested from a user-provided
    source. This is the classic contamination symptom: a page
    appears with detailed facts but no pointer in `sources:`
    explains where the facts came from.

  When the lint detects a likely contamination, the report lists
  the suspect pages, the missing or suspicious provenance, and
  asks the user to confirm whether the content belongs.

- **Orphan check** — every file under the case directory should
  be reachable from at least one other file via a relative link,
  or be a well-known top-level file (`CLAUDE.md`, `README.md`,
  `cortex.yaml`, skeleton Layer 1 files, spine files). Flag
  unlinked files as **nit: orphan**. Entity and concept pages
  with no inbound links are particularly suspect. Files in
  `_archive/` are exempt from orphan checking.
- **Contradiction scan** — heuristic pass looking for pairs of
  claims that appear to contradict (same entity in two pages
  with divergent facts; concept page with a definition that
  differs from a skeleton-file summary; entity page identity
  facts contradicting the source summary that mentioned them);
  report as **blocker**.
- **Concept-vs-entity routing** — heuristic pass looking for
  pages that appear to be in the wrong directory: a
  `concepts/{slug}.md` whose content describes a named
  real-world thing with identity (identity facts, role,
  location) belongs in `entities/`; an `entities/{slug}.md` that
  describes only a mechanism or definition belongs in
  `concepts/`. Report as **warning: likely mis-routed**.
- **Fan-out sanity** — for any ingest log entry in Layer 2,
  count the entity *and* concept pages it produced. If an
  ingest touched 10+ pages of source content but only 1–2 pages
  exist across both directories, flag as **warning:
  under-ingested**. The fix is to re-run Ingest with better
  enumeration.
- **Date-format hygiene** — all dates in markdown content should
  be `YYYY-MM-DD`. Flag deviations as **nit**.
- **Confidentiality propagation** — frontmatter confidentiality values
  should use `public`, `internal`, `restricted`, or `confidential`.
  Derived artifacts inherit the strictest input level. Public artifacts
  generated from restricted/confidential inputs require an explicit
  redaction marker and notes.
- **Stale horizon** — if `cortex.yaml` has `last_reviewed` and
  it is older than 90 days, emit a **warning: cortex has not
  had a review pass in N days**.
- **Archive hygiene** — `03-derived/_archive/` should not contain
  files that are also at the active path. If a file appears
  both in the active location and in `_archive/`, flag as
  **nit: artifact present in both active and archive**.

---

## 6.2 — Output: the lint report

Write the findings to
`03-derived/lint/{YYYY-MM-DD}-lint-report.md` with standard Layer
3 provenance frontmatter:

```yaml
---
generated_at: {ISO timestamp}
generator: case-cortex skill — Workflow 6 (Lint)
inputs:
  - {all Layer 1, 2, 3, 4 files scanned — listed with current hashes}
kind: lint-report
case: {case-id}
---
```

Body structure:

```markdown
# Cortex Lint — {case-id} — {YYYY-MM-DD}

## Summary

{N} blockers, {N} warnings, {N} nits. {Brief one-liner on overall
health.}

## Blockers

1. **{short title}** — {file path}. {description}. {suggested fix}.
2. ...

## Warnings

1. **{short title}** — {file path}. {description}. {suggested fix}.
2. ...

## Nits

1. **{short title}** — {file path}. {description}. {suggested fix}.
2. ...

## Not checked

{list any checks skipped and why — e.g. remote pointer HTTP checks,
git-history append-only check when no git repo present, hash-based
staleness when artifact was generated under date-only fallback}
```

Before writing the new report: if a previous lint report exists at
the active path that is older than the most recent two retained,
move the older ones to `03-derived/_archive/lint/`. Convention is
to keep the most recent two reports active so trend is visible at a
glance, and archive the rest.

Then show the user a short in-chat summary:

> Lint found {N} blockers, {N} warnings, {N} nits. Report at
> `03-derived/lint/{YYYY-MM-DD}-lint-report.md`. Top 3 blockers
> are: {1}, {2}, {3}. Want me to walk through fixes?

---

## 6.3 — When to run

Run Workflow 6 when:

- The user asks for it ("lint / audit / health-check / is anything
  stale").
- The user is about to share the Cortex with a new reader.
- A Layer 1 file has just been materially edited (auto-offer).
- A major Ingest has just completed (auto-offer — catches
  under-ingestion early).
- On a schedule — recommend monthly for any Cortex that is being
  actively maintained.

---

## 6.4 — Principles

- **Diagnose, don't silently fix.** The user decides whether to
  rewrite, supersede, or archive. Lint reports; the user or a
  Maintain/Ingest invocation fixes.
- **Respect append-only.** Fixes to Layer 2 decisions are *new*
  decision entries referencing the stale one, never in-place
  rewrites of substance.
- **Stale Layer 3 artifacts are flagged, not regenerated.**
  Regeneration is a Workflow 5 action with the user's consent.
- **Lint reports are themselves Layer 3 artifacts** — they carry
  provenance, they get retained per the archive policy, they can
  be superseded by newer lint runs.
- **Use content hashes, not mtimes.** mtime-based staleness
  produces false positives every time someone touches the Change
  Log. Hash-based staleness fires only when substance changes.
