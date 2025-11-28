# Go Coding Conventions

## Style Guide

Go style is **enforced by tooling** - there's no debate.

| Document | Description |
|----------|-------------|
| [Effective Go](https://go.dev/doc/effective_go) | Official style guide |
| [Go Code Review Comments](https://go.dev/wiki/CodeReviewComments) | Common review feedback |

## Tool Configuration

| Tool | Purpose | Notes |
|------|---------|-------|
| `gofmt` | Formatting | **Non-negotiable** - run automatically |
| `go vet` | Static analysis | Built-in, catches common mistakes |
| `golangci-lint` | Extended linting | Config in `.golangci.yml` |

**Check `.golangci.yml`** - it defines which additional linters are enabled.

**Before committing:**
```bash
go fmt ./...
go vet ./...
golangci-lint run
```

## Go Naming (Enforced by Convention)

| Type | Pattern | Example |
|------|---------|---------|
| Packages | `lowercase` | `user`, `httputil` |
| Exported | `PascalCase` | `UserService`, `ProcessRequest()` |
| Unexported | `camelCase` | `userCache`, `validateInput()` |
| Interfaces | `-er` suffix (single method) | `Reader`, `Stringer` |
| Acronyms | All caps | `HTTPClient`, `userID` |

## Project-Specific Conventions

<!--
Document ONLY:
- golangci-lint configuration choices
- Project-specific patterns (repository pattern, etc.)
- Error handling conventions beyond standard
- Logging/metrics patterns

Standard Go conventions don't need documentation - they're enforced.
-->

[Add your project-specific conventions here]

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial conventions | Project setup |
