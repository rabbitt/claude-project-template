# Django Project Structure

## Standard Layout

We follow [Django's recommended project layout](https://docs.djangoproject.com/en/stable/intro/tutorial01/) with apps in an `apps/` directory.

```
shopflow/
├── apps/                   # Django applications (one per domain)
│   ├── users/
│   ├── products/
│   ├── cart/
│   ├── orders/
│   ├── payments/
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

### Apps by Domain

- **users**: Customer accounts, authentication, profiles
- **products**: Catalog, categories (django-mptt), inventory
- **cart**: Shopping cart, cart items, guest cart persistence
- **orders**: Order processing, order items, status tracking
- **payments**: Stripe integration, webhooks, refunds
- **core**: Shared models, utilities, permissions

### Service vs Selector Pattern

- `services.py` = write operations + side effects
- `selectors.py` = read operations + complex queries

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| 2024-01-03 | Added payments app | Feature 7 - Stripe integration |
| 2023-11-20 | Initial structure | Project setup |
