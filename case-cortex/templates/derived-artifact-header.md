# Derived artifact frontmatter — template

Every file written to `03-derived/` starts with this YAML
frontmatter. It is what makes the artifact regenerable and its
provenance auditable.

---

## Template

```yaml
---
generated_at: {{YYYY-MM-DDTHH:MM:SSZ}}
generator: {{SKILL_OR_GENERATOR_NAME}}   # e.g. "case-cortex skill" or a more specific skill name
inputs:
  - path: {{RELATIVE_PATH}}
    hash: sha256:{{FIRST_12_CHARS_OF_CONTENT_HASH}}
    hash_mode: material-v1                # material-v1 | raw | commit | date-only
  - path: {{RELATIVE_PATH}}
    hash: sha256:{{FIRST_12_CHARS_OF_CONTENT_HASH}}
    hash_mode: material-v1
kind: {{ARTIFACT_KIND}}                  # briefing | analysis | summary | report | recommendation | deck | model | memo | lint-report
case: {{CASE_SLUG}}                      # the case_id from cortex.yaml
confidentiality: {{CONFIDENTIALITY}}      # public | internal | restricted | confidential
# Optional
confidence: high | medium | low          # author's confidence in the output
redaction: none | applied
redaction_notes: {{REDACTION_NOTES}}
notes: |
  One or two lines of methodology notes if useful for the reader.
---
```

---

## Provenance markers — choose the strongest available

The `inputs` block records what the artifact was built from. The
preferred format is **content hashes** (sha256, first 12 characters
of the file's content). Hashes are robust to mtime drift caused by
trivial edits (Change Log appends, whitespace fixes) that should
not invalidate the artifact.

Order of preference:

1. **Material content hashes** (recommended):
   `hash: sha256:{{FIRST_12_CHARS}}` with `hash_mode: material-v1`.
   Normalize away YAML maintenance fields, `## Change Log` sections,
   and whitespace-only differences before hashing.
2. **Raw content hashes**: `hash: sha256:{{FIRST_12_CHARS}}` with
   `hash_mode: raw`. Robust and deterministic, but conservative:
   whitespace and Change Log edits change the hash.
3. **Commit hashes** (when git is initialised): use the commit SHA
   the file was at when the artifact was generated. Equivalent in
   practice to content hashes but cheaper to compute.
4. **Date-only fallback** (when neither hashing nor git is
   available): `path: {{PATH}}@{{YYYY-MM-DD}}`. Tell the user
   staleness detection is best-effort under this fallback.

Lint Workflow 6 re-computes hashes using each input's `hash_mode`.
mtime is *not* used for staleness checks.

## Confidentiality

Set `confidentiality` to the strictest level among all inputs:

`public < internal < restricted < confidential`.

If a public artifact is generated from restricted or confidential
inputs, run a redaction pass and set `redaction: applied` with a short
`redaction_notes` explanation. Otherwise use `redaction: none`.

---

## Artifact kinds — when to use which

| Kind | Use for |
|---|---|
| `briefing` | Pre-meeting prep, stakeholder background, short context packs |
| `analysis` | Substantive examination of a question — competitive, financial, regulatory, etc. |
| `summary` | Condensed view of the case or a slice of it |
| `report` | Longer-form structured output, often a deliverable |
| `recommendation` | Output that takes a position and argues for it |
| `deck` | Slide-shaped content (even if stored as markdown) |
| `model` | Quantitative artifacts — scenario models, projections |
| `memo` | Internal note, typically short |
| `lint-report` | Output of Workflow 6 (Lint) |

---

## What goes after the frontmatter

The artifact itself, as normal markdown. The frontmatter is for
tooling and for staleness checks; readers mostly look at the
content below it.

---

## Example

```markdown
---
generated_at: 2026-04-24T14:30:00Z
generator: case-cortex skill
inputs:
  - path: 01-canonical/identity.md
    hash: sha256:a3f2b1c8e91d
    hash_mode: material-v1
  - path: 01-canonical/scope.md
    hash: sha256:7c2e44f0a92b
    hash_mode: material-v1
  - path: 01-canonical/concepts/{{KEY_CONCEPT}}.md
    hash: sha256:f99c00abe521
    hash_mode: material-v1
  - path: 02-working-memory/decisions.md
    hash: sha256:1234567890ab
    hash_mode: material-v1
kind: briefing
case: {{CASE_ID}}
confidentiality: internal
confidence: medium
redaction: none
redaction_notes: ""
notes: |
  Stakeholder data is partial — three named contacts still marked
  TODO. Resolve before this briefing is used in-meeting.
---

# Briefing — {{WORKSHOP_OR_AUDIENCE}}

...
```

---

## Retention

When a new version of an existing artifact is generated (same kind
and slug), the prior version is moved to
`03-derived/_archive/{{KIND}}/{{YYYY-MM-DD}}-{{SLUG}}.md` before the new file
is written at the active path. See `references/architecture.md`
"Layer 3 retention" for the full convention.
