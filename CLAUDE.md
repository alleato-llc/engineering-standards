# CLAUDE.md

## Project Overview

Canonical source of truth for software engineering patterns across projects and languages. This is a meta-project — it doesn't contain application code. It defines skills (portable patterns), tracks which reference projects implement them, and documents cross-cutting standards.

## What this repo contains

- `README.md` — Reference project registry and skill matrix (coverage + versions)
- `VERSIONING.md` — How skills are versioned (semver rules, workflow, reading the matrix)
- `CHANGELOG.md` — What changed in each skill version, organized by skill
- `BOOTSTRAP.md` — Universal project setup requirements (formatting, linting, git hooks, dependency scanning)

## Reference Projects

| ID | Project | Path |
|---|---|---|
| **java** | spring-boot-testing-reference | `../spring-boot-testing-reference/` |
| **rust** | rust-cli-reference | `../rust-cli-reference/` |

## How skills work

Skills live in each reference project's `.claude/skills/` directory. Each skill has:
- A `SKILL.md` file with frontmatter (`name`, `description`, `version`)
- Rules, code examples, and conventions for a specific concern

The skill matrix in `README.md` tracks which skills exist, their latest version, and which version each project implements.

## Skill versioning

Skills follow semantic versioning. See [VERSIONING.md](VERSIONING.md) for full rules.

- **Major**: Pattern changed — projects need code changes
- **Minor**: New guidance added — projects benefit but existing code isn't wrong
- **Patch**: Wording/formatting — no project impact

## Workflows

### When updating a skill in a reference project
1. Edit the skill's `SKILL.md` in the reference project
2. Bump the `version` in frontmatter per semver rules
3. Update the matrix in this repo's `README.md` (project column + Latest column if this is the newest version)
4. Add a CHANGELOG entry in this repo

### When adding a new skill
1. Create `.claude/skills/<skill-name>/SKILL.md` in the reference project with `version: 1.0.0`
2. Add a row to the matrix in `README.md` with Latest = `1.0.0`
3. Add a CHANGELOG entry
4. Update the reference project's `CLAUDE.md` skills list

### When checking project alignment
Read the matrix. If a project's version is behind Latest, check the CHANGELOG to understand what changed and whether it requires code updates.

## Conventions

- Skills are the unit of change — one skill per concern, versioned independently
- The matrix is the single view of cross-project coverage and currency
- CHANGELOG is organized by skill, not by date — find a skill's history in one place
- Reference projects link back to this repo in their CLAUDE.md
