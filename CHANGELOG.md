# Changelog

Organized by skill. Each entry describes what changed and why, so projects behind on a version know whether updating matters and what code changes are needed.

## project-structure

### 1.0.0 — 2026-03-12
Initial versioned release. Domain-oriented layout, module/package size constraints, templatized with `{core_domain}`/`{subdomain}` placeholders. Java: layered core domain packages. Rust: lib/bin split, flat subdomain modules. Swift: modular SPM packages (Core/Services/TestSupport), 7-file directory limit.

## component-design

### 1.0.0 — 2026-03-12
Initial versioned release. Shared rules (single responsibility, method sizing, method composition at one level of abstraction, composition over inheritance). Java: controllers/services/repos/clients/pub-sub. Rust: services/repos/clients/calculators. Swift: Views/ViewModels/Repos/Clients/Calculators.

## naming-conventions

### 1.0.0 — 2026-03-12
Initial versioned release. `*Service`, `*Client`, `*Calculator` suffixes. Technology-prefixed implementations. Test naming conventions. Swift adds `*ViewModel`, `*View`, protocol plain names, `SwiftData*` prefix for impls.

## entity-design

### 1.0.0 — 2026-03-12
Initial versioned release. JPA `with*` fluent mutators, result records for pure computation, constructor-based initialization. Swift: SwiftData `@Model`, enum-as-String rawValue, `createdAt`/`modifiedAt` pattern.

## inversion-of-control

### 1.0.0 — 2026-03-12
Initial versioned release. Consolidates dependency-injection, trait-boundaries, and protocol-boundaries into one generic skill. Java: Spring `@Bean` methods, constructor injection, no `@Autowired` on fields. Rust: traits as contracts, `Box<dyn Trait>`, `RefCell` for test mutability. Swift: protocols as contracts, `DependencyContainer` struct, existential types (`any Protocol`).

## error-handling

### 1.0.0 — 2026-03-12
Initial versioned release. Java: minimal exception hierarchy (abstract base + 4 subclasses), `@ControllerAdvice` maps type to HTTP status, context maps. Rust: `thiserror` enums per boundary, `anyhow` for application, `#[from]` propagation. Swift: error enum with associated values, `ErrorPresenter` for centralized UI display.

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
Initial versioned release. Unit vs integration decision table, test the contract principle. Java: JUnit + AssertJ, `@Nested`/`@DisplayName`. Rust: `#[test]` in `tests/` directory. Swift: Swift Testing (`@Suite`, `@Test`, `#expect`), `@MainActor` for ViewModel tests.

## adding-integration-tests

### 1.0.0 — 2026-03-12
Initial versioned release. Observable side effect assertions, derive-from-inputs pattern, negative assertions. Java: typed HTTP clients, `BaseIntegrationTest`. Rust: test doubles + real SQLite. Swift: ViewModel tests with test doubles, repository tests with in-memory SwiftData.

## test-data-isolation

### 1.0.0 — 2026-03-12
Initial versioned release. Random IDs, domain vs contextual data distinction, checklist. Java: `UUID.randomUUID()`, `@BeforeEach` reset. Rust: fresh service/repo per test, `tempfile` for I/O. Swift: `UUID()`, in-memory SwiftData, `TestRecipeFactory`.

## testing-boundaries

### 1.0.0 — 2026-03-12
Initial versioned release. Consolidates `test-doubles`, `integrating-external-sdk`, `integrating-external-sdk-no-interface`, and `integrating-external-api` into one skill organized around contract fidelity. Shared principles: fakes over mocks, contract fidelity, call capture, configurable errors, reset between tests. Java: three patterns (SDK with interface, simulator for concrete classes, custom interface for REST APIs), `throwWhen`, `ExpectedException<T>`, `TestConfiguration`/`BaseIntegrationTest` wiring. Rust: `RefCell` for interior mutability, `Rc<Recording>` for shared assertions, one file per trait in `tests/support/`. Swift: protocol-conforming fakes in TestSupport package, `@MainActor` isolation, `errorToThrow` for failure injection.

## schema-migrations

### 1.0.0 — 2026-03-12
Initial versioned release. Renamed from `adding-flyway-migrations` to support multiple persistence backends. Java: Flyway versioned SQL files, `FlywayMigrationIntegrationTest`, `ALTER TABLE` patterns. Swift: SwiftData `VersionedSchema` + `SchemaMigrationPlan`, lightweight migration stages, full model redeclaration per version.

## setting-up-docker-for-tests

### 1.0.0 — 2026-03-12
Initial versioned release. Docker-managed Postgres, decision framework for docker vs test doubles, no Testcontainers.

## project-documentation

### 1.0.0 — 2026-03-12
Initial versioned release. Required root files (README, CONTRIBUTING, LICENSE, SECURITY, CLAUDE.md), docs/ structure, feature doc template, when-to-update table.

## view-architecture

### 1.0.0 — 2026-03-12
Initial versioned release. Swift: thin SwiftUI views, `@Environment` for DI, `NavigationStack` + `navigationDestination`, `.task` for async loading, `.alert` for errors, `.sheet` for modals. Generic name — other projects can add their UI patterns.

## concurrency

### 1.0.0 — 2026-03-12
Initial versioned release. Java: virtual threads as default, structured concurrency (`StructuredTaskScope`) for fan-out, `CompletableFuture` composition rules, no `@Async`, connection pool protection via `Semaphore`, transaction boundary rules, bulk data partitioning, context propagation. Swift: `async`/`await` for all async operations, `@MainActor` only for ViewModels, services non-isolated, `Task { }` for sync-to-async bridging, `Sendable` conformance. Generic name — Rust could add tokio.

## state-management

### 1.0.0 — 2026-03-12
Initial versioned release. Swift: `@Observable` for ViewModels (per-property tracking), `@State` for view-local state, `@Environment` for DI, `@Bindable` for two-way binding, `@AppStorage` for UserDefaults. Generic name — covers reactive state in any UI framework.

## persistence

### 1.0.0 — 2026-03-12
Initial versioned release. Swift: SwiftData `@Model` entities, `ModelContainer` at app startup, `ModelConfiguration(isStoredInMemoryOnly: true)` for tests, `FetchDescriptor` with `#Predicate`. Generic name — unifies Java entity-design + flyway and Rust SQLite patterns.
