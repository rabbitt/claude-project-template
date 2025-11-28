# ShopFlow Architecture Decisions

## Decision Log

### ADR-006: Category Tree Structure
**Date**: 2023-11-28
**Status**: Accepted

**Context**:
Products need hierarchical categories (Electronics > Phones > Smartphones). Need efficient queries for ancestors, descendants, and tree rendering.

**Decision**:
Use django-mptt for category tree structure.

**Alternatives Considered**:
- **Adjacency list**: Simple parent_id foreign key. Rejected because inefficient for tree queries (multiple joins for ancestors/descendants).
- **django-treebeard**: Similar to MPTT with different algorithms. Rejected because less popular, smaller community.
- **Closure table**: Stores all ancestor-descendant pairs. Rejected because complex writes and more storage overhead.

**Consequences**:
- Efficient `get_ancestors()`, `get_descendants()` methods
- Template tags for rendering trees
- MPTT fields add complexity to migrations
- Tree must be rebuilt if corrupted
- Write operations slightly slower (tree rebalancing)

---

### ADR-005: Service Layer Pattern
**Date**: 2023-11-20
**Status**: Accepted

**Context**:
Need clear separation between views and business logic. Views were becoming bloated with business rules.

**Decision**:
Implement service layer pattern with `services.py` (writes) and `selectors.py` (reads) in each app.

**Alternatives Considered**:
- **Fat models**: Put logic in model methods. Rejected because models become bloated and hard to test.
- **Fat views**: Keep logic in views. Rejected because untestable, logic gets duplicated across views.
- **Domain-driven design**: Full DDD with aggregates, repositories. Rejected because overkill for current project scale.

**Consequences**:
- Clear separation of concerns
- Services are easy to test in isolation
- Reusable across views, management commands, Celery tasks
- Selectors optimize query patterns in one place
- More files per app (overhead for simple CRUD)
- Team needs to follow the pattern consistently

---

### ADR-004: Authentication System
**Date**: 2023-11-20
**Status**: Accepted

**Context**:
Need user registration, login, OAuth providers, email verification, and password reset flows.

**Decision**:
Use django-allauth for authentication.

**Alternatives Considered**:
- **Custom implementation**: Build from scratch. Rejected because reinventing the wheel, security risk.
- **django-rest-auth**: DRF-focused auth. Rejected because less maintained, API-only focus.
- **dj-rest-auth**: Fork of django-rest-auth. Rejected because same API-only limitations.

**Consequences**:
- Handles OAuth providers (Google, GitHub, etc.) out of the box
- Email verification and password reset built-in
- Well-maintained with large community
- Works with both templates and API
- Additional dependency to manage
- Must customize templates for our design

---

### ADR-003: Frontend Approach
**Date**: 2023-11-20
**Status**: Accepted

**Context**:
Need interactive frontend without SPA complexity. Team has Django experience but limited frontend framework experience.

**Decision**:
Use HTMX + Alpine.js with Django templates (server-rendered with progressive enhancement).

**Alternatives Considered**:
- **React SPA**: Full client-side interactivity. Rejected because adds build complexity, requires API-first architecture, team learning curve.
- **Vue.js SPA**: Similar to React. Rejected because same concerns about complexity and learning curve.
- **Hotwire/Turbo**: Rails-originated approach. Rejected because less Django-native than HTMX, smaller Django community.

**Consequences**:
- Progressive enhancement - works without JavaScript
- No build step required for frontend
- Server-rendered HTML = better SEO
- Django templates stay the source of truth
- Minimal JavaScript knowledge required
- Fast development velocity
- Less suitable for highly interactive features
- Some complex interactions may need custom JavaScript

---

### ADR-002: Background Task Queue
**Date**: 2023-11-25
**Status**: Accepted

**Context**:
Need async processing for emails, payment callbacks, inventory updates. Requests shouldn't block on slow operations.

**Decision**:
Use Celery with Redis as the message broker.

**Alternatives Considered**:
- **Django-Q**: Simpler setup, Django-native. Rejected because less mature ecosystem, fewer monitoring tools.
- **Dramatiq**: Modern, type-hinted API. Rejected because smaller community, less Django integration documentation.
- **RQ (Redis Queue)**: Simple Redis-based queue. Rejected because fewer features (no scheduled tasks, limited monitoring).

**Consequences**:
- Battle-tested at scale
- Excellent Django integration
- Celery Beat for scheduled tasks
- Large ecosystem of monitoring tools (Flower)
- Redis dependency (but we use it for caching anyway)
- More complex deployment (worker processes)
- Need to handle task failures and retries

---

### ADR-001: Payment Provider Selection
**Date**: 2024-01-10
**Status**: Accepted

**Context**:
Need to integrate payment processing for checkout. Must handle credit cards, support webhooks for async events, be PCI compliant.

**Decision**:
Use Stripe as the payment provider.

**Alternatives Considered**:
- **PayPal**: Wider consumer recognition. Rejected because worse developer experience, unreliable webhooks, complex integration.
- **Square**: Good for in-person payments. Rejected because less mature for online-only, limited international support.
- **Braintree**: PayPal-owned, similar features. Rejected because same webhook reliability concerns as PayPal.

**Consequences**:
- Best-in-class documentation and developer experience
- Reliable webhook delivery with built-in retry logic
- Strong support for subscriptions if we add them later
- Global coverage for international expansion
- Stripe Elements for PCI-compliant frontend
- Stripe fees (~2.9% + $0.30 per transaction)
- Must implement webhook signature verification
- Need to handle idempotency for retries

---

## Pending Decisions

### Session Storage (FEAT-8.0+)
Currently using database-backed sessions. May need Redis sessions for multi-server deployment. Decision deferred until scaling requirements are clearer.

---

## Index by Category

### Infrastructure
- [ADR-002: Background Task Queue](#adr-002-background-task-queue)

### Data Model
- [ADR-006: Category Tree Structure](#adr-006-category-tree-structure)

### API Design
- [ADR-005: Service Layer Pattern](#adr-005-service-layer-pattern)

### Frontend
- [ADR-003: Frontend Approach](#adr-003-frontend-approach)

### Authentication
- [ADR-004: Authentication System](#adr-004-authentication-system)

### Payments
- [ADR-001: Payment Provider Selection](#adr-001-payment-provider-selection)
