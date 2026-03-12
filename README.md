# Engineering Standards

Canonical source of truth for software engineering patterns across projects and languages. Each reference project implements these patterns in a specific language/framework, guided by skills that codify the patterns as actionable rules.

## Reference Projects

| Project | Language | Framework | Domain |
|---|---|---|---|
| [spring-boot-testing-reference](https://github.com/alleato-llc/spring-boot-reference) | Java 25 | Spring Boot | Order management |
| [rust-cli-reference](https://github.com/alleato-llc/rust-cli-reference) | Rust | CLI/TUI | Expense tracking |

## Skill Matrix

Skills are portable patterns that guide code generation. Each skill defines rules, code examples, and conventions for a specific concern. The matrix below tracks which skills exist in each reference project.

### Legend

- **Y** — Skill exists and is implemented
- **—** — Skill does not exist yet
- **N/A** — Not applicable to this language/framework

### Core

| Skill | Java/Spring Boot | Rust CLI | Notes |
|---|---|---|---|
| project-structure | Y | Y | Java: domain-oriented packages, sibling subdomains. Rust: domain-oriented modules, lib/bin split |
| component-design | Y | Y | Java: controllers, services, repositories, clients. Rust: services, repositories, clients, calculators |
| naming-conventions | Y | — | Java: `*Service`, `*Client`, `*Calculator` suffixes. Rust follows similar conventions informally |
| entity-design | Y | N/A | JPA-specific (`with*` fluent mutators). Rust uses plain structs |
| dependency-injection | Y | N/A | Spring DI. Rust uses constructor injection via trait objects — covered by trait-boundaries |
| trait-boundaries | N/A | Y | Rust-specific: traits as contracts, `Box<dyn Trait>` for DI, `RefCell` for test mutability |
| error-handling | Y | Y | Java: exception hierarchy + `@ControllerAdvice`. Rust: `thiserror` + `anyhow` + `?` propagation |
| configuration | Y | — | Java: `@ConfigurationProperties`, env var binding, profiles. Rust: TBD (likely `clap` + env vars) |

### Infrastructure

| Skill | Java/Spring Boot | Rust CLI | Notes |
|---|---|---|---|
| logging | Y | — | Java: SLF4J, structured JSON, `@Redacted`. Rust: TBD (`tracing` crate likely) |
| tracing | Y | — | Java: Micrometer Tracing, MDC, message attribute propagation. Rust: TBD |

### Testing

| Skill | Java/Spring Boot | Rust CLI | Notes |
|---|---|---|---|
| adding-unit-tests | Y | Y | Java: JUnit + AssertJ. Rust: `#[test]` + assert macros |
| adding-integration-tests | Y | Y | Java: full Spring Boot + Postgres. Rust: services with test doubles or real SQLite |
| test-data-isolation | Y | Y | Both: fresh data per test, random IDs, no cross-test dependencies |
| test-doubles | — | Y | Rust-specific skill. Java covers this across integrating-external-* skills |
| integrating-external-sdk | Y | — | Java: test implementations of SDK client interfaces (AWS). Rust: TBD |
| integrating-external-sdk-no-interface | Y | — | Java: simulator pattern for concrete SDK classes. Rust: TBD |
| integrating-external-api | Y | — | Java: custom interface + HTTP impl + test double. Rust: TBD |
| adding-flyway-migrations | Y | N/A | Java/SQL-specific. Rust uses manual SQL migration files |
| setting-up-docker-for-tests | Y | N/A | Java: Postgres via docker-compose. Rust: SQLite in-memory, no Docker needed |

### Documentation

| Skill | Java/Spring Boot | Rust CLI | Notes |
|---|---|---|---|
| project-documentation | Y | Y | Same structure: README, docs/, feature docs |

## Gaps and Priorities

### Rust CLI — missing skills that should be portable

1. **naming-conventions** — Formalize the `*Service`, `*Client`, `*Calculator`, `*Repository` suffixes
2. **configuration** — CLI args via `clap`, env var binding, config file support
3. **logging** — Structured logging via `tracing` crate

### Java/Spring Boot — missing skills that Rust has

1. **test-doubles** — Java covers this implicitly across three skills (`integrating-external-sdk`, `integrating-external-api`, `integrating-external-sdk-no-interface`). Consider a unified overview skill.

### Cross-cutting — not yet in either project

1. **CI/CD** — Build, test, release pipeline patterns
2. **graceful-shutdown** — Startup/shutdown lifecycle patterns
