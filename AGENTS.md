# AGENTS.md

Rules for editing the **release-versioning** skill. User-facing guidance lives in `SKILL.md`. `README.md` is the human skim layer.

## File roles

| File | Role |
| --- | --- |
| `SKILL.md` | The release inventory, semver rules, workflow, and artifact rules |
| `README.md` | Short human summary |

## Editing

- Bump `metadata.version` with semver in the same change whenever behavior changes: patch for wording, minor for new guidance or a new release-surface category, major for a changed workflow or scope.
- Quote every frontmatter string value. Keys stay unquoted.
- No em dashes, and no semicolons used to join what should be separate sentences. Use commas, periods, parentheses, or "and".
- Capitalized bullets and parallel list voice within each list.

## Before finishing

- Every bullet list stays capitalized and parallel.
- `metadata.version` bumped if and only if behavior changed.
- `README.md` matches the actual file layout.
