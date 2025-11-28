# Tangent Tasks

<!--
  TEMPLATE INSTRUCTIONS (delete this block when customizing):

  This file captures work discovered while doing other work.

  The key insight: During feature development, you'll discover issues,
  improvements, and ideas that aren't part of the current scope. Without
  a place to capture these, you either:
  - Chase every tangent (never finish anything)
  - Forget them (lose valuable insights)

  This file solves that by capturing tangents with breadcrumbs back to
  where they were discovered.

  IMPORTANT: The AI won't know it's going off on a tangent. YOU must
  recognize this and tell it to document here instead of pursuing.
-->

## What Is a Tangent?

A tangent is work that:
- Was discovered while working on something else
- Is NOT part of the current feature scope
- Is worth remembering but shouldn't derail current work

**Examples:**
- Found a bug while implementing a feature (not related to the feature)
- Noticed inconsistent patterns that should be standardized
- Had an idea for a future improvement
- Discovered technical debt that should be addressed

---

## Current Tangents

<!--
  Active tangents that haven't been addressed or converted to features.
  Include enough context to pick them up later.
-->

*No active tangents.*

<!-- Example tangent entry:

### Error Handling Inconsistency
**Origin Feature**: Feature 3 - API Endpoints
**Discovered**: [Date]
**Priority**: Medium
**Status**: Discovered

**Description**:
While implementing the /users endpoint, noticed that error handling is
inconsistent across the codebase. Some functions return error codes,
others throw exceptions, and some return null.

**Context**:
- `api/users.js` uses exceptions
- `api/auth.js` returns error codes
- `lib/database.js` returns null on failure

**Suggested Action**:
Standardize on exceptions with a custom error hierarchy. Would need to:
- Define error classes
- Update existing handlers
- Add error middleware

**Breadcrumb**: Return to Feature 3 - API Endpoints after documenting.

-->

---

## Format for New Tangents

When documenting a new tangent, include:

```markdown
### [Descriptive Title]
**Origin Feature**: [Feature that was being worked on when this was discovered]
**Discovered**: [Date]
**Priority**: [High/Medium/Low]
**Status**: [Discovered/Planned/In Progress/Completed/Deferred]

**Description**:
[What the issue/opportunity is]

**Context**:
[Relevant details, files, examples]

**Suggested Action**:
[What should be done about this]

**Breadcrumb**: [Reminder of what to return to after documenting]
```

---

## Completed Tangents

<!--
  Tangents that have been addressed, either as standalone fixes or
  converted to features. Keep for historical context.
-->

*No completed tangents.*

<!-- Example completed tangent:

### Database Connection Pooling ✅
**Origin Feature**: Feature 2 - Core API
**Resolved**: [Date]
**Resolution**: Converted to Feature 2.5 and implemented

**Original Issue**:
Database connections were being created per-request, causing performance
issues under load.

**How Resolved**:
Created Feature 2.5 (Database Connection Pooling), implemented pooling
with configurable limits. Merged in commit `def5678`.

-->

---

## Deferred Tangents

<!--
  Tangents that were evaluated and intentionally deferred.
  Document WHY they were deferred so you don't re-evaluate later.
-->

*No deferred tangents.*

<!-- Example deferred tangent:

### TypeScript Migration
**Origin Feature**: Feature 1 - Project Setup
**Deferred**: [Date]
**Reason**: Project scope doesn't justify migration cost

**Original Idea**:
Consider migrating from JavaScript to TypeScript for better type safety.

**Why Deferred**:
- Project is small enough that JS is manageable
- Team doesn't have TypeScript experience
- Would delay MVP by estimated 2 weeks
- Can revisit if project grows significantly

-->

---

## Guidelines

### When to Create a Tangent Entry

- You discover something outside current feature scope
- You have an idea that would derail current work
- You find technical debt worth remembering
- The AI starts going off-track (tell it to document and refocus)

### When to Convert Tangent to Feature

- The tangent is large enough to need its own branch
- Multiple tangents cluster around the same theme
- The tangent becomes blocking for other work

### When to Defer a Tangent

- It's a "nice to have" that doesn't justify the effort now
- Dependencies aren't in place yet
- Higher priority work exists

### The Breadcrumb Pattern

Always note what you were working on when the tangent was discovered.
This helps you (and the AI) return to the main work after documenting.

Example: "Breadcrumb: Return to Feature 3 - API Endpoints, specifically
the /users endpoint validation logic."
