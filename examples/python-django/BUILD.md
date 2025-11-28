# Django Build & Run Commands

## Prerequisites

- Python 3.10+
- [uv](https://docs.astral.sh/uv/) (recommended) or pip
- PostgreSQL (production) or SQLite (development)
- Redis (optional, for Celery)

## Quick Reference

```bash
# Setup
uv sync                                    # Install dependencies

# Database
uv run python manage.py migrate            # Run migrations
uv run python manage.py createsuperuser    # Create admin

# Development
uv run python manage.py runserver          # Start dev server (http://localhost:8000)
uv run python manage.py shell_plus         # Django shell

# Testing
uv run pytest                              # Run tests
uv run pytest --cov=apps                   # With coverage

# Quality
uv run ruff check . && ruff format --check . && mypy .
```

## Additional Commands

```bash
# Migrations
uv run python manage.py makemigrations     # Create migrations
uv run python manage.py showmigrations     # Check status

# Data
uv run python manage.py loaddata fixtures/initial_data.json
uv run python manage.py dumpdata users --indent 2 > fixtures/users.json

# Celery (if using)
uv run celery -A config worker -l info     # Start worker

# Production
uv run python manage.py collectstatic      # Collect static files
uv run python manage.py check --deploy     # Security checklist
```

## Common Issues

| Issue | Fix |
|-------|-----|
| `No changes detected` | Ensure app is in `INSTALLED_APPS` and has `migrations/__init__.py` |
| Static files 404 | Run `collectstatic`, configure web server for `STATIC_ROOT` |
| Database connection refused | Check PostgreSQL is running, verify `DATABASE_URL` |

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial build setup | Project setup |
