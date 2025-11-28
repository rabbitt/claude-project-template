# ShopFlow Architecture Decisions

## ADR-001: Payment Provider Selection

**Date:** 2024-01-10
**Status:** Accepted
**Context:** Need to integrate payment processing for checkout.

**Decision:** Use Stripe as the payment provider.

**Alternatives Considered:**
- **PayPal**: Wider consumer recognition, but worse developer experience and webhook reliability
- **Square**: Good for in-person, less mature for online-only
- **Braintree**: Owned by PayPal, similar issues

**Rationale:**
- Best-in-class documentation and developer experience
- Reliable webhook delivery with built-in retry logic
- Strong support for subscriptions if we add them later
- Global coverage for international expansion
- Stripe Elements for PCI-compliant frontend

**Consequences:**
- Stripe fees (~2.9% + $0.30 per transaction)
- Must implement webhook signature verification
- Need to handle idempotency for retries

---

## ADR-002: Background Task Queue

**Date:** 2023-11-25
**Status:** Accepted
**Context:** Need async processing for emails, payment callbacks, inventory updates.

**Decision:** Use Celery with Redis as the broker.

**Alternatives Considered:**
- **Django-Q**: Simpler, but less mature ecosystem
- **Dramatiq**: Modern, but smaller community
- **RQ (Redis Queue)**: Simpler, but fewer features

**Rationale:**
- Battle-tested at scale
- Excellent Django integration
- Celery Beat for scheduled tasks
- Large ecosystem of monitoring tools (Flower)
- Team familiarity

**Consequences:**
- Redis dependency (but we use it for caching anyway)
- More complex deployment (worker processes)
- Need to handle task failures and retries

---

## ADR-003: Frontend Approach

**Date:** 2023-11-20
**Status:** Accepted
**Context:** Need interactive frontend without SPA complexity.

**Decision:** Use HTMX + Alpine.js with Django templates.

**Alternatives Considered:**
- **React SPA**: Full interactivity, but adds build complexity and API-first architecture
- **Vue.js**: Similar to React concerns
- **Hotwire/Turbo**: Good, but less Django-native than HTMX

**Rationale:**
- Progressive enhancement - works without JS
- No build step required
- Server-rendered = better SEO
- Django templates stay the source of truth
- Minimal JS knowledge required
- Fast development velocity

**Consequences:**
- Less suitable for highly interactive features
- Team needs to learn HTMX patterns
- Some complex interactions may need custom JS

---

## ADR-004: Authentication System

**Date:** 2023-11-20
**Status:** Accepted
**Context:** Need user registration, login, OAuth, password reset.

**Decision:** Use django-allauth.

**Alternatives Considered:**
- **Custom implementation**: Full control, but reinventing the wheel
- **django-rest-auth**: DRF-focused, but less maintained
- **dj-rest-auth**: Fork of above, API-only focus

**Rationale:**
- Handles OAuth providers (Google, GitHub, etc.)
- Email verification built-in
- Password reset flows
- Well-maintained, large community
- Works with both templates and API

**Consequences:**
- Additional dependency
- Must customize templates for our design
- Some complexity in configuration

---

## ADR-005: Service Layer Pattern

**Date:** 2023-11-20
**Status:** Accepted
**Context:** Need clear separation between views and business logic.

**Decision:** Implement service layer pattern with `services.py` and `selectors.py`.

**Alternatives Considered:**
- **Fat models**: Django convention, but models become bloated
- **Fat views**: Quick, but untestable and duplicated logic
- **Domain-driven design**: Overkill for current scale

**Rationale:**
- Clear separation of concerns
- Services are easy to test in isolation
- Reusable across views, management commands, tasks
- Selectors optimize query patterns in one place

**Consequences:**
- More files per app
- Team needs to follow the pattern consistently
- Some overhead for simple CRUD

---

## ADR-006: Category Tree Structure

**Date:** 2023-11-28
**Status:** Accepted
**Context:** Products need hierarchical categories (Electronics > Phones > Smartphones).

**Decision:** Use django-mptt for category tree.

**Alternatives Considered:**
- **Adjacency list**: Simple, but inefficient for tree queries
- **django-treebeard**: Similar to MPTT, less popular
- **Closure table**: Faster reads, complex writes

**Rationale:**
- Efficient ancestor/descendant queries
- Well-documented Django integration
- `get_ancestors()`, `get_descendants()` methods
- Template tags for rendering trees

**Consequences:**
- MPTT fields add complexity to migrations
- Tree must be rebuilt if corrupted
- Write operations slightly slower (tree rebalancing)

---

## Pending Decisions

### Session Storage (Feature 8+)
Currently using database-backed sessions. May need Redis sessions for multi-server deployment. Decision deferred until scaling requirements are clearer.

---

## Change Log

| Date | ADR | Change |
|------|-----|--------|
| 2024-01-10 | ADR-001 | Added payment provider decision |
| 2023-11-28 | ADR-006 | Added category tree decision |
| 2023-11-25 | ADR-002 | Added Celery decision |
| 2023-11-20 | ADR-003,004,005 | Initial architecture decisions |
