# Contributing

Community contributions are welcome — fixes, improvements, and new skills.

## Who publishes here

This repository is a curated public selection, not accilium's working repository. Skills reach it only after an internal review that covers sanitization and publishing rights, and maintainers open the pull request. **If you work at accilium, do not open a pull request here directly** — a pull request against a public repository is itself a publication, visible before anyone reviews it. Take the skill through the internal process instead.

Everything below applies to contributions from outside accilium.

## Ground rules

- **No client or company-specific data.** Examples must use fictional cases. Maintainers run a contamination check on every PR; anything that looks like real-world confidential material gets the PR closed.
- **One skill per folder**, kebab-case folder name matching the `name:` field in the `SKILL.md` frontmatter.
- **`SKILL.md` is the entry point.** Its `description:` must contain concrete trigger phrases ("build a cortex for X") *and* explicit exclusions ("Do NOT use for …"). Larger skills split detail into `references/` and `templates/` so the entry point stays small.
- **Test before you submit.** Run the skill against at least three different inputs and confirm the output matches what the skill promises. Say in the PR what you tested.

## Workflow

1. **Improvements / fixes** — open a PR directly. Reference an issue if one exists.
2. **New skills** — open an issue first describing the workflow the skill encodes and why it is generally useful. This avoids building something we can't merge.
3. PRs are reviewed by accilium maintainers. Squash merge.

Before your first commit, enable the repository's hooks:

```
git config core.hooksPath .githooks
```

They check two things: that the commit author is a person rather than a bot or assistant account, and that the author email is a real address rather than the local hostname git substitutes when `user.email` was never set. The second one exists because that default publishes the name of your machine.

## Versioning

Skills carry a `version:` in their frontmatter (semver). Bump the patch version for fixes, minor for new capabilities, major for breaking changes to the skill's on-disk contracts (templates, frontmatter schemas).

## License

By contributing you agree that your contribution is licensed under the [MIT license](LICENSE).
