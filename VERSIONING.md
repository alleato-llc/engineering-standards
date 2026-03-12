# Skill Versioning

Skills follow semantic versioning. Each skill's frontmatter includes a `version` field that tracks its current state in engineering-standards. Each reference project's skill frontmatter reflects which version that project has implemented.

## Frontmatter format

```yaml
---
name: error-handling
description: ...
version: 1.0.0
---
```

## Semver rules

| Bump | When | Project impact |
|---|---|---|
| **Major** | Pattern changed — new hierarchy, different approach, restructured rules | Projects need code changes to align |
| **Minor** | New guidance added — new section, expanded examples, additional rules | Projects benefit but existing code isn't wrong |
| **Patch** | Wording, formatting, typo fixes | No project impact |

## Workflow

1. **Edit the skill** in the reference project where it's being developed
2. **Bump the version** in the skill's frontmatter according to the semver rules above
3. **Update the matrix** in `README.md` — set the project's cell to the new version
4. **Add a CHANGELOG entry** describing what changed and why
5. **Other projects** update their local copy when ready — the matrix shows who's behind

## Reading the matrix

| Cell value | Meaning |
|---|---|
| `1.0.0` | Implemented at version 1.0.0 |
| `1.0.0` (when Latest is `2.0.0`) | Implemented but behind — check CHANGELOG for what changed |
| `—` | Not yet implemented |
| `N/A` | Not applicable to this language/framework |

## What the version tracks

The version is on the **skill definition** (the SKILL.md file), not the project's code. A skill at `2.0.0` means the skill document has been through two major revisions. When a project updates its skill to `2.0.0`, it means the project's code and local skill file match the `2.0.0` definition.

## Starting point

All existing skills start at `1.0.0` as of 2026-03-12. Prior refinements (portability cleanup, Rust alignment) are captured in this initial version. Future changes follow the semver rules above.
