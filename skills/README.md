# Skills index

Skills are grouped by **category** (`skills/<category>/<skill>/`).

| Category | Skills | What it covers |
|---|---|---|
| [video](video/) | [bilingual-video](video/bilingual-video/), [bilingual-tech-explainer](video/bilingual-tech-explainer/) | Producing bilingual (zh+en) videos with HyperFrames |

## Taxonomy rules

These rules govern how the directory grows. They are recorded as [ADR-0001](../.agents/adr/0001-skill-directory-layout.md); change them only through a new ADR.

1. **Grow the structure, don't design it.** A new category directory is created only when a skill that genuinely belongs to it arrives. Never create empty placeholder categories.
2. **Every category has a README.** It defines the category boundary: what belongs here, what does not. Without it, categories rot as skills accumulate.
3. **Dependencies within a category are implicit; across categories they are explicit.** A skill may assume its sibling skills in the same category are installed. Depending on a skill in another category must be declared in the skill's `description` and body.
4. **Lifecycle directories** (created when first needed, not before):
   - `skills/in-progress/` — skills being incubated. Not listed in the root README reference table until graduated into a real category.
   - `skills/deprecated/` — retired skills are moved here, never deleted, so existing installs don't silently break.
5. **No whole-repo re-layouts.** New categories and per-skill moves are allowed; reorganizing everything at once is not.
