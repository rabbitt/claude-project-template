# Feature Plan

<!--
  TEMPLATE INSTRUCTIONS (delete this block when customizing):

  This file tracks your feature roadmap. Update it as features progress.

  Sections:
  - Current Status: Quick reference to what's active
  - Completed Features: History with commit references
  - Current Feature: What's being worked on now
  - Planned Features: What's coming next

  Keep completed features for context - they help the AI understand
  what patterns have been established.
-->

## Current Status

- **Active Feature**: Feature 1 - [Feature Name]
- **Branch**: `feature/[branch-name]`
- **Progress**: [Brief status]
- **Next Up**: Feature 2 - [Feature Name]

---

## Completed Features

<!--
  Keep completed features documented for context.
  Include commit hash for reference.
-->

*No features completed yet.*

<!-- Example of completed feature:
### Feature 0: Project Setup ✅
**Branch**: `feature/project-setup` (merged)
**Commit**: `abc1234`
**Completed**: [Date]
**Summary**: Initial project structure, build system, basic configuration
-->

---

## Current Feature

### Feature 1: [Feature Name]
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

### Feature 2: [Feature Name]
**Priority**: [High/Medium/Low]
**Dependencies**: Feature 1
**Estimated Effort**: [Small/Medium/Large]

**Scope**:
- [Brief description of what this will do]

---

### Feature 3: [Feature Name]
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
Feature 1 (Setup)
    └── Feature 2 (Core)
            ├── Feature 3 (Extension A)
            └── Feature 4 (Extension B)
                    └── Feature 5 (Advanced)
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
