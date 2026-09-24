# AGENTS.md

Rules for editing the **release-versioning** skill. User-facing guidance lives in `SKILL.md`. `README.md` is the human skim layer.

## File roles

| File | Role |
| --- | --- |
| `SKILL.md` | The release inventory, semver rules, workflow, and artifact rules |
| `README.md` | Short human summary |

## Editing

- Bump `metadata.version` by this skill's own rules for skills in `SKILL.md`.
- Quote every frontmatter string value. Keys stay unquoted.
- No em dashes, and no semicolons used to join what should be separate sentences. Use commas, periods, parentheses, or "and".
- Capitalized bullets and parallel list voice within each list.
- This skill is the one owner of version rules. Other skills, skill-forge included, link here instead of restating them.

## Before finishing

- Every bullet list stays capitalized and parallel.
- `metadata.version` bumped as the rules for skills in `SKILL.md` require.
- `README.md` matches the actual file layout.
