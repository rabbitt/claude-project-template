# Go Project Structure

## Standard Layout

We follow [Standard Go Project Layout](https://github.com/golang-standards/project-layout) conventions.

```
myapp/
├── cmd/myapp/              # Application entry point
│   └── main.go
├── internal/               # Private application code
│   ├── config/
│   ├── user/               # Domain packages
│   ├── handler/            # HTTP handlers
│   └── platform/           # Infrastructure (db, cache)
├── pkg/                    # Public library code (optional)
├── go.mod
└── go.sum
```

## Where Code Goes

| Type | Location |
|------|----------|
| Entry points | `cmd/<app>/main.go` |
| Domain logic | `internal/<domain>/` |
| HTTP handlers | `internal/handler/` |
| Infrastructure | `internal/platform/` |
| Public libraries | `pkg/` (if needed) |
| Tests | `*_test.go` alongside code |

## Project-Specific Notes

<!--
Document ONLY:
- Deviations from standard Go layout
- Domain package organization
- External dependencies of note
-->

[Add your project-specific structure notes here]

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial structure | Project setup |
