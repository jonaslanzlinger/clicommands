```markdown
# Feature Specification: Command Snippets (terminal tool)

**Feature Branch**: `001-cli-commands`  
**Created**: 2025-11-01  
**Status**: Draft  
**Input**: User description: "Create a terminal-integrated tool invoked as 'clicommands' that lets users store command snippets (CLI and other useful commands), search them, take commands from the clipboard, assign tags to commands, and search commands by tags. Make the tool very lightweight and easy to use."

## User Scenarios & Testing _(mandatory)_

### User Story 1 - Store a command snippet quickly (Priority: P1)

As a terminal user, I want to store a frequently-used command snippet (shell commands, SQL snippets, Git workflows, editor commands, etc.) so I can recall and re-run or reuse it later without retyping it.

**Why this priority**: This is the core value of the tool — short-term and long-term productivity improvements for CLI and development tasks.

**Independent Test**: Start the tool, add a new snippet, then list or search for it and verify the stored snippet appears with correct text, tags, and context.

**Acceptance Scenarios**:

1. **Given** no stored command with the same identifier, **When** the user saves a command with optional tags, **Then** the command is persisted and visible in lists/search results.
2. **Given** a stored command, **When** the user requests details for that command, **Then** they see the exact command text and its tags.

---

### User Story 2 - Search commands by text or tag (Priority: P1)

As a user, I want to search my saved commands by keyword or tag so I can quickly find the right command.

**Why this priority**: Fast retrieval is required for the tool to save time and be adopted.

**Independent Test**: Save several commands with distinct keywords and tags, perform keyword and tag searches, and verify returned results match the query.

**Acceptance Scenarios**:

1. **Given** multiple stored commands, **When** the user searches by a keyword present in command text, **Then** commands containing the keyword are returned ordered by relevance.
2. **Given** multiple stored commands with tags, **When** the user searches by tag, **Then** only commands with that tag are returned.

---

### User Story 3 - Import snippet from clipboard (Priority: P2)

As a user copying commands or snippets from elsewhere, I want to import the clipboard content into the tool so I can save it without retyping.

**Why this priority**: Improves convenience and lowers friction when capturing snippets from docs, web pages, or clipboard history.

**Independent Test**: Put a snippet in the system clipboard, invoke the clipboard-import flow, and confirm the snippet was added with the clipboard content as text and an optional detected context.

**Acceptance Scenarios**:

1. **Given** the clipboard contains a non-empty snippet string, **When** the user chooses to import from clipboard, **Then** a new stored snippet is created with that text.
2. **Given** the clipboard is empty or contains non-snippet data, **When** the user attempts import, **Then** the tool shows a clear message and does not create an invalid entry.

---

### User Story 4 - Tag management and assignment (Priority: P2)

As a user, I want to assign and remove tags on saved snippets so I can categorize and find snippets by context.

**Why this priority**: Tags make search and organization far more useful for power users.

**Independent Test**: Add tags to a saved snippet, search by those tags, remove a tag, and verify search results update accordingly.

**Acceptance Scenarios**:

1. **Given** a stored snippet, **When** the user assigns one or more tags, **Then** the tags are associated with the snippet and visible in searches.
2. **Given** a tag is removed from a snippet, **When** the user searches by that tag, **Then** the snippet is no longer returned.

---

### Edge Cases

-  Duplicate commands: if a user saves the same command text multiple times, the tool should either deduplicate or store distinct entries with clear metadata (timestamp) so users can distinguish them.
-  Very long commands: the tool should accept long command strings and surface them in a readable way (e.g., truncated in lists with full detail view).
-  Empty or invalid clipboard content on import should not create entries and should present the user with a clear message.
-  Tag collisions (same tag with different casing) should be normalized to a consistent form for search.

## Requirements _(mandatory)_

### Functional Requirements

-  **FR-001**: The system MUST allow a user to store a command entry containing the command text and optional metadata such as tags and a short note.
-  **FR-002**: The system MUST provide a search function that returns stored commands matching keywords in the command text.
-  **FR-003**: The system MUST allow users to create, assign, and remove textual tags for stored commands.
-  **FR-004**: The system MUST support searching commands by tag (single-tag and multi-tag intersection/AND search).
-  **FR-005**: The system MUST allow importing a command from the system clipboard as a new command entry, with validation to avoid empty entries.
-  **FR-006**: The system MUST provide a small set of list and detail views: list stored commands, view single command with tags and notes, and simple pagination or limits for long lists.
-  **FR-007**: The system MUST be lightweight and usable locally without requiring remote services by default (assumption documented below).

### Key Entities _(include if feature involves data)_

-  **CommandEntry**: Represents a saved command snippet. Key attributes: id, command_text (the snippet text), context (optional, e.g., "shell", "sql", "git", "editor"), tags (list of strings), note (optional), created_at, last_used_at (optional).
-  **Tag**: A simple textual label. Key attributes: name (normalized for case), count (optional derived), list of associated CommandEntry ids.

## Success Criteria _(mandatory)_

### Measurable Outcomes

-  **SC-001**: Primary workflows (store, search by keyword, import from clipboard, and search by tag) are executable end-to-end by a user in under 3 steps/interactions on average.
-  **SC-002**: 95% of keyword and tag searches return relevant results within 1 second on a typical developer laptop for datasets up to 5,000 stored commands.
-  **SC-003**: A user can successfully import non-empty clipboard content into a stored command in at least 95% of attempts (measured by a small user test suite).
-  **SC-004**: The tool remains a lightweight local utility — initial install and first run complete without manual configuration in under 2 minutes.

## Assumptions

-  This is primarily a local, single-user CLI tool. No remote sync or authentication is required for the MVP.
-  Data is stored locally as a plain JSON file and designed for small to medium personal collections (up to ~5k entries). JSON is chosen for portability, ease of backup, and manual editing. If users need larger datasets or sync, that is out of scope for MVP.
-  Tag names are always stored and displayed in lowercase. This avoids confusion and ensures consistent search and tagging behavior.
-  When importing from clipboard, the tool never sets the snippet context automatically. The user must set context manually if desired.
-  The term "lightweight" implies minimal runtime dependencies and that the tool can be installed and run on common developer machines.

## Notes

-  Implementation choices (file format, exact storage engine, language) are intentionally omitted from this spec and left to implementation planning.
```

