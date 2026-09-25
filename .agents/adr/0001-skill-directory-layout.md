# ADR-0001: Skill directory layout

- Status: accepted
- Date: 2026-09-25

## Context

The repo started with two skills at `skills/<skill>/`. It will grow into a
multi-domain collection (reference: mattpocock/skills, which organizes ~38
skills under `skills/<category>/<skill>/`). Past history already contains one
flatten-then-unflatten reversal, so the layout needs a written decision that
ends further whole-repo churn.

## Decision

1. Skills live at `skills/<category>/<skill>/`. A category directory is
   created only when a real skill needs it — never as empty scaffolding.
2. Every category carries a `README.md` defining its boundary (what belongs,
   what does not).
3. Dependencies between skills in the same category are implicit (siblings
   may be assumed installed). Cross-category dependencies must be declared
   explicitly in the skill's `description` and body.
4. Lifecycle directories `skills/in-progress/` and `skills/deprecated/` are
   created on first use. Incubating skills live in `in-progress/` and stay out
   of the root README reference table; retired skills are moved to
   `deprecated/`, never deleted.
5. Whole-repo re-layouts are forbidden. New categories and per-skill moves
   are the only permitted structural changes.

## Consequences

- The two existing skills move to `skills/video/` (they already depend on
  each other, so they start as one category).
- Compatibility with both distribution channels (`npx skills add` and the
  Claude Code plugin marketplace) is preserved — nested skill paths are
  enumerated explicitly in `.claude-plugin/plugin.json`.
- The taxonomy rules are duplicated in `skills/README.md` for discoverability;
  this ADR is the source of truth, and rule changes require a new ADR.
