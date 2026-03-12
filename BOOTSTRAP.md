# Project Bootstrap

Every reference project must have the following tooling configured. The specific tools vary by language, but the requirements are universal.

## Requirements

### 1. Formatting

All source code is auto-formatted. No style debates in code review — the formatter is the authority.

**Rules:**
- One formatter per language, configured at the project root
- Format-on-save in editor or format as a pre-commit step
- CI fails on unformatted code

| Language | Tool | Config file |
|---|---|---|
| Java | google-java-format (via Spotless) | `build.gradle` (Spotless plugin) |
| Rust | rustfmt | `rustfmt.toml` |
| Go | gofmt | None (built-in, zero config) |
| Python | ruff format | `pyproject.toml` |
| TypeScript | Prettier | `.prettierrc` |
| Swift | SwiftFormat | `.swiftformat` |

### 2. Linting

Static analysis catches bugs, enforces idioms, and flags suspicious patterns beyond what the compiler catches.

**Rules:**
- One primary linter per language
- All warnings are errors in CI — no warning suppression without a comment explaining why
- Linter config lives in the project root

| Language | Tool | Config file |
|---|---|---|
| Java | Checkstyle | `config/checkstyle/checkstyle.xml` |
| Rust | Clippy | `clippy.toml` or `Cargo.toml` `[lints]` |
| Go | golangci-lint | `.golangci.yml` |
| Python | ruff | `pyproject.toml` |
| TypeScript | ESLint | `eslint.config.js` |
| Swift | SwiftLint | `.swiftlint.yml` |

### 3. Git hooks

Pre-commit hooks run format + lint before every commit. Code that doesn't pass never enters the repo.

**Rules:**
- Hooks run format and lint at minimum
- Hooks must be fast (< 10 seconds) — run only on staged files, not the entire project
- Hooks are installed automatically (documented in README or set up via a bootstrap script)
- Never bypass hooks (`--no-verify`) unless explicitly justified

| Language | Tool | Config file |
|---|---|---|
| Java | pre-commit or Gradle task | `.pre-commit-config.yaml` or `build.gradle` |
| Rust | pre-commit or cargo-husky | `.pre-commit-config.yaml` |
| Go | pre-commit | `.pre-commit-config.yaml` |
| Python | pre-commit | `.pre-commit-config.yaml` |
| TypeScript | husky + lint-staged | `.husky/`, `package.json` |
| Swift | pre-commit | `.pre-commit-config.yaml` |

### 4. Dependency scanning

Automated checks for known vulnerabilities in dependencies. Runs in CI and optionally as a pre-push hook.

**Rules:**
- CI runs dependency scanning on every PR
- Automated PRs for dependency updates (Dependabot or Renovate)
- Critical/high vulnerabilities block merge
- Scanning covers both direct and transitive dependencies

| Language | Scanning tool | Update tool |
|---|---|---|
| Java | OWASP dependency-check (Gradle plugin) | Dependabot or Renovate |
| Rust | `cargo audit` | Dependabot or Renovate |
| Go | `govulncheck` | Dependabot or Renovate |
| Python | `pip-audit` | Dependabot or Renovate |
| TypeScript | `npm audit` | Dependabot or Renovate |
| Swift | `swift package audit` (or manual) | Dependabot or Renovate |

## Project checklist

When bootstrapping a new reference project, verify:

- [ ] Formatter configured and documented in README
- [ ] Linter configured, all warnings are errors in CI
- [ ] Git hooks install automatically and run format + lint on staged files
- [ ] Dependency scanning runs in CI
- [ ] Dependabot or Renovate configured for automated dependency updates
- [ ] README documents how to set up the dev environment (hooks, tools)