# Feature Specification: [FEATURE NAME]

**Feature Branch**: `[###-feature-name]`  
**Created**: [DATE]  
**Status**: Draft  
**Input**: User description: "$ARGUMENTS"

## User Scenarios & Testing _(mandatory)_

<!--
  IMPORTANT: User stories should be PRIORITIZED as user journeys ordered by importance.
  Each user story/journey must be INDEPENDENTLY TESTABLE - meaning if you implement just ONE of them,
  you should still have a viable MVP (Minimum Viable Product) that delivers value.
  
  ```markdown
  # Feature Specification: Command Snippets (terminal tool)

  **Feature Branch**: `001-cli-commands`  
  **Created**: 2025-11-01  
  **Status**: Draft  
  **Input**: User description: "Create a terminal-integrated tool invoked as 'clicommands' that lets users store command snippets (CLI and other useful commands), search them, take commands from the clipboard, assign tags to commands, and search commands by tags. Make the tool very lightweight and easy to use."

  ## User Scenarios & Testing *(mandatory)*


  ### User Story 1 - Store a command snippet quickly (Priority: P1)

  As a terminal user, I want to store a frequently-used command snippet (shell commands, SQL snippets, Git workflows, editor commands, etc.) so I can recall and re-run or reuse it later without retyping it.

  **Why this priority**: This is the core value of the tool — short-term and long-term productivity improvements for CLI and development tasks.

  **Independent Test**: Start the tool, add a new snippet, then list or search for it and verify the stored snippet appears with correct text, tags, and context.

  **Acceptance Scenarios**:

  1. **Given** no stored command with the same identifier, **When** the user saves a command with optional tags, **Then** the command is persisted and visible in lists/search results.
  2. **Given** a stored command, **When** the user requests details for that command, **Then** they see the exact command text and its tags.

  ---

  ### User Story 2 - Search commands by text or tag (Priority: P1)

  As a user, I want to search my saved commands by keyword or tag so I can quickly find the right command.

  **Why this priority**: Fast retrieval is required for the tool to save time and be adopted.

  **Independent Test**: Save several commands with distinct keywords and tags, perform keyword and tag searches, and verify returned results match the query.

  **Acceptance Scenarios**:

  1. **Given** multiple stored commands, **When** the user searches by a keyword present in command text, **Then** commands containing the keyword are returned ordered by relevance.
  2. **Given** multiple stored commands with tags, **When** the user searches by tag, **Then** only commands with that tag are returned.

  ---

  ### User Story 3 - Import snippet from clipboard (Priority: P2)

  As a user copying commands or snippets from elsewhere, I want to import the clipboard content into the tool so I can save it without retyping.

  **Why this priority**: Improves convenience and lowers friction when capturing snippets from docs, web pages, or clipboard history.

  **Independent Test**: Put a snippet in the system clipboard, invoke the clipboard-import flow, and confirm the snippet was added with the clipboard content as text and an optional detected context.

  **Acceptance Scenarios**:

  1. **Given** the clipboard contains a non-empty snippet string, **When** the user chooses to import from clipboard, **Then** a new stored snippet is created with that text.
  2. **Given** the clipboard is empty or contains non-snippet data, **When** the user attempts import, **Then** the tool shows a clear message and does not create an invalid entry.

  ---

  ### User Story 4 - Tag management and assignment (Priority: P2)

  As a user, I want to assign and remove tags on saved snippets so I can categorize and find snippets by context.

  **Why this priority**: Tags make search and organization far more useful for power users.

  **Independent Test**: Add tags to a saved snippet, search by those tags, remove a tag, and verify search results update accordingly.

  **Acceptance Scenarios**:

  1. **Given** a stored snippet, **When** the user assigns one or more tags, **Then** the tags are associated with the snippet and visible in searches.
  2. **Given** a tag is removed from a snippet, **When** the user searches by that tag, **Then** the snippet is no longer returned.

  ---

  ### Edge Cases

  - Duplicate commands: if a user saves the same command text multiple times, the tool should either deduplicate or store distinct entries with clear metadata (timestamp) so users can distinguish them.
  - Very long commands: the tool should accept long command strings and surface them in a readable way (e.g., truncated in lists with full detail view).
  - Empty or invalid clipboard content on import should not create entries and should present the user with a clear message.
  - Tag collisions (same tag with different casing) should be normalized to a consistent form for search.

  ## Requirements *(mandatory)*

  ### Functional Requirements

  - **FR-001**: The system MUST allow a user to store a command entry containing the command text and optional metadata such as tags and a short note.
  - **FR-002**: The system MUST provide a search function that returns stored commands matching keywords in the command text.
  - **FR-003**: The system MUST allow users to create, assign, and remove textual tags for stored commands.
  - **FR-004**: The system MUST support searching commands by tag (single-tag and multi-tag intersection/AND search).
  - **FR-005**: The system MUST allow importing a command from the system clipboard as a new command entry, with validation to avoid empty entries.
  - **FR-006**: The system MUST provide a small set of list and detail views: list stored commands, view single command with tags and notes, and simple pagination or limits for long lists.
  - **FR-007**: The system MUST be lightweight and usable locally without requiring remote services by default (assumption documented below).

  ### Key Entities *(include if feature involves data)*

  - **CommandEntry**: Represents a saved command snippet. Key attributes: id, command_text (the snippet text), context (optional, e.g., "shell", "sql", "git", "editor"), tags (list of strings), note (optional), created_at, last_used_at (optional).
  - **Tag**: A simple textual label. Key attributes: name (normalized for case), count (optional derived), list of associated CommandEntry ids.

  ## Success Criteria *(mandatory)*

  ### Measurable Outcomes

  - **SC-001**: Primary workflows (store, search by keyword, import from clipboard, and search by tag) are executable end-to-end by a user in under 3 steps/interactions on average.
  - **SC-002**: 95% of keyword and tag searches return relevant results within 1 second on a typical developer laptop for datasets up to 5,000 stored commands.
  - **SC-003**: A user can successfully import non-empty clipboard content into a stored command in at least 95% of attempts (measured by a small user test suite).
  - **SC-004**: The tool remains a lightweight local utility — initial install and first run complete without manual configuration in under 2 minutes.

  ## Assumptions

  - This is primarily a local, single-user CLI tool. No remote sync or authentication is required for the MVP.
  - Data is stored locally (file or lightweight local store) and designed for small to medium personal collections (up to ~5k entries). If users need larger datasets or sync, that is out of scope for MVP.
  - Tag names are normalized to lowercase for search and storage.
  - The term "lightweight" implies minimal runtime dependencies and that the tool can be installed and run on common developer machines.

  ## Notes

  - Implementation choices (file format, exact storage engine, language) are intentionally omitted from this spec and left to implementation planning.

  ```
