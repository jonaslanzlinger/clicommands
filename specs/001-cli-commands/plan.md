
# Implementation Plan: Command Snippets (terminal tool)

**Branch**: `001-cli-commands` | **Date**: 2025-11-01 | **Spec**: [specs/001-cli-commands/spec.md](specs/001-cli-commands/spec.md)
**Input**: Feature specification from `/specs/001-cli-commands/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/commands/plan.md` for the execution workflow.

## Summary

Create a lightweight terminal tool (`clicommands`) for storing, searching, and tagging command snippets (CLI, SQL, git, editor, etc.), with import from clipboard, local JSON storage, and always-lowercase tags. No remote sync, no auto-detection of context, and designed for single-user productivity.

## Technical Context

**Language/Version**: Python 3.11 (recommended for CLI and JSON handling)
**Primary Dependencies**: click (CLI), pyperclip (clipboard), rich (optional, for output formatting), pytest (testing)
**Storage**: Local JSON file (portable, easy to back up and edit)
**Testing**: pytest
**Target Platform**: Linux/macOS/Windows terminal (cross-platform CLI)
**Project Type**: Single CLI tool (src/cli, src/models, src/services, src/lib)
**Performance Goals**: All search/import/list operations complete in <1s for up to 5,000 snippets
**Constraints**: Offline-capable, <50MB memory, no external services required
**Scale/Scope**: Single user, up to ~5,000 snippets, no multi-user or sync

## Constitution Check

GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.

- Library-First: Core logic (models, storage, search) will be implemented as importable modules, not just CLI glue.
- CLI Interface: All features accessible via CLI with text in/out, supporting both human and JSON output.
- Test-First: All features will have tests written before implementation (TDD cycle enforced).
- Integration Testing: Not required for MVP (single-user, no external integrations), but contract tests for CLI output will be included.
- Simplicity: No unnecessary complexity; single JSON file, no DB, no remote services.

No constitution violations detected. All gates pass for Phase 0.

## Project Structure

### Documentation (this feature)

```text
specs/[###-feature]/
├── plan.md              # This file (/speckit.plan command output)
├── research.md          # Phase 0 output (/speckit.plan command)
├── data-model.md        # Phase 1 output (/speckit.plan command)
├── quickstart.md        # Phase 1 output (/speckit.plan command)
├── contracts/           # Phase 1 output (/speckit.plan command)
└── tasks.md             # Phase 2 output (/speckit.tasks command - NOT created by /speckit.plan)
```

### Source Code (repository root)
<!--
  ACTION REQUIRED: Replace the placeholder tree below with the concrete layout
  for this feature. Delete unused options and expand the chosen structure with
  real paths (e.g., apps/admin, packages/something). The delivered plan must
  not include Option labels.
-->

```text
# [REMOVE IF UNUSED] Option 1: Single project (DEFAULT)
src/
├── models/
├── services/
├── cli/
└── lib/

tests/
├── contract/
├── integration/
└── unit/

# [REMOVE IF UNUSED] Option 2: Web application (when "frontend" + "backend" detected)
backend/
├── src/
│   ├── models/
│   ├── services/
│   └── api/
└── tests/

frontend/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/
└── tests/

# [REMOVE IF UNUSED] Option 3: Mobile + API (when "iOS/Android" detected)
api/
└── [same as backend above]

ios/ or android/
└── [platform-specific structure: feature modules, UI flows, platform tests]
```

**Structure Decision**: [Document the selected structure and reference the real
directories captured above]

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [e.g., 4th project] | [current need] | [why 3 projects insufficient] |
| [e.g., Repository pattern] | [specific problem] | [why direct DB access insufficient] |
