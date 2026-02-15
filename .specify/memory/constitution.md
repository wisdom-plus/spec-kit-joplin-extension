<!--
Sync Impact Report
- Version change: template → 1.0.0
- Modified principles: New set defined (Code Quality & Maintainability; Security & Privacy by Design;
  Performance & Responsiveness; Joplin Compatibility & Stability; Testing & Review Discipline)
- Added sections: Joplin Extension Constraints; Development Workflow & Quality Gates
- Removed sections: None
- Templates requiring updates:
  - ✅ .specify/templates/plan-template.md
  - ✅ .specify/templates/spec-template.md
  - ✅ .specify/templates/tasks-template.md
- Follow-up TODOs: Ratification date needed
-->
# Joplin Extension Constitution

## Core Principles

### I. Code Quality & Maintainability
All extension code MUST be readable, typed, and modular. Enforce linting/formatting,
avoid large functions, and document non-obvious behavior. Public interfaces MUST be
stable and minimal to reduce future migration costs.

### II. Security & Privacy by Design
Extensions MUST request the least privilege, validate all inputs, and avoid unsafe
evaluation or shell execution. Secrets MUST NOT be logged or stored in plaintext.
Network access MUST be explicit, minimal, and documented in the spec.

### III. Performance & Responsiveness
User-visible actions MUST remain responsive. Long-running work MUST be asynchronous,
and large data operations MUST be incremental or cached. Performance regressions MUST
be measured and documented with a mitigation plan.

### IV. Joplin Compatibility & Stability
The extension MUST target supported Joplin APIs and degrade gracefully if a capability
is unavailable. Manifest and settings MUST remain backward compatible unless a
documented migration is provided.

### V. Testing & Review Discipline
Core logic MUST be covered by automated tests; any exception requires explicit
justification in the spec. Every change MUST pass lint, type checks, and tests before
review, and reviews MUST verify compliance with this constitution.

## Joplin Extension Constraints

- The extension MUST include a clear manifest with accurate permissions and metadata.
- User data storage MUST be minimal, scoped to the feature, and documented.
- External dependencies MUST be pinned and periodically reviewed for security updates.
- UI changes MUST follow Joplin UX conventions to avoid confusing behavior.

## Development Workflow & Quality Gates

- Specs MUST include security and performance considerations before implementation.
- Changes MUST include tests or a documented exception approved in review.
- Performance-sensitive code MUST include a measurement plan or benchmark notes.
- Release notes MUST list user-visible changes and any migrations.

## Governance

- This constitution supersedes other guidance when conflicts arise.
- Amendments require documented rationale, impact analysis, and approval in review.
- Versioning follows semantic versioning: MAJOR for breaking governance changes,
  MINOR for new principles/sections, PATCH for clarifications.
- Compliance MUST be checked in plan/spec/tasks templates and in code reviews.

**Version**: 1.0.0 | **Ratified**: TODO(RATIFICATION_DATE): original adoption date unknown | **Last Amended**: 2026-01-24
