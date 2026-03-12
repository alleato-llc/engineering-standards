# Changelog

Organized by skill. Each entry describes what changed and why, so projects behind on a version know whether updating matters and what code changes are needed.

## project-structure

### 1.0.0 — 2026-03-12
Initial versioned release. Domain-oriented layout, module/package size constraints, templatized with `{core_domain}`/`{subdomain}` placeholders. Java: layered core domain packages. Rust: lib/bin split, flat subdomain modules.

## component-design

### 1.0.0 — 2026-03-12
Initial versioned release. Shared rules (single responsibility, method sizing, method composition at one level of abstraction, composition over inheritance). Java: controllers/services/repos/clients/pub-sub. Rust: services/repos/clients/calculators.

## naming-conventions

### 1.0.0 — 2026-03-12
Initial versioned release. `*Service`, `*Client`, `*Calculator` suffixes. Technology-prefixed implementations. Test naming conventions.

## entity-design

### 1.0.0 — 2026-03-12
Initial versioned release. JPA `with*` fluent mutators, result records for pure computation, constructor-based initialization.

## dependency-injection

### 1.0.0 — 2026-03-12
Initial versioned release. Constructor injection only, no `@Autowired` on fields, `@Bean` methods own object creation.

## trait-boundaries

### 1.0.0 — 2026-03-12
Initial versioned release. Traits as contracts, `Box<dyn Trait>` for DI, production vs test implementation pattern.

## error-handling

### 1.0.0 — 2026-03-12
Initial versioned release. Java: minimal exception hierarchy (abstract base + 4 subclasses), `@ControllerAdvice` maps type to HTTP status, context maps. Rust: `thiserror` enums per boundary, `anyhow` for application, `#[from]` propagation.

## configuration

### 1.0.0 — 2026-03-12
Initial versioned release. `@ConfigurationProperties` with project-name prefix, env var binding, nested config decomposition, sensitive value protection.

## logging

### 1.0.0 — 2026-03-12
Initial versioned release. SLF4J + structured JSON, `@Redacted` annotation, log level guidelines, boundary logging.

## tracing

### 1.0.0 — 2026-03-12
Initial versioned release. Micrometer Tracing, correlation ID propagation (HTTP auto, SQS/SNS via message attributes), MDC utilities.

## adding-unit-tests

### 1.0.0 — 2026-03-12
Initial versioned release. Unit vs integration decision table, test the contract principle. Java: JUnit + AssertJ, `@Nested`/`@DisplayName`. Rust: `#[test]` in `tests/` directory.

## adding-integration-tests

### 1.0.0 — 2026-03-12
Initial versioned release. Observable side effect assertions, derive-from-inputs pattern, negative assertions. Java: typed HTTP clients, `BaseIntegrationTest`. Rust: test doubles + real SQLite.

## test-data-isolation

### 1.0.0 — 2026-03-12
Initial versioned release. Random IDs, domain vs contextual data distinction, checklist. Java: `UUID.randomUUID()`, `@BeforeEach` reset. Rust: fresh service/repo per test, `tempfile` for I/O.

## test-doubles

### 1.0.0 — 2026-03-12
Initial versioned release. Rust-specific: `RefCell` for interior mutability, `Rc<Recording>` for shared assertions, one file per trait in `tests/support/`.

## integrating-external-sdk

### 1.0.0 — 2026-03-12
Initial versioned release. Test implementations of SDK client interfaces, `throwWhen` for failure simulation, call recording.

## integrating-external-sdk-no-interface

### 1.0.0 — 2026-03-12
Initial versioned release. Simulator pattern for concrete SDK classes via Mockito, `ExpectedException<T>` infrastructure, stateless vs stateful simulators.

## integrating-external-api

### 1.0.0 — 2026-03-12
Initial versioned release. Custom interface + HTTP impl + in-memory test double, `@Profile("!test")`, `throwWhen` for failures.

## adding-flyway-migrations

### 1.0.0 — 2026-03-12
Initial versioned release. Versioned SQL files, `FlywayMigrationIntegrationTest`, `ALTER TABLE` patterns.

## setting-up-docker-for-tests

### 1.0.0 — 2026-03-12
Initial versioned release. Docker-managed Postgres, decision framework for docker vs test doubles, no Testcontainers.

## project-documentation

### 1.0.0 — 2026-03-12
Initial versioned release. Required root files (README, CONTRIBUTING, LICENSE, SECURITY, CLAUDE.md), docs/ structure, feature doc template, when-to-update table.
