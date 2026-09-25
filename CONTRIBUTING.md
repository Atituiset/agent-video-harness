# Contributing

Thanks for considering a contribution. This repo is a curated collection of agent skills, and the bar is "would a working engineer trust this in production?"

## Ground rules

1. **Run the validator before opening a PR**: `node scripts/validate-skills.mjs`. CI runs the same check.
2. **Skills are plain Markdown + CLI scripts.** No build step, no runtime framework. A skill must be self-contained in its directory — everything it needs installs with it.
3. **Write for agents first, humans second.** A `SKILL.md` is a routing + instruction document an agent loads mid-task: compact, directive, no marketing prose. Human-facing context goes in the skill's `README.md`.
4. **Frontmatter contract**: `name` must equal the directory name; `description` ends with an English "Use when …" routing sentence so any agent can decide when to reach for it.

## Adding a new skill

1. Find the right category under `skills/`, or propose a new one. Categories are created only when a real skill needs them — see [ADR-0001](.agents/adr/0001-skill-directory-layout.md) and [skills/README.md](skills/README.md) for the growth rules.
2. Unsure it's ready? Open a draft PR with the skill under `skills/in-progress/` (create the directory if you're the first). It graduates to a real category once it has been exercised on a real task.
3. Update the category `README.md` table. Skills in `in-progress/` stay out of the root README reference table.

## Changing conventions

Anything that changes how the repo itself works (layout, taxonomy, lifecycle rules, frontmatter contract) is decided through an ADR in [.agents/adr/](.agents/adr/). Copy the format of `0001-skill-directory-layout.md`: context → decision → consequences, one page.

## Reporting issues

- **Bug in a skill**: use the *Bug report* template — name the skill, the agent you ran it on, and what it did vs. what you expected.
- **New skill idea**: use the *Skill proposal* template — describe the failure mode it fixes first. Skills that encode a recurring pain are welcome; skills that wrap a one-off task are not.

## License

By contributing you agree your contributions are licensed under the [MIT License](LICENSE).
