# Phase 0 Research: Kindle Highlights Import

## Decision 1: Target platform
- Decision: Joplin Desktop plugin (Electron-based) as the primary target.
- Rationale: Requires an embedded login flow and DOM scraping of the Kindle Cloud
  Reader highlights page, which aligns with desktop plugin capabilities.
- Alternatives considered: Joplin Mobile (limited plugin surface); CLI (no webview).

## Decision 2: Language and core API
- Decision: TypeScript using the Joplin Plugin API.
- Rationale: Standard for Joplin plugins, improves readability and safety.
- Alternatives considered: Plain JavaScript (less type safety).

## Decision 3: Amazon login and session use
- Decision: Users log in within an embedded webview; the active session is reused
  for scraping without persisting credentials.
- Rationale: Minimizes credential handling risk while enabling scraping.
- Alternatives considered: Cookie paste; external browser session reuse.

## Decision 4: Scraping approach
- Decision: DOM-based extraction from the Kindle Cloud Reader highlights page with
  incremental loading.
- Rationale: No official API; DOM extraction is straightforward and can be tested
  with fixtures.
- Alternatives considered: File import (not available); unofficial APIs (unstable).

## Decision 5: Deduplication strategy
- Decision: Deduplicate by (book title + highlight text + location/page) and store
  fingerprints in plugin settings for the target note.
- Rationale: Prevents duplicate imports without re-parsing the entire note each time.
- Alternatives considered: Parse existing note on every import (slower, fragile).

## Decision 6: Performance and UX
- Decision: Async import with progress indicator and manual retry on failure.
- Rationale: Keeps UI responsive and aligns with user-controlled retries.
- Alternatives considered: Synchronous import (UI freeze); auto-retry (less control).

## Decision 7: Testing focus
- Decision: Unit tests for parsing and deduplication; integration tests for note
  creation/appending.
- Rationale: Core logic is parser/dedupe; integration confirms Joplin note behavior.
- Alternatives considered: Manual-only testing (riskier).
