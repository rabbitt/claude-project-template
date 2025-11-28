# ShopFlow - Development Context

## Project Overview

ShopFlow is a Django-based e-commerce platform for small to medium businesses. It provides a complete solution for product catalog management, shopping cart functionality, order processing, and customer management.

**Tech Stack:**
- Backend: Django 4.2 with Django REST Framework
- Database: PostgreSQL 15
- Cache/Queue: Redis 7 with Celery for background tasks
- Frontend: HTMX + Alpine.js (server-rendered with progressive enhancement)
- Authentication: django-allauth with OAuth2 providers

**Architecture:**
- Service layer pattern (business logic in `services.py`, queries in `selectors.py`)
- Apps organized by domain: `users`, `products`, `cart`, `orders`, `payments`
- Shared utilities in `apps/core/`
- API endpoints follow REST conventions with consistent response formats

**Target Users:**
- Store owners managing products and orders (admin interface)
- Customers browsing and purchasing (storefront)
- Third-party integrations via REST API

## Critical Startup Instructions

**MANDATORY: Read these files at the start of EVERY session:**

1. `docs/process/FEATURE_WORKFLOW.md` - Development process
2. `docs/process/FEATURE_PLAN.md` - Current feature roadmap
3. `docs/process/TANGENT_TASKS.md` - Outstanding tangents

**Reference as needed:**
- `docs/reference/CONVENTIONS.md` - Coding patterns and PEP 8 overrides
- `docs/reference/BUILD.md` - Build, test, run commands
- `docs/reference/STRUCTURE.md` - App and file organization
- `docs/architecture/DECISIONS.md` - ADR log (payment provider, Celery, etc.)

## Critical Rules

### ALWAYS:
- Follow the 9-step feature workflow
- Document tangents instead of pursuing them
- Get explicit approval before merging
- Run `pytest` before committing
- Use type hints for all function signatures
- Put business logic in `services.py`, not views
- Use `selectors.py` for complex queries

### NEVER:
- Merge without user review and approval
- Put business logic in views or serializers
- Skip writing tests for new functionality
- Commit `.env` or secrets to the repository
- Use raw SQL without documenting why ORM won't work
- Break the REST API contract without versioning

### Payment-Specific Rules (Feature 7):
- NEVER log full card numbers or CVVs
- ALWAYS verify webhook signatures before processing
- Use idempotency keys for all Stripe API calls
- Test with Stripe test mode only in development

---

## AI-Managed Below

<!--
  Everything below this line is updated by the AI each session.
  The AI should keep these sections current as work progresses.
-->

---

## Current Status

- **Active Feature**: Feature 7 - Stripe Payment Integration
- **Branch**: `feature/stripe-payments`
- **Progress**: Webhook handling complete, checkout flow 80% done
- **Last Session**: 2024-01-15 - Implemented Stripe webhook signature verification and payment intent creation

### Recent Completions
- Feature 6: Order Status Emails (merged 2024-01-12)
- Feature 5: Inventory Tracking (merged 2024-01-08)
- Feature 4: Shopping Cart Persistence (merged 2024-01-03)

## Current Feature Context (Feature 7)

### What's Done:
- Stripe account configuration and API key management
- Payment Intent creation endpoint (`POST /api/checkout/payment-intent/`)
- Webhook endpoint with signature verification (`POST /api/webhooks/stripe/`)
- Handling for `payment_intent.succeeded` and `payment_intent.payment_failed`
- Order status updates on successful payment

### What Remains:
- Frontend checkout form integration with Stripe Elements
- Handling for refunds (`charge.refunded` webhook)
- Payment receipt email trigger
- Error handling UI for declined cards
- Integration tests for full checkout flow

### Key Files:
- `apps/payments/services.py` - Stripe API interactions
- `apps/payments/views.py` - Checkout and webhook endpoints
- `apps/payments/tasks.py` - Async payment processing
- `apps/orders/services.py` - Order completion logic
- `templates/checkout/payment.html` - Checkout UI

## Known Issues & Technical Debt

1. **Cart expiration** - Carts don't expire, may accumulate stale data
   - Tracked in: TANGENT_TASKS.md (T-012)
   - Priority: Low (address in Phase 3)

2. **N+1 queries in product list** - Need to add `select_related`
   - Tracked in: TANGENT_TASKS.md (T-015)
   - Priority: Medium (performance impact)

3. **Missing index on orders.status** - Slow queries on order filtering
   - Tracked in: TANGENT_TASKS.md (T-018)
   - Priority: Medium (add migration)

## Notes for Next Session

- **Continue Feature 7**: Start with frontend Stripe Elements integration
- **Test file to reference**: `apps/payments/tests/test_checkout.py` has test payment intents
- **Stripe test cards**: Use `4242424242424242` for success, `4000000000000002` for decline
- **Remember**: Webhook endpoint must return 200 quickly, do heavy processing in Celery task
- **TODO**: After Feature 7, revisit T-015 (N+1 queries) before starting Feature 8
