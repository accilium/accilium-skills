# Contributing

Community contributions are welcome — fixes, improvements, and new skills.

## Ground rules

- **No client or company-specific data.** Examples must use fictional cases. Maintainers run a contamination check on every PR; anything that looks like real-world confidential material gets the PR closed.
- **One skill per folder**, kebab-case folder name matching the `name:` field in the `SKILL.md` frontmatter.
- **`SKILL.md` is the entry point.** Its `description:` must contain concrete trigger phrases ("build a cortex for X") *and* explicit exclusions ("Do NOT use for …"). Larger skills split detail into `references/` and `templates/` so the entry point stays small.
- **Test before you submit.** Run the skill against at least three different inputs and confirm the output matches what the skill promises. Say in the PR what you tested.

## Workflow

1. **Improvements / fixes** — open a PR directly. Reference an issue if one exists.
2. **New skills** — open an issue first describing the workflow the skill encodes and why it is generally useful. This avoids building something we can't merge.
3. PRs are reviewed by accilium maintainers. Squash merge.

## Versioning

Skills carry a `version:` in their frontmatter (semver). Bump the patch version for fixes, minor for new capabilities, major for breaking changes to the skill's on-disk contracts (templates, frontmatter schemas).

## License

By contributing you agree that your contribution is licensed under the [MIT license](LICENSE).
