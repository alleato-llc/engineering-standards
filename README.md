# Engineering Standards

Canonical source of truth for software engineering patterns across projects and languages. Each reference project implements these patterns in a specific language/framework, guided by skills that codify the patterns as actionable rules.

## Reference Projects

| ID | Project | Language | Framework | Domain |
|---|---|---|---|---|
| **java** | [spring-boot-testing-reference](https://github.com/alleato-llc/spring-boot-reference) | Java 25 | Spring Boot | Order management |
| **rust** | [rust-cli-reference](https://github.com/alleato-llc/rust-cli-reference) | Rust | CLI/TUI | Expense tracking |

## Skill Matrix

Skills are portable patterns that guide code generation. Each skill defines rules, code examples, and conventions for a specific concern.

**Legend:** Y = implemented, — = not yet, N/A = not applicable

| Skill | Category | java | rust | Notes |
|---|---|---|---|---|
| project-structure | Core | Y | Y | Java: domain-oriented packages. Rust: domain-oriented modules, lib/bin split |
| component-design | Core | Y | Y | Java: controllers/services/repos/clients. Rust: services/repos/clients/calculators |
| naming-conventions | Core | Y | — | `*Service`, `*Client`, `*Calculator` suffixes. Rust follows informally |
| entity-design | Core | Y | N/A | JPA-specific (`with*` fluent mutators) |
| dependency-injection | Core | Y | N/A | Spring DI. Rust uses trait objects — see trait-boundaries |
| trait-boundaries | Core | N/A | Y | Rust: traits as contracts, `Box<dyn Trait>`, `RefCell` for test mutability |
| error-handling | Core | Y | Y | Java: exception hierarchy + `@ControllerAdvice`. Rust: `thiserror` + `anyhow` |
| configuration | Core | Y | — | Java: `@ConfigurationProperties`, env vars, profiles. Rust: TBD |
| logging | Infra | Y | — | Java: SLF4J, structured JSON, `@Redacted`. Rust: TBD (`tracing` crate) |
| tracing | Infra | Y | — | Java: Micrometer, MDC, message attribute propagation. Rust: TBD |
| adding-unit-tests | Test | Y | Y | Java: JUnit + AssertJ. Rust: `#[test]` + assert macros |
| adding-integration-tests | Test | Y | Y | Java: full app + Postgres. Rust: services + test doubles or real SQLite |
| test-data-isolation | Test | Y | Y | Fresh data per test, random IDs, no cross-test deps |
| test-doubles | Test | — | Y | Rust-specific. Java covers this across integrating-external-* skills |
| integrating-external-sdk | Test | Y | — | Test implementations of SDK client interfaces |
| integrating-external-sdk-no-interface | Test | Y | — | Simulator pattern for concrete SDK classes |
| integrating-external-api | Test | Y | — | Custom interface + HTTP impl + test double |
| adding-flyway-migrations | Test | Y | N/A | Java/SQL-specific |
| setting-up-docker-for-tests | Test | Y | N/A | Java: Postgres via docker-compose. Rust: SQLite in-memory |
| project-documentation | Docs | Y | Y | Same structure: README, docs/, feature docs |

## Gaps and Priorities

### Portable skills missing from Rust CLI

1. **naming-conventions** — Formalize the `*Service`, `*Client`, `*Calculator`, `*Repository` suffixes
2. **configuration** — CLI args via `clap`, env var binding, config file support
3. **logging** — Structured logging via `tracing` crate

### Java/Spring Boot gaps

1. **test-doubles** — Covered implicitly across three skills. Consider a unified overview.

### Cross-cutting — not yet in any project

1. **CI/CD** — Build, test, release pipeline patterns
2. **graceful-shutdown** — Startup/shutdown lifecycle patterns
