# Engineering Standards

Canonical source of truth for software engineering patterns across projects and languages. Each reference project implements these patterns in a specific language/framework, guided by skills that codify the patterns as actionable rules.

## Reference Projects

| ID | Project | Language | Framework | Domain |
|---|---|---|---|---|
| **java** | [spring-boot-testing-reference](https://github.com/alleato-llc/spring-boot-reference) | Java 25 | Spring Boot | Order management |
| **rust** | [rust-cli-reference](https://github.com/alleato-llc/rust-cli-reference) | Rust | CLI/TUI | Expense tracking |

## Skill Matrix

Skills are portable patterns that guide code generation. Each skill defines rules, code examples, and conventions for a specific concern. Skills follow [semantic versioning](VERSIONING.md). See [CHANGELOG.md](CHANGELOG.md) for what changed in each version.

**Legend:** version = implemented at that version, — = not yet defined or implemented, N/A = not applicable

| Skill | Category | Latest | java | rust | Notes |
|---|---|---|---|---|---|
| project-structure | Core | 1.0.0 | 1.0.0 | 1.0.0 | Java: domain-oriented packages. Rust: domain-oriented modules, lib/bin split |
| component-design | Core | 1.0.0 | 1.0.0 | 1.0.0 | Java: controllers/services/repos/clients. Rust: services/repos/clients/calculators |
| naming-conventions | Core | 1.0.0 | 1.0.0 | — | `*Service`, `*Client`, `*Calculator` suffixes. Rust follows informally |
| entity-design | Core | 1.0.0 | 1.0.0 | N/A | JPA-specific (`with*` fluent mutators) |
| dependency-injection | Core | 1.0.0 | 1.0.0 | N/A | Spring DI. Rust uses trait objects — see trait-boundaries |
| trait-boundaries | Core | 1.0.0 | N/A | 1.0.0 | Rust: traits as contracts, `Box<dyn Trait>`, `RefCell` for test mutability |
| error-handling | Core | 1.0.0 | 1.0.0 | 1.0.0 | Java: exception hierarchy + `@ControllerAdvice`. Rust: `thiserror` + `anyhow` |
| configuration | Core | 1.0.0 | 1.0.0 | — | Java: `@ConfigurationProperties`, env vars, profiles. Rust: TBD |
| input-validation | Core | — | — | — | Where/how to validate, sanitization, boundary rules |
| api-design | Core | — | — | — | URL conventions, status codes, pagination, versioning, response shape |
| authentication | Security | — | — | — | Auth flow patterns (JWT, OAuth2, API keys), middleware placement |
| authorization | Security | — | — | — | Role/permission checks, resource-level vs action-level, where checks live |
| secrets-management | Security | — | — | — | How secrets enter the app, rotation, what never goes in code |
| logging | Infra | 1.0.0 | 1.0.0 | — | Java: SLF4J, structured JSON, `@Redacted`. Rust: TBD (`tracing` crate) |
| tracing | Infra | 1.0.0 | 1.0.0 | — | Java: Micrometer, MDC, message attribute propagation. Rust: TBD |
| adding-unit-tests | Test | 1.0.0 | 1.0.0 | 1.0.0 | Java: JUnit + AssertJ. Rust: `#[test]` + assert macros |
| adding-integration-tests | Test | 1.0.0 | 1.0.0 | 1.0.0 | Java: full app + Postgres. Rust: services + test doubles or real SQLite |
| test-data-isolation | Test | 1.0.0 | 1.0.0 | 1.0.0 | Fresh data per test, random IDs, no cross-test deps |
| test-doubles | Test | 1.0.0 | — | 1.0.0 | Rust-specific. Java covers this across integrating-external-* skills |
| integrating-external-sdk | Test | 1.0.0 | 1.0.0 | — | Test implementations of SDK client interfaces |
| integrating-external-sdk-no-interface | Test | 1.0.0 | 1.0.0 | — | Simulator pattern for concrete SDK classes |
| integrating-external-api | Test | 1.0.0 | 1.0.0 | — | Custom interface + HTTP impl + test double |
| adding-flyway-migrations | Test | 1.0.0 | 1.0.0 | N/A | Java/SQL-specific |
| setting-up-docker-for-tests | Test | 1.0.0 | 1.0.0 | N/A | Java: Postgres via docker-compose. Rust: SQLite in-memory |
| project-documentation | Docs | 1.0.0 | 1.0.0 | 1.0.0 | Same structure: README, docs/, feature docs |
| project-bootstrap | Setup | — | — | — | Formatting, linting, git hooks, dependency scanning. See [BOOTSTRAP.md](BOOTSTRAP.md) |

## Gaps and Priorities

### Portable skills missing from Rust CLI

1. **naming-conventions** — Formalize the `*Service`, `*Client`, `*Calculator`, `*Repository` suffixes
2. **configuration** — CLI args via `clap`, env var binding, config file support
3. **logging** — Structured logging via `tracing` crate

### Java/Spring Boot gaps

1. **test-doubles** — Covered implicitly across three skills. Consider a unified overview.

### Cross-cutting — not yet in any project

1. **input-validation** — Boundary validation rules, sanitization, reject vs coerce
2. **api-design** — URL shape, status codes, pagination, versioning, response conventions
3. **authentication** — JWT/OAuth2/API key patterns, middleware placement, accessing the authenticated user
4. **authorization** — Role/permission model, where checks live, resource-level access control
5. **secrets-management** — Extends configuration; vault integration, rotation, what never goes in code
6. **CI/CD** — Build, test, release pipeline patterns
7. **graceful-shutdown** — Startup/shutdown lifecycle patterns
