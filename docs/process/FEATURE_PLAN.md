# Feature Plan

<!--
  TEMPLATE INSTRUCTIONS (delete this block when customizing):

  This file tracks your feature roadmap. Update it as features progress.

  Sections:
  - Completed Features: History with commit references
  - Current Feature: What's being worked on now
  - Planned Features: What's coming next

  NOTE: "Current Status" lives in CLAUDE.md (the index into work).
  This file contains the work details themselves.

  Keep completed features for context - they help the AI understand
  what patterns have been established.
-->

## ID Conventions

**Features** use `FEAT-X.Y` format with optional letter suffix for sub-features:
- `FEAT-1.0`, `FEAT-2.0`, `FEAT-3.0` for main features
- `FEAT-1.5` for insertions (e.g., tangent converted to feature between 1.0 and 2.0)
- `FEAT-2.0A`, `FEAT-2.0B` for sub-features

**Tangents** use `TAN-XXX` format (simple increment):
- `TAN-001`, `TAN-002`, `TAN-003`
- When converted to a feature, mark as "Converted to FEAT-X.Y"

This provides stable references that don't change if items are renamed, with insertion slots for features.

---

## Completed Features

<!--
  Keep completed features documented for context.
  Include commit hash for reference.
-->

*No features completed yet.*

<!-- Example of completed feature:
### FEAT-1.0: Project Setup ✅
**Branch**: `feature/project-setup` (merged)
**Commit**: `abc1234`
**Completed**: [Date]
**Summary**: Initial project structure, build system, basic configuration
-->

---

## Current Feature

### FEAT-1.0: [Feature Name]
**Branch**: `feature/[branch-name]`
**Status**: 🔄 In Progress
**Priority**: High
**Dependencies**: None

**Scope**:
- [What this feature will do]
- [Key functionality included]
- [What's explicitly NOT included]

**Files Affected**:
- `[file-path]` - [What changes]
- `[file-path]` - [What changes]

**Progress**:
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]

**Notes**:
- [Any important context]
- [Decisions made during implementation]

---

## Planned Features

<!--
  List upcoming features in priority order.
  Include enough detail to understand scope without being exhaustive.
-->

### FEAT-2.0: [Feature Name]
**Priority**: [High/Medium/Low]
**Dependencies**: FEAT-1.0
**Estimated Effort**: [Small/Medium/Large]

**Scope**:
- [Brief description of what this will do]

---

### FEAT-3.0: [Feature Name]
**Priority**: [High/Medium/Low]
**Dependencies**: [None or list dependencies]
**Estimated Effort**: [Small/Medium/Large]

**Scope**:
- [Brief description of what this will do]

---

## Feature Ideas (Backlog)

<!--
  Ideas that aren't yet planned but might be implemented later.
  Less detail needed here.
-->

- **[Idea Name]**: [One-line description]
- **[Idea Name]**: [One-line description]

---

## Dependencies Graph

<!--
  Optional: Visual representation of feature dependencies.
  Helps understand what blocks what.
-->

```
FEAT-1.0 (Setup)
    └── FEAT-2.0 (Core)
            ├── FEAT-3.0 (Extension A)
            └── FEAT-4.0 (Extension B)
                    └── FEAT-5.0 (Advanced)
```

---

## Conventions

### Status Icons
- ✅ Completed
- 🔄 In Progress
- ⏸️ Paused
- 📋 Planned
- ❌ Cancelled

### Priority Levels
- **High**: Blocking other work or critical path
- **Medium**: Important but not blocking
- **Low**: Nice to have, do when time permits

### Commit Message Format
Follow [Conventional Commits](https://www.conventionalcommits.org/):
- `feat:` - New features
- `fix:` - Bug fixes
- `refactor:` - Code restructuring
- `docs:` - Documentation
- `test:` - Tests
- `chore:` - Maintenance
