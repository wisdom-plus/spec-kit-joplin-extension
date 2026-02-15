---

description: "Task list template for feature implementation"
---

# Tasks: Kindle Highlights Import

**Input**: Design documents from `/Users/tomoshi/repo/sdd/joplin-extension/specs/001-kindle-highlights/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Tests**: The examples below include test tasks. Tests are REQUIRED unless the
spec explicitly documents an approved exception.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

- **Single project**: `src/`, `tests/` at repository root
- Paths shown below assume single project - adjust based on plan.md structure

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure

- [ ] T001 Create base folders per plan in /Users/tomoshi/repo/sdd/joplin-extension/src/ and /Users/tomoshi/repo/sdd/joplin-extension/tests/
- [ ] T002 [P] Add minimal plugin manifest in /Users/tomoshi/repo/sdd/joplin-extension/src/manifest.json
- [ ] T003 [P] Configure lint/format scripts in /Users/tomoshi/repo/sdd/joplin-extension/package.json
- [ ] T004 [P] Add testing config in /Users/tomoshi/repo/sdd/joplin-extension/tests/jest.config.js

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

- [ ] T005 Implement plugin entry and registration in /Users/tomoshi/repo/sdd/joplin-extension/src/index.ts
- [ ] T006 [P] Create settings storage wrapper for fingerprints in /Users/tomoshi/repo/sdd/joplin-extension/src/core/settingsStore.ts
- [ ] T007 [P] Define import session types in /Users/tomoshi/repo/sdd/joplin-extension/src/core/types.ts
- [ ] T008 Create shared error/result helpers in /Users/tomoshi/repo/sdd/joplin-extension/src/lib/result.ts

**Checkpoint**: Foundation ready - user story implementation can now begin in parallel

---

## Phase 3: User Story 1 - Import highlights into a note (Priority: P1) 🎯 MVP

**Goal**: Import highlights for a selected book into a new Joplin note

**Independent Test**: Import one book and confirm a new note contains all highlights

### Tests for User Story 1 (REQUIRED unless exception is approved) ⚠️

- [ ] T009 [P] [US1] Add parser unit tests in /Users/tomoshi/repo/sdd/joplin-extension/tests/unit/highlightParser.test.ts
- [ ] T010 [P] [US1] Add note creation integration test in /Users/tomoshi/repo/sdd/joplin-extension/tests/integration/importNote.test.ts

### Implementation for User Story 1

- [ ] T011 [P] [US1] Build webview login panel in /Users/tomoshi/repo/sdd/joplin-extension/src/ui/loginPanel.ts
- [ ] T012 [P] [US1] Implement scraper to extract book list in /Users/tomoshi/repo/sdd/joplin-extension/src/import/scrapeBooks.ts
- [ ] T013 [P] [US1] Implement scraper to extract highlights for a book in /Users/tomoshi/repo/sdd/joplin-extension/src/import/scrapeHighlights.ts
- [ ] T014 [US1] Implement highlight parser/normalizer in /Users/tomoshi/repo/sdd/joplin-extension/src/import/parseHighlights.ts
- [ ] T015 [US1] Implement note creation writer in /Users/tomoshi/repo/sdd/joplin-extension/src/core/noteWriter.ts
- [ ] T016 [US1] Wire import flow (login -> select book -> create note) in /Users/tomoshi/repo/sdd/joplin-extension/src/import/importFlow.ts

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently

---

## Phase 4: User Story 2 - Choose target note behavior (Priority: P2)

**Goal**: Allow user to append highlights to an existing note

**Independent Test**: Import into an existing note and confirm previous content remains

### Tests for User Story 2 (REQUIRED unless exception is approved) ⚠️

- [ ] T017 [P] [US2] Add append behavior integration test in /Users/tomoshi/repo/sdd/joplin-extension/tests/integration/appendNote.test.ts

### Implementation for User Story 2

- [ ] T018 [P] [US2] Add note picker UI in /Users/tomoshi/repo/sdd/joplin-extension/src/ui/notePicker.ts
- [ ] T019 [US2] Update note writer to append mode in /Users/tomoshi/repo/sdd/joplin-extension/src/core/noteWriter.ts
- [ ] T020 [US2] Update import flow to route to selected note in /Users/tomoshi/repo/sdd/joplin-extension/src/import/importFlow.ts

**Checkpoint**: At this point, User Stories 1 AND 2 should both work independently

---

## Phase 5: User Story 3 - Avoid duplicate imports (Priority: P3)

**Goal**: Prevent duplicate highlight entries on repeated imports

**Independent Test**: Import same book twice and confirm no duplicates

### Tests for User Story 3 (REQUIRED unless exception is approved) ⚠️

- [ ] T021 [P] [US3] Add dedupe integration test in /Users/tomoshi/repo/sdd/joplin-extension/tests/integration/dedupe.test.ts

### Implementation for User Story 3

- [ ] T022 [P] [US3] Implement fingerprint builder in /Users/tomoshi/repo/sdd/joplin-extension/src/import/fingerprint.ts
- [ ] T023 [US3] Store and check fingerprints in /Users/tomoshi/repo/sdd/joplin-extension/src/core/settingsStore.ts
- [ ] T024 [US3] Apply dedupe before writing notes in /Users/tomoshi/repo/sdd/joplin-extension/src/import/importFlow.ts

**Checkpoint**: All user stories should now be independently functional

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories

- [ ] T025 [P] Add progress UI and cancellation in /Users/tomoshi/repo/sdd/joplin-extension/src/ui/progressPanel.ts
- [ ] T026 Add error messaging for common failures in /Users/tomoshi/repo/sdd/joplin-extension/src/ui/errorBanner.ts
- [ ] T027 [P] Update quickstart and README in /Users/tomoshi/repo/sdd/joplin-extension/specs/001-kindle-highlights/quickstart.md
- [ ] T028 [P] Add security/privacy notes in /Users/tomoshi/repo/sdd/joplin-extension/specs/001-kindle-highlights/research.md
- [ ] T029 Run quickstart validation in /Users/tomoshi/repo/sdd/joplin-extension/specs/001-kindle-highlights/quickstart.md

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3+)**: All depend on Foundational phase completion
  - User stories can then proceed in parallel (if staffed)
  - Or sequentially in priority order (P1 → P2 → P3)
- **Polish (Final Phase)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) - No dependencies on other stories
- **User Story 2 (P2)**: Can start after Foundational (Phase 2) - May integrate with US1 but should be independently testable
- **User Story 3 (P3)**: Can start after Foundational (Phase 2) - May integrate with US1/US2 but should be independently testable

### Within Each User Story

- Tests (if included) MUST be written and FAIL before implementation
- Models before services
- Services before endpoints
- Core implementation before integration
- Story complete before moving to next priority

### Parallel Opportunities

- All Setup tasks marked [P] can run in parallel
- All Foundational tasks marked [P] can run in parallel (within Phase 2)
- Once Foundational phase completes, all user stories can start in parallel (if team capacity allows)
- All tests for a user story marked [P] can run in parallel
- Different user stories can be worked on in parallel by different team members

---

## Parallel Example: User Story 1

```bash
# In parallel, after foundational tasks complete
T011 (login panel), T012 (scrapeBooks), T013 (scrapeHighlights), T009 (parser tests)
```
