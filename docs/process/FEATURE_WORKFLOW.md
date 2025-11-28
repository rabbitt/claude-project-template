# Feature Development Workflow

This document defines the 9-step process for implementing features with AI assistance.

## The 9-Step Process

### Step 1: Propose 10K Foot View

Before any implementation, present a high-level overview:

- **Scope**: What will this feature do?
- **Files Affected**: Which files will be created/modified?
- **Dependencies**: What must exist before this can be built?
- **Breaking Changes**: Will this break existing functionality?
- **Estimated Effort**: Rough size (small/medium/large)

**Wait for user approval before proceeding.**

### Step 2: Create Feature Branch

```bash
git checkout -b feature/[feature-name]
```

Naming convention: `feature/[descriptive-name]`
- `feature/user-authentication`
- `feature/api-rate-limiting`
- `feature/database-migrations`

### Step 3: Implement Changes

- Follow the approved plan from Step 1
- Use conventional commit messages (see below)
- Track progress (update status in FEATURE_PLAN.md if needed)
- **If you discover tangents**: Document in TANGENT_TASKS.md, don't pursue

### Step 4: Commit Changes

Use [Conventional Commits](https://www.conventionalcommits.org/) format:

| Prefix | Use For |
|--------|---------|
| `feat:` | New features |
| `fix:` | Bug fixes |
| `refactor:` | Code restructuring (no behavior change) |
| `docs:` | Documentation only |
| `test:` | Test additions/changes |
| `chore:` | Build, tooling, maintenance |

Examples:
```
feat(auth): add user registration endpoint
fix(api): handle null response from external service
refactor(db): extract connection pooling to separate module
docs(readme): add API usage examples
test(auth): add integration tests for login flow
```

### Step 5: Iterate

Repeat Steps 3-4 as needed:
- Continue implementation
- Keep commits focused and atomic
- Update progress tracking

### Step 6: Squash Commits

Before requesting review, collapse all feature commits into one clean commit:

```bash
# Option A: Soft reset (recommended)
git reset --soft main
git commit -m "feat(scope): comprehensive description of feature"

# Option B: Interactive rebase
git rebase -i main
# Mark all commits except first as "squash"
```

The final commit message should:
- Summarize what the feature does
- Be understandable without reading the code
- Follow conventional commit format

### Step 7: Request Review

**CRITICAL: Never merge without review.**

Provide a summary that includes:
- What was implemented
- Key decisions made during implementation
- Any deviations from the original plan
- Testing performed
- Known limitations or future work

Wait for explicit approval, questions, or change requests.

### Step 8: Handle Review Feedback

| Feedback Type | Action |
|---------------|--------|
| Questions | Answer, then return to Step 8 |
| Change Requests | Go back to Step 3, implement changes |
| Approval | Proceed to Step 9 |

### Step 9: Merge and Complete

1. **Update documentation**:
   - Mark feature complete in `FEATURE_PLAN.md`
   - Update `TANGENT_TASKS.md` if any tangents were addressed
   - Update `CLAUDE.md` current status section

2. **Merge to main**:
   ```bash
   git checkout main
   git merge feature/[feature-name]
   ```

3. **Clean up**:
   ```bash
   git branch -d feature/[feature-name]
   git push origin --delete feature/[feature-name]  # if pushed to remote
   ```

4. **Prepare for next feature**:
   - Review `FEATURE_PLAN.md` for next priority
   - Check `TANGENT_TASKS.md` for any urgent tangents

---

## Key Rules

| Rule | Rationale |
|------|-----------|
| **Never merge without explicit approval** | Maintains human control over codebase |
| **Always squash before review** | Clean history, easier to review |
| **Always provide detailed review summary** | Reviewer needs context |
| **Follow conventional commits** | Consistent, parseable history |
| **Document tangents, don't pursue them** | Maintains focus on current feature |

---

## When to Skip This Process

For trivial changes, the full 9-step process is overkill:

**Skip for:**
- Typo fixes
- Single-line changes
- Documentation-only updates
- Changes that take < 5 minutes

**Use full process for:**
- Any new functionality
- Changes touching multiple files
- Architectural changes
- Anything that needs review

---

## Quick Reference

```
1. Plan      → Propose 10K foot view, wait for approval
2. Branch    → git checkout -b feature/[name]
3. Build     → Implement according to plan
4. Commit    → Use conventional commit format
5. Iterate   → Repeat 3-4 as needed
6. Squash    → Collapse to single commit
7. Review    → Request review with summary
8. Feedback  → Address questions/changes
9. Merge     → Update docs, merge, clean up
```
