# Feature Specification: Kindle Highlights Import

**Feature Branch**: `001-kindle-highlights`  
**Created**: 2026-01-24  
**Status**: Draft  
**Input**: User description: "joplinの拡張機能を作成します amazonのkindleのハイライトをノートにコピーする拡張機能"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Import highlights into a note (Priority: P1)

As a Joplin user, I want to bring my Kindle highlights into a Joplin note so I can
review them alongside my other notes.

**Why this priority**: This is the core value: getting Kindle highlights into Joplin.

**Independent Test**: Can be tested by importing highlights for one book and
confirming a note is created with all highlights.

**Acceptance Scenarios**:

1. **Given** I have access to my Kindle highlights, **When** I start an import for a
   selected book, **Then** a new Joplin note is created containing those highlights.
2. **Given** an import completes, **When** I open the created note, **Then** the
   highlights are readable and associated with the correct book title.

---

### User Story 2 - Choose target note behavior (Priority: P2)

As a user, I want to choose whether highlights go into a new note or an existing note
so I can organize my notebook structure.

**Why this priority**: Users often have existing notebooks/notes and need control
over where the import lands.

**Independent Test**: Can be tested by selecting an existing note and confirming
highlights are appended without overwriting existing content.

**Acceptance Scenarios**:

1. **Given** I select an existing note as the target, **When** I import highlights,
   **Then** the highlights are added without deleting prior content.

---

### User Story 3 - Avoid duplicate imports (Priority: P3)

As a user, I want repeated imports to avoid duplicating the same highlight so my
notes stay clean.

**Why this priority**: Importing more than once is common, and duplicates reduce
note quality.

**Independent Test**: Can be tested by importing the same book twice and confirming
no duplicate highlights are added.

**Acceptance Scenarios**:

1. **Given** I already imported a book, **When** I import it again, **Then** the
   note does not contain duplicate highlight entries.

---

### Edge Cases

- What happens when the highlights source has no highlights for a selected book?
- How does the system handle partial or interrupted imports?
- What happens when highlight text includes unusual characters or very long passages?

## Security & Performance Considerations *(mandatory)*

### Security

- Permissions/least privilege: Only the minimum Joplin permissions required to
  create or update notes.
- Input validation: Validate highlight content and book metadata before writing
  to notes.
- Secrets handling: Avoid storing credentials; if needed, only keep them in memory
  for the session.
- Network access: Fetch highlights by scraping the Kindle Cloud Reader highlights
  page, which requires Amazon login.

### Performance

- User-visible latency target: An import for a single book completes in under
  30 seconds on typical libraries.
- Long-running work: Large imports run asynchronously with progress feedback.
- Measurement plan: Track import duration, highlight count, and failure rate.

## Assumptions

- Users already have a Joplin account and can install extensions.
- Highlights are associated with a book title and can be grouped per book.
- Users expect imports to preserve highlight order as provided by the source.

## Clarifications

### Session 2026-01-24

- Q: How is Amazon login handled for scraping? → A: Users log in directly within the
  extension (web view) and the session is used for scraping.
- Q: What uniqueness rule is used to avoid duplicates? → A: Book + highlight text +
  location/page.
- Q: How should import failures be handled? → A: Show a clear error; user initiates
  retry.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST let users initiate an import of Kindle highlights.
- **FR-002**: System MUST allow selecting a book (or collection) to import.
- **FR-003**: System MUST create a new note or append to an existing note based on
  user choice.
- **FR-004**: System MUST avoid duplicating highlights across repeated imports for
  the same target note using a book + highlight text + location/page uniqueness rule.
- **FR-005**: System MUST clearly report import success or failure to the user.
- **FR-005a**: System MUST show a clear error message on failure and allow users to
  retry manually.
- **FR-006**: System MUST handle missing or malformed highlight data without
  crashing.
- **FR-007**: System MUST respect user privacy and avoid storing sensitive
  credentials beyond the active session.
- **FR-007a**: System MUST allow users to log in within the extension UI and reuse
  the active session for scraping without persisting credentials.
- **FR-008**: System MUST support cancellation of an in-progress import without
  corrupting notes.
- **FR-009**: System MUST provide a way to choose the target note location
  (new note vs existing note). Default is a new note per book.
- **FR-010**: System MUST define how highlights are formatted inside the note
  (e.g., grouped by book, include location/date). Each highlight includes the
  book title only.

### Key Entities *(include if feature involves data)*

- **Highlight**: The text excerpt and any associated metadata (e.g., book title,
  location).
- **Book**: The source item containing a set of highlights.
- **Import Session**: A record of an import run, used to prevent duplicates.
- **Target Note**: The Joplin note that receives imported highlights.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: 90% of users can complete an import for one book in under 3 minutes
  without assistance.
- **SC-002**: Duplicate highlights are reduced to zero for repeated imports of the
  same book.
- **SC-003**: 95% of imports complete successfully without requiring retries.
- **SC-004**: Users rate the imported notes as easy to read and organize (average
  4/5 or higher in feedback).
