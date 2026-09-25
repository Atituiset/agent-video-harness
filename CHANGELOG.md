# Changelog

All notable changes to this project are documented here. Format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/); this project
adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.0] - 2026-09-26

### Changed

- SKILL.md bodies and the 26-rule pitfalls checklist rewritten English-primary
  (short zh summary kept in each `description` for zh routing). Recipe and
  storyboard skeletons intentionally stay Chinese — they are content templates
  for the zh project. This is the internationalization milestone.

## [0.1.0] - 2026-09-25

First structured release.

### Added

- Category layout `skills/<category>/<skill>/` with taxonomy rules in
  `skills/README.md`, governed by ADR-0001 (`.agents/adr/`).
- `video` category containing the two existing skills:
  `bilingual-video` and `bilingual-tech-explainer`.
- Claude Code plugin manifests (`.claude-plugin/plugin.json`,
  `marketplace.json`) — installable via `/plugin marketplace add`.
- CI validating the skill contract (frontmatter, name/directory match,
  relative links) via `scripts/validate-skills.mjs`.
- `CONTRIBUTING.md`, GitHub issue templates (bug report, skill proposal).

### Changed

- Root README rewritten (EN + zh-CN): narrative "why these skills exist"
  structure, 30-second install for all channels, per-category reference table.
- LICENSE copyright holder corrected to the current project identity.
