# Implementation Plan: Kindle Highlights Import

**Branch**: `001-kindle-highlights` | **Date**: 2026-01-24 | **Spec**: /Users/tomoshi/repo/sdd/joplin-extension/specs/001-kindle-highlights/spec.md
**Input**: Feature specification from `/Users/tomoshi/repo/sdd/joplin-extension/specs/001-kindle-highlights/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/commands/plan.md` for the execution workflow.

## Summary

Kindle Cloud Reader のハイライトをスクレイピングし、書籍ごとに新規ノートへ取り込む
Joplin 拡張を作る。埋め込みログインでセッションを得て、重複は「書籍+本文+位置」で排除。
コードはシンプルで読みやすく、最小依存・最小権限を守る。

## Technical Context

**Language/Version**: TypeScript (Joplin plugin standard)  
**Primary Dependencies**: Joplin Plugin API, embedded webview/DOM APIs  
**Storage**: Joplin settings (key-value) for import fingerprints  
**Testing**: Jest (unit for parser/dedupe) + lightweight integration tests  
**Target Platform**: Joplin Desktop (Windows/macOS/Linux)  
**Project Type**: single  
**Performance Goals**: 1 book import completes <30s; UI remains responsive  
**Constraints**: no credential persistence, minimal permissions, avoid heavy deps,
keep code simple/readable  
**Scale/Scope**: typical 0-5,000 highlights total; 0-500 per book

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- Code Quality & Maintainability: typing, linting, and modular structure planned
- Security & Privacy: least privilege, input validation, secrets handling documented
- Performance & Responsiveness: async strategy and measurement plan defined
- Joplin Compatibility: target API/manifest compatibility and migration notes confirmed
- Testing & Review Discipline: test approach and exceptions (if any) documented

**Gate Status (pre-research)**: PASS

## Project Structure

### Documentation (this feature)

```text
/Users/tomoshi/repo/sdd/joplin-extension/specs/001-kindle-highlights/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
└── tasks.md
```

### Source Code (repository root)

```text
/Users/tomoshi/repo/sdd/joplin-extension/
src/
├── core/
├── import/
├── ui/
└── lib/

tests/
├── integration/
└── unit/
```

**Structure Decision**: Single project under repo root with src/ and tests/.

## Complexity Tracking

No constitution violations detected; no complexity exceptions required.

## Phase 0: Research (Completed)

Output: `/Users/tomoshi/repo/sdd/joplin-extension/specs/001-kindle-highlights/research.md`

## Phase 1: Design & Contracts (Completed)

Output:
- `/Users/tomoshi/repo/sdd/joplin-extension/specs/001-kindle-highlights/data-model.md`
- `/Users/tomoshi/repo/sdd/joplin-extension/specs/001-kindle-highlights/contracts/highlights-import.openapi.yaml`
- `/Users/tomoshi/repo/sdd/joplin-extension/specs/001-kindle-highlights/quickstart.md`

**Gate Status (post-design)**: PASS
