# accilium skills

Agent skills from [accilium](https://www.accilium.com)'s AI-native transformation, shared in public.

## Why we share this

We run our internal AI rollout as a weekly build-and-ship cycle: consulting workflows get encoded as skills, tested by our own teams, and shipped every Friday. Some of those skills are generic enough to be useful far beyond our walls. We publish them here because we think the value of consulting craft lies in how fast you adapt it, not in keeping it secret — and because skills get better when more people use them and report back.

Everything in this repo is sanitized: no client data, no internal data. Examples use fictional cases.

## What a skill is

A skill is a folder containing a `SKILL.md` file (plus optional references and templates) in [Anthropic's Agent Skills format](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview). An agent loads the skill when the task matches its description and follows the instructions inside. Skills work in Claude Code, claude.ai, and other runtimes that support the format.

## How to use

**Claude Code** — add this repo as a plugin marketplace:

```
/plugin marketplace add accilium/accilium-skills
/plugin install case-cortex@accilium-skills
```

**Manual** — copy a skill folder into your skills directory (for example `~/.claude/skills/`).

## Skills

| Skill | What it does |
|---|---|
| [`case-cortex`](case-cortex/) | Build and maintain a **Case Cortex**: a structured, living, file-based memory for a single bounded knowledge-work problem — a deal, a matter, an investigation, a research question. Four layers (canonical facts, working memory, derived artifacts, pointers), six workflows (initialize, seed, ingest, maintain, use, lint), full provenance on everything. |

## Feedback and contributions

Found a problem or have an improvement? Open an issue or a pull request — see [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)
