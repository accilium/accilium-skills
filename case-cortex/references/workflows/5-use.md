# Workflow 5 — Use

Goal: turn a maintained Cortex into answers and artifacts. Three
sub-workflows: 5a queries, 5b derived artifacts, 5c cross-checks
(deferred to Lint).

---

## 5a — Answer a question from the Cortex

When the user asks a question about the case ("what's our scope
again?", "who's the controller at the subsidiary?", "where did we
land on Approach A vs B?"):

1. **Read the right files first.** Start with `01-canonical/` for
   ground truth, `02-working-memory/` for live state, then Layer 4
   pointers if the answer requires checking external data.
2. **Use the spine.** `index.md` is the navigation surface;
   `synthesis.md` is the opinion-bearing summary; `overview.md`
   is the entry point for new readers (including the LLM in a new
   session). Reading these first usually answers the question or
   points to the right deeper file.
3. **Cite the file.** Always tell the user which file the answer
   came from: *"Per `01-canonical/scope.md`, the case covers …"*.
4. **Don't guess if the Cortex is silent.** If the answer isn't in
   the Cortex, say so explicitly. Offer to (a) add the question
   to `open-questions.md` for tracking, or (b) ingest a source
   that would answer it.
5. **Don't synthesise across layers without saying so.** If you
   stitch together facts from `entities/`, `concepts/`, and
   `decisions.md`, mark the response as a synthesis. Concrete
   citations stay grounded.

---

## 5b — Generate a derived artifact

When the user asks for a briefing, analysis, summary, report,
recommendation, deck outline, or similar Layer 3 output:

1. **Identify the inputs.** Read the relevant Layer 1 files
   (skeleton, entities, concepts, sources) and the relevant slice
   of Layer 2 (decisions, recent log, open questions). Be
   explicit with yourself about which files you're using.

2. **Compute input hashes.** For each input file, compute the
   strongest available hash:
   - Prefer `material-v1`: normalized content with YAML maintenance
     fields, `## Change Log` sections, and whitespace-only
     differences removed.
   - Fall back to `raw`: sha256 of the file content. Raw hashes are
     conservative and can mark artifacts stale after non-substantive
     edits.
   Store the first 12 characters in the artifact's frontmatter along
   with `hash_mode`.

   If code execution is available, use it for hash computation and
   link validation rather than doing these mechanically by eye.

3. **Determine effective confidentiality.** Read `confidentiality`
   from each input's frontmatter where present. The artifact inherits
   the strictest input level using:
   `public < internal < restricted < confidential`.

   If the user asks for a lower-confidentiality artifact than the
   inputs allow, ask whether to keep the higher classification or run
   a redaction pass. A redacted public artifact must include
   `redaction: applied` and a short `redaction_notes` field.

4. **Write the artifact** to
   `03-derived/{kind}/{YYYY-MM-DD}-{slug}.md` with provenance
   frontmatter from `templates/derived-artifact-header.md`:

```yaml
---
generated_at: {ISO timestamp}
generator: case-cortex skill (or specific skill name if applicable)
inputs:
  - path: 01-canonical/identity.md
    hash: sha256:{first-12-chars}
    hash_mode: material-v1
  - path: 01-canonical/concepts/{slug}.md
    hash: sha256:{first-12-chars}
    hash_mode: material-v1
  - path: 01-canonical/entities/{slug}.md
    hash: sha256:{first-12-chars}
    hash_mode: material-v1
  - path: 02-working-memory/decisions.md
    hash: sha256:{first-12-chars}
    hash_mode: material-v1
kind: briefing | analysis | summary | report | recommendation | deck | model | memo
case: {case-id}
confidentiality: public | internal | restricted | confidential
---
```

When git is available, commit hashes are an acceptable substitute
for content hashes. When neither is available, fall back to
date-only markers (`{path}@{YYYY-MM-DD}`) and tell the user
staleness detection is best-effort under that fallback.

5. **Show the user the artifact path and a short summary.** Do
   not dump the full artifact into chat unless they ask — the
   file *is* the deliverable. A 2–4 sentence summary plus the
   path is the right shape.

6. **Move any prior version to `_archive/`.** If a Layer 3
   artifact of the same kind and slug already exists at the
   active path, move it to `03-derived/_archive/{kind}/` before
   writing the new one. This is the retention convention from
   `references/architecture.md`.

### Health dashboard variant

When the user asks for a health summary, dashboard, snapshot, or quick
state-of-the-Cortex report, generate:

`03-derived/health/{YYYY-MM-DD}-health-dashboard.md`

Use Layer 3 frontmatter and include at least:

- entity count, concept count, source summary count, derived artifact
  count;
- link density: average outbound links per entity/concept page, plus
  pages with zero outbound links;
- stale derived artifacts based on stored input hashes;
- open questions older than 60 days;
- TODOs older than 90 days using `TODO(YYYY-MM-DD): ...`;
- confidentiality distribution and any derived artifacts whose
  declared confidentiality is lower than their inputs;
- last review date from `cortex.yaml`;
- top 5 recommended cleanup actions.

This is a convenience artifact, not a full lint. If the dashboard
finds blockers or suspicious provenance, recommend Workflow 6.

Snapshot/export and state diff are optional runtime conveniences:
create a zip/tar bundle or compare two git refs only when the runtime
supports it and the user asks. Record the generated bundle/diff as a
Layer 3 artifact with provenance.

---

## 5c — Cross-check for consistency

When asked to review or challenge the Cortex, defer to Workflow 6
(Lint).
