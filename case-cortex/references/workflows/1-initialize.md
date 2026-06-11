# Workflow 1 — Initialize

Goal: create a new Cortex in a location the user can reach across
sessions. This workflow is mechanical — do not over-ask, but do not
skip the runtime/persistence step.

---

## Source-isolation rule (read first)

Even at initialization, source isolation matters. The case name,
domain flavor, owner, purpose, and any other content written into
`CLAUDE.md`, `cortex.yaml`, `README.md`, or seeded skeleton files
must come from what the user typed in this conversation — not from
memory, not from sibling skills, not from inferred context.

If the user's prompt is short ("set up a cortex for my acquisition
review") and gives no further detail:

- Use a generic case name (`acquisition-review`, or ask the user
  to confirm a name) — do not borrow a target name from memory or
  context.
- Leave `CLAUDE.md` section 1 (Purpose) close to what the user
  literally said. Do not "fill in" likely details about the deal,
  the target, the sector, or the user's role unless the user
  provided them.
- Leave domain flavor as `general` if the user didn't specify, or
  ask. Do not infer the flavor from memory ("I know this user is a
  consultant, so use consulting") — *this case* might not fit the
  user's usual flavor.

Initialization should produce a clean, generic scaffold the user
recognises as theirs because they wrote it, not because the LLM
inferred it from elsewhere.

---

## Step 1.1 — Settle the persistence question

Before anything else: where does this Cortex live? See SKILL.md
"Where the Cortex lives" for the runtime branches.

Three cases:

**A) Local filesystem available (Codex, Claude Code, dev environment).**
Ask the user for an absolute path to the parent directory where
`{case-name}/` will be created. If the user has no preference,
suggest `~/cortexes/` and tell them what you'll do. Confirm before
creating.

**B) Sandboxed code-execution filesystem.** Tell the user explicitly that the working filesystem
does not persist across conversations, and ask them how they want
to handle persistence:

> The filesystem here doesn't persist between conversations. I can
> still build the Cortex in `/mnt/user-data/outputs/cases/{case-name}/`
> and you can download it as a zip at the end. But to maintain it
> across sessions, you'll need one of:
>
> 1. Re-upload the zip at the start of each session, and I'll
>    rebuild the workspace before we work.
> 2. Host the Cortex in a synced location (a GitHub repo, a cloud
>    drive). I can read from the connector at the start of each
>    session and propose updates that you commit/sync back.
> 3. Keep this as a one-shot exploration with no persistence — I'll
>    build it once and you'll save what you want.
>
> Which fits your setup?

Do not proceed until they pick one. Each option implies different
mechanics during Maintain (Workflow 4) — surface them now so the user
isn't surprised later.

**C) No filesystem available at all.** Tell the user the skill cannot
create files in this runtime, and offer alternatives:

> I can't create files in this runtime. I can either:
>
> 1. Print the scaffolding into chat for you to copy-paste into a
>    text editor, or
> 2. Wait for you to switch to a runtime with file access (Codex,
>    Claude Code, or another runtime with code execution).
>
> Which would you like?

If they pick option 1, walk through the scaffold structure and emit
each file's content as a separate fenced code block, so they can
save them one at a time.

---

## Step 1.2 — Pick minimal or full mode

If the user has not already told you, ask:

> Two starting modes:
>
> 1. **Minimal** — one growing notes file plus the operating manual.
>    Best when you're not sure yet whether you want sustained
>    structure. I'll watch for signs you're outgrowing it and offer
>    to migrate.
> 2. **Full** — the four-layer scaffolding from day one. Best when
>    you already know you'll be ingesting multiple sources or
>    reasoning over the case for weeks/months.
>
> Which?

When in doubt, default to **minimal** and offer to upgrade. Friction
of upgrading later is much lower than friction of an over-built
scaffold on day one.

If full mode is chosen, also ask for:

1. **Case name** — short slug-friendly identifier (e.g.
   `acquisition-target-x`, `regulatory-review-2026`,
   `internal-restructuring-q3`). Use ASCII-only, lowercase, hyphens.
2. **Domain flavor** — one of: `consulting`, `legal`, `research`,
   `engineering`, `investigation`, `general`. This picks the Layer
   1 skeleton template. If unsure, offer `general` and note they
   can extend later.
3. **Owner** — person responsible for the Cortex. Default to "you"
   if it's clearly a solo case.

If minimal mode is chosen, you only need the case name and owner.
The domain flavor is unnecessary for minimal mode.

