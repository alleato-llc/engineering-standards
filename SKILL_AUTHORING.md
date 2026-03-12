# Skill Authoring Guide

Rules for writing skill files across reference projects. Following this structure prevents drift between platform-specific implementations of the same skill.

## Frontmatter

Every `SKILL.md` starts with YAML frontmatter:

```yaml
---
name: skill-name
description: One-line description of the skill. End with "Use when..." to clarify when to apply it.
version: 1.0.0
---
```

- **name**: Matches the directory name. Lowercase, hyphenated.
- **description**: Concise but specific. Always end with a "Use when..." clause (e.g., "Use when writing or reviewing integration tests.").
- **version**: Semantic version matching engineering-standards. See [VERSIONING.md](VERSIONING.md).

## Required Sections

Skills must use these sections in this order. Omit a section only if it genuinely does not apply.

```markdown
# Skill Name

One-paragraph intro: what this skill covers and why it matters.

## Shared rules                     (if the skill spans multiple component types)

Cross-cutting principles that apply regardless of language or component.
Use `### N. Rule name` numbered subsections with code examples.

## {Platform-specific sections}     (the bulk of the skill)

Language/framework-specific patterns, examples, and rules.
Heading names should match across projects where the concept is the same
(e.g., "## Service pattern" in both Java and Rust).

## Conventions

Bullet list of conventions. Short, scannable, imperative voice.

## Checklist

Verification checklist for writing or reviewing code that uses this skill.
Use `- [ ]` checkbox format.
```

### Section details

| Section | Purpose | Required? |
|---|---|---|
| Intro paragraph | What and why, under the `# Skill Name` heading | Yes |
| Shared rules | Cross-cutting principles (numbered `### N. Title` subsections) | When skill covers multiple component types |
| Platform sections | Language-specific patterns with code examples | Yes |
| Conventions | Scannable rules list | Yes |
| Checklist | Verification items for writing/reviewing | Yes |

## Writing Principles

### Shared concepts get the same heading name

If Java and Swift both cover "Method sizing", use `### Method size` in both — not `### Method Sizing` in one and `## Method size guidelines` in the other.

### Number shared principles consistently

When a skill has ordered principles (like test-data-isolation), use `### N. Title` format and keep the same numbers across projects for shared concepts:

```markdown
## Principles

### 1. Every test creates its own data
### 2. Use random identifiers
### 3. Distinguish domain data from contextual data
### 4. {Platform-specific reset mechanism}
```

Platform-specific principles append at the end or replace a generic slot.

### Description field format

Always end with "Use when...":

```yaml
# Good
description: Ensures tests are independent by using random IDs and fresh data per test. Use when writing or reviewing tests.

# Bad — no guidance on when to apply
description: Random UUIDs and fresh data per test with factory helpers
```

### Checklists are mandatory

Every skill ends with a checklist. Items should be verifiable by reading the code:

```markdown
## Checklist

- [ ] Each test creates its own domain data
- [ ] All IDs are random — no hardcoded strings
- [ ] Assertions reference the test's own data
```

### Conventions section is a scannable list

Use imperative bullet points, not paragraphs:

```markdown
## Conventions

- Store enums as String rawValue in SwiftData
- One repository per aggregate root
- Never expose ModelContext to ViewModels directly
```

## Cross-Project Alignment

When creating or updating a skill that exists in multiple projects:

1. Read the skill in all projects that implement it before making changes
2. Ensure shared concepts use the same heading names and principle numbers
3. Platform-specific content goes in platform-specific sections — don't omit shared concepts
4. Update all implementations when adding a new shared concept (e.g., adding a checklist)
5. Update the engineering-standards matrix and changelog
