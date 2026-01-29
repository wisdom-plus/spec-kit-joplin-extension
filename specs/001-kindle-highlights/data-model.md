# Data Model: Kindle Highlights Import

## Entities

### Book
- **Fields**: title (string), author (string, optional), sourceId (string, optional)
- **Relationships**: has many Highlights
- **Notes**: sourceId is a stable identifier if available from the source page.

### Highlight
- **Fields**: text (string), bookTitle (string), location (string, optional),
  createdAt (string, optional)
- **Relationships**: belongs to Book
- **Validation**: text must be non-empty; trim whitespace; preserve original order.

### Target Note
- **Fields**: noteId (string), notebookId (string, optional), title (string)
- **Notes**: default is one new note per book unless user chooses existing note.

### Import Session
- **Fields**: sessionId (string), bookTitle (string), targetNoteId (string),
  startedAt (timestamp), status (enum: idle, in_progress, completed, failed, canceled),
  importedCount (number), errorMessage (string, optional)
- **Relationships**: references Book and Target Note
- **Validation**: status transitions must be linear (idle -> in_progress -> completed/failed/canceled).

## Uniqueness Rules

- Highlight uniqueness is defined by (book title + highlight text + location/page).
- Import Session is unique per run and tied to a target note.

## Data Volume Assumptions

- Typical libraries: 0-5,000 highlights; per book: 0-500 highlights.
- Imports should handle large books with incremental processing.