---

## Step 1.3 — Create the directory structure

### Minimal mode

Create at `{storage_path}/{case-name}/`:

```
{case-name}/
  CLAUDE.md
  cortex.yaml
  README.md
  notes.md
```

Populate:

- `CLAUDE.md` — use `templates/claude-md-template.md`. Fill in
  section 1 (Purpose) from what the user told you. Mark the case
  as **minimal mode** in section 2 (Pointer to generic schema).
  Leave sections 4–8 mostly empty.
- `cortex.yaml` — use `templates/cortex-yaml-template.yaml`. Set
  `mode: minimal`, `cortex_schema: 1`, and `skill_version: 1.0`.
- `README.md` — use `templates/readme-template.md`, with a
  minimal-mode variant note pointing the user at `notes.md`.
- `notes.md` — use `templates/notes-template.md`.

Minimal mode remains a real Cortex mode, not a throwaway note. Route
ordinary updates through Workflow 4's minimal-mode path: append dated
notes, maintain the Open questions and Decisions sections, preserve
Pointers, and offer migration when triggers appear.

### Full mode

Create at `{storage_path}/{case-name}/`:

```
{case-name}/
  CLAUDE.md
  cortex.yaml
  README.md
  01-canonical/
    overview.md
    synthesis.md
    index.md
    identity.md
    scope.md
    context.md
    concepts/
      .gitkeep
    entities/
      .gitkeep
    sources/
      .gitkeep
  02-working-memory/
    decisions.md
    open-questions.md
    log/
      .gitkeep
  03-derived/
    .gitkeep
    _archive/
      .gitkeep
  04-pointers/
    systems.yaml
    external.yaml
```

Populate the files as follows:

- **`CLAUDE.md`** — use `templates/claude-md-template.md`. This is
  the per-case operating manual: language convention,
  domain-specific page conventions, jurisdictional defaults, tone
  bias, and any case-specific tweaks to the generic workflows. The
  generic skill provides the four-layer shape and the six
  workflows; `CLAUDE.md` is the per-case overlay that co-evolves
  with the LLM as conventions emerge. Fill in section 1 (Purpose)
  from what the user told you during Step 1.2; set section 3
  (Language convention) to English unless the user specified
  otherwise; leave sections 4 (Domain conventions), 5 (Workflow
  tweaks), and 8 (Open items) mostly empty for the first session
  — they grow during use. Always include the initial entry in the
  Change Log. Without `CLAUDE.md`, future sessions see only the
  generic skill and have no per-case memory of what conventions
  were settled.
- **`cortex.yaml`** — use the template in
  `templates/cortex-yaml-template.yaml`, filling in the case name,
  domain, owner, creation date, and a generated `case_id`
  (lowercase slug). Set `mode: full`, `cortex_schema: 1`, and
  `skill_version: 1.0`.
- **`README.md`** — use `templates/readme-template.md`,
  substituting the case name and a one-line purpose statement.
- **Spine files** (`overview.md`, `synthesis.md`, `index.md`) —
  these are the three first-class meta-layer files that turn a
  Cortex from a flat document store into a navigable knowledge
  base. They are stubs at initialization and grow during Ingest,
  Use, and Lint. Use, in order:
  - `templates/overview-template.md` for `overview.md` — a narrative
    entry point: "what is this case, why does it exist, what's the
    design in one paragraph, where do you start reading"
  - `templates/synthesis-template.md` for `synthesis.md` —
    opinion-bearing current best-thinking: direction, open risks,
    design patterns chosen or rejected, parked items
  - `templates/index-template.md` for `index.md` — the curated
    catalog of every page in the Cortex, grouped by topical cluster
    (not just an auto-generated file list)

  These start mostly empty with structural placeholders; they are
  populated iteratively as concepts and sources accumulate. The
  discipline of having them present from day one is what prevents
  the meta-layer gap.

- **Layer 1 skeleton files** (`identity.md`, `scope.md`,
  `context.md`) — populate with the domain-specific scaffolding
  from `templates/domains/{flavor}.md`. These are *structured
  placeholders*, not filled content — the user fills them in
  during the Seed workflow.

- **`01-canonical/concepts/`** — starts empty. This is the home
  for per-concept pages generated during Ingest (see Workflow 3).
  Do not pre-seed it; the case hasn't earned its concepts yet.
  Concepts are mechanisms, KPIs, terms of art, calculation rules,
  clauses — things that *describe how something works*, not
  things that *act* in the case.

