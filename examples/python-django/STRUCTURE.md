# Django Project Structure

## Standard Layout

We follow [Django's recommended project layout](https://docs.djangoproject.com/en/stable/intro/tutorial01/) with apps in an `apps/` directory.

```
myproject/
├── apps/                   # Django applications (one per domain)
│   ├── users/
│   ├── orders/
│   └── core/               # Shared utilities
├── config/                 # Project configuration
│   ├── settings/           # Environment-specific settings
│   ├── urls.py
│   └── celery.py
├── templates/              # Global templates
├── static/                 # Global static files
├── manage.py
└── pyproject.toml
```

## App Structure

Each app follows Django conventions plus service layer:

```
apps/orders/
├── models.py           # Database models
├── views.py            # Views or ViewSets
├── urls.py             # URL routing
├── serializers.py      # DRF serializers (if API)
├── services.py         # Business logic (writes)
├── selectors.py        # Query logic (reads)
├── admin.py            # Admin configuration
├── tasks.py            # Celery tasks
└── tests/              # Test directory
```

## Where Code Goes

| Type | Location |
|------|----------|
| Database model | `apps/<app>/models.py` |
| Business logic | `apps/<app>/services.py` |
| Complex queries | `apps/<app>/selectors.py` |
| API endpoint | `apps/<app>/views.py` |
| Background job | `apps/<app>/tasks.py` |
| Shared utilities | `apps/core/` |

## Project-Specific Notes

<!--
Document ONLY:
- Deviations from standard Django layout
- Custom directories unique to this project
- Special patterns for this codebase
-->

[Add your project-specific structure notes here]

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial structure | Project setup |
