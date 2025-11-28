# Go Build & Run Commands

## Prerequisites

- Go 1.21+
- Optional: golangci-lint, air (live reload)

```bash
# macOS
brew install go golangci-lint

# Ubuntu
sudo snap install go --classic
go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest
```

## Quick Reference

```bash
go build ./...           # Build all
go run ./cmd/myapp       # Run
go test ./...            # Test
go test -cover ./...     # Test with coverage
golangci-lint run        # Lint
```

## Additional Commands

```bash
# Dependencies
go mod tidy              # Clean up go.mod/go.sum
go mod download          # Download dependencies

# Testing
go test -v ./...                    # Verbose
go test -run TestName ./pkg/...     # Specific test
go test -race ./...                 # Race detector

# Building
go build -o bin/myapp ./cmd/myapp                    # Named output
GOOS=linux GOARCH=amd64 go build -o bin/myapp ./cmd/myapp  # Cross-compile

# Development
air                      # Live reload (if installed)
```

## Build System

Go modules (`go.mod`) handle dependencies. Check `Makefile` if present for project-specific targets.

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial build setup | Project setup |