- **`01-canonical/entities/`** — starts empty. This is the home
  for per-entity pages: people, organisations, teams, legal
  entities, products, systems, projects, regulators,
  jurisdictions — anything named with identity that *acts* in the
  case. One file per entity, named `{slug}.md`. See
  `templates/entity-template.md`.

- **`01-canonical/sources/`** — starts empty. This is the home
  for one rich page per ingested source: the LLM's "reading
  notes" with TL;DR, parties involved, structural breakdown, key
  facts, notable quotes, takeaways for the case. One file per
  source, named `{YYYY-MM-DD}_{slug}.md`. See
  `templates/source-summary-template.md`. This is not optional —
  every Ingest produces a source summary in addition to fanning
  out concepts and entities. It is the bridge between the raw
  source and the fan-out, and it is what makes the Cortex
  auditable.

- **`decisions.md`** and **`open-questions.md`** — use
  `templates/working-memory-skeleton.md` content.

- **`systems.yaml`** — use `templates/systems-template.yaml`.

- **`external.yaml`** — use `templates/external-template.yaml`.

- **`.gitkeep` files** — empty; they preserve empty directories.

---

## Step 1.4 — Confirm and offer next step

Show the user the created path and the tree. Briefly explain:

For full mode:

- the three spine files (`overview.md`, `synthesis.md`,
  `index.md`) — the meta-layer that distinguishes a Cortex from a
  flat folder of notes;
- the split between `concepts/` (mechanisms, definitions,
  calculations) and `entities/` (named people, orgs, systems —
  things with identity);
- the `sources/` directory — one summary per ingested source;
- `CLAUDE.md` — the per-case operating manual that the LLM and
  the user co-evolve to capture conventions specific to this case
  (language, jurisdiction, tone, domain quirks).

Then explicitly offer:

> Cortex scaffold is ready at `{path}`. Want me to seed it now? I
> can either walk you through a wizard (I ask, you answer), take
> a brief you paste and fill it in one shot, or ingest an
> existing document.

For minimal mode, offer:

> Minimal Cortex ready at `{path}`. `notes.md` is the working
> surface for now. I can append notes, track questions and decisions,
> keep pointers tidy, and offer to migrate to the full structure when
> it's worth it. Want to start with a first note, paste a small intake
> brief, or come back later?

Do not auto-proceed. Wait for their choice.

---

## Migrating minimal → full

When a minimal-mode Cortex outgrows itself, the skill offers
migration. Triggers:

- `notes.md` exceeds ~500 lines.
- The user is about to ingest a second source.
- The user starts asking the skill questions that the flat
  structure can't answer ("what did we decide about X" — without
  Layer 2 decisions logged separately, the skill has to grep
  through `notes.md`).

When triggered, propose:

> `notes.md` is getting long ({N} lines) and you're about to
> {ingest a second source / log a third decision}. The flat
> structure is working against you now. Want me to migrate to
> the full four-layer structure? I'll split the notes into the
> right layers and you can keep working — no content is lost.

Migration mechanics:

1. Create the full directory structure from Step 1.3.
2. Walk through `notes.md` and split:
   - Identity-shaped content (case name, purpose, success
     criteria) → `01-canonical/identity.md`.
   - Scope-shaped content (in/out of scope, constraints) →
     `01-canonical/scope.md`.
   - Context-shaped content (background, sector, history) →
     `01-canonical/context.md`.
   - Decisions → `02-working-memory/decisions.md` (one entry per
     decision, dated).
   - Open questions → `02-working-memory/open-questions.md`.
   - Dated entries (meetings, events, observations) → one log
     file each at `02-working-memory/log/{YYYY-MM-DD}-{slug}.md`.
   - Anything that looks like an entity blurb (a person, a firm,
     a product) → propose creating an entity page; ask the user
     before writing.
   - Anything that looks like a concept blurb (a mechanism, a
     KPI, a term-of-art) → propose creating a concept page; ask.
3. Update `cortex.yaml` (`mode: full`) and `CLAUDE.md` section 2
   to reference the four-layer model.
4. Move the original `notes.md` to
   `03-derived/_archive/notes-pre-migration.md` with a header
   explaining what was migrated where. Do not delete it.
5. Generate stub spine files (`overview.md`, `synthesis.md`,
   `index.md`) populated from the migrated content.
6. Add a Change Log entry to `CLAUDE.md` documenting the migration.

Tell the user the migration is complete and ask if they want to
review the splits before continuing.
