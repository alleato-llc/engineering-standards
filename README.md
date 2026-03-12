# Engineering Standards

Canonical source of truth for software engineering patterns across projects and languages. Each reference project implements these patterns in a specific language/framework, guided by skills that codify the patterns as actionable rules.

## Reference Projects

| ID | Project | Language | Framework | Domain |
|---|---|---|---|---|
| **java** | [spring-boot-testing-reference](https://github.com/alleato-llc/spring-boot-reference) | Java 25 | Spring Boot | Order management |
| **rust** | [rust-cli-reference](https://github.com/alleato-llc/rust-cli-reference) | Rust | CLI/TUI | Expense tracking |
| **swift** | [swift-ios-reference](https://github.com/alleato-llc/swift-ios-reference) | Swift 6.0 | SwiftUI/iOS | Recipe/meal planning |

## Skill Matrix

Skills are portable patterns that guide code generation. Each skill defines rules, code examples, and conventions for a specific concern. Skills follow [semantic versioning](VERSIONING.md). See [CHANGELOG.md](CHANGELOG.md) for what changed in each version. See [SKILL_AUTHORING.md](SKILL_AUTHORING.md) for the required structure and writing guidelines.

**Legend:** version = implemented at that version, — = not yet defined or implemented, N/A = not applicable

| Skill | Category | Latest | java | rust | swift | Notes |
|---|---|---|---|---|---|---|
| project-structure | Core | 1.0.0 | 1.0.0 | 1.0.0 | 1.0.0 | Java: domain-oriented packages. Rust: domain-oriented modules. Swift: modular SPM packages |
| component-design | Core | 1.0.0 | 1.0.0 | 1.0.0 | 1.0.0 | Java: controllers/services/repos/clients. Rust: services/repos/clients. Swift: Views/ViewModels/Repos/Clients/Calculators |
| naming-conventions | Core | 1.0.0 | 1.0.0 | — | 1.0.0 | `*Service`, `*Client`, `*Calculator` suffixes. Swift adds `*ViewModel`, `*View` |
| entity-design | Core | 1.0.0 | 1.0.0 | N/A | 1.0.0 | Java: JPA `with*` fluent mutators. Swift: SwiftData `@Model`, enum-as-String |
| inversion-of-control | Core | 1.0.0 | 1.0.0 | 1.0.0 | 1.0.0 | Java: Spring `@Bean` + constructor injection. Rust: `Box<dyn Trait>`, `RefCell`. Swift: protocols + `DependencyContainer` |
| error-handling | Core | 1.0.0 | 1.0.0 | 1.0.0 | 1.0.0 | Java: exception hierarchy. Rust: `thiserror`. Swift: error enum + `ErrorPresenter` |
| configuration | Core | 1.0.0 | 1.0.0 | — | — | Java: `@ConfigurationProperties`, env vars, profiles |
| input-validation | Core | — | — | — | — | Where/how to validate, sanitization, boundary rules |
| api-design | Core | — | — | — | — | URL conventions, status codes, pagination, versioning, response shape |
| view-architecture | UI | 1.0.0 | N/A | N/A | 1.0.0 | Swift: thin SwiftUI views, `@Environment`, navigation patterns |
| concurrency | Infra | 1.0.0 | — | — | 1.0.0 | Swift: `async`/`await`, `@MainActor`. Java: virtual threads TBD. Rust: tokio TBD |
| state-management | UI | 1.0.0 | N/A | N/A | 1.0.0 | Swift: `@Observable`, `@State`, `@Environment`, `@Bindable` |
| persistence | Core | 1.0.0 | — | — | 1.0.0 | Swift: SwiftData `@Model`, `ModelContainer`. Java: covered by entity-design + flyway |
| authentication | Security | — | — | — | — | Auth flow patterns (JWT, OAuth2, API keys), middleware placement |
| authorization | Security | — | — | — | — | Role/permission checks, resource-level vs action-level, where checks live |
| secrets-management | Security | — | — | — | — | How secrets enter the app, rotation, what never goes in code |
| logging | Infra | 1.0.0 | 1.0.0 | — | — | Java: SLF4J, structured JSON, `@Redacted`. Swift: OSLog TBD. Rust: TBD |
| tracing | Infra | 1.0.0 | 1.0.0 | — | — | Java: Micrometer, MDC, message attribute propagation |
| adding-unit-tests | Test | 1.0.0 | 1.0.0 | 1.0.0 | 1.0.0 | Java: JUnit + AssertJ. Rust: `#[test]`. Swift: Swift Testing (`@Suite`, `@Test`) |
| adding-integration-tests | Test | 1.0.0 | 1.0.0 | 1.0.0 | 1.0.0 | Java: full app + Postgres. Rust: services + test doubles or real SQLite. Swift: ViewModels + test doubles, repositories + in-memory SwiftData |
| test-data-isolation | Test | 1.0.0 | 1.0.0 | 1.0.0 | 1.0.0 | Fresh data per test, random IDs, in-memory SwiftData for Swift |
| testing-boundaries | Test | 1.0.0 | 1.0.0 | 1.0.0 | 1.0.0 | Contract-honoring test doubles. Java: SDK interfaces + simulators + custom interfaces. Rust: RefCell/Rc trait fakes. Swift: protocol fakes |
| schema-migrations | Test | 1.0.0 | 1.0.0 | N/A | 1.0.0 | Java: Flyway versioned SQL. Swift: SwiftData VersionedSchema + SchemaMigrationPlan |
| setting-up-docker-for-tests | Test | 1.0.0 | 1.0.0 | N/A | N/A | Java: Postgres via docker-compose |
| project-documentation | Docs | 1.0.0 | 1.0.0 | 1.0.0 | 1.0.0 | Same structure: README, docs/, feature docs |
| project-bootstrap | Setup | — | — | — | — | Formatting, linting, git hooks, dependency scanning. See [BOOTSTRAP.md](BOOTSTRAP.md) |

## Gaps and Priorities

### Portable skills missing from Rust CLI

1. **naming-conventions** — Formalize the `*Service`, `*Client`, `*Calculator`, `*Repository` suffixes
2. **configuration** — CLI args via `clap`, env var binding, config file support
3. **logging** — Structured logging via `tracing` crate

### Swift/iOS gaps

1. **logging** — OSLog/Logger conventions, subsystem + category pattern
2. **configuration** — App configuration, feature flags, environment-based settings

### Java/Spring Boot gaps

1. **concurrency** — Virtual threads, structured concurrency
2. **persistence** — Covered by entity-design + flyway. Consider unified overview.

### Cross-cutting — not yet in any project

1. **input-validation** — Boundary validation rules, sanitization, reject vs coerce
2. **api-design** — URL shape, status codes, pagination, versioning, response conventions
3. **authentication** — JWT/OAuth2/API key patterns, middleware placement, accessing the authenticated user
4. **authorization** — Role/permission model, where checks live, resource-level access control
5. **secrets-management** — Extends configuration; vault integration, rotation, what never goes in code
6. **CI/CD** — Build, test, release pipeline patterns
7. **graceful-shutdown** — Startup/shutdown lifecycle patterns
