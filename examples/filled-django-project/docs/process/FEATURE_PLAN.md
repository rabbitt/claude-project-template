# ShopFlow Feature Plan

## Commit Conventions

```
feat:     New feature or functionality
fix:      Bug fix
refactor: Code restructuring without behavior change
docs:     Documentation changes
test:     Test additions or modifications
chore:    Build, config, dependency updates
```

## Feature Roadmap

### Phase 1: Core E-commerce (Complete)

- [x] **Feature 1**: User Registration & Authentication
  - Status: ✅ Merged (2023-11-20)
  - Branch: `feature/user-auth`
  - Commits: 12

- [x] **Feature 2**: Product Catalog & Categories
  - Status: ✅ Merged (2023-11-28)
  - Branch: `feature/product-catalog`
  - Commits: 18

- [x] **Feature 3**: Basic Shopping Cart
  - Status: ✅ Merged (2023-12-10)
  - Branch: `feature/shopping-cart`
  - Commits: 14

### Phase 2: Order Processing (In Progress)

- [x] **Feature 4**: Cart Persistence (Guest & Logged-in)
  - Status: ✅ Merged (2024-01-03)
  - Branch: `feature/cart-persistence`
  - Commits: 9

- [x] **Feature 5**: Inventory Tracking
  - Status: ✅ Merged (2024-01-08)
  - Branch: `feature/inventory`
  - Commits: 11

- [x] **Feature 6**: Order Status Emails
  - Status: ✅ Merged (2024-01-12)
  - Branch: `feature/order-emails`
  - Commits: 8

- [ ] **Feature 7**: Stripe Payment Integration 🔄 ACTIVE
  - Status: 🔄 In Progress (80%)
  - Branch: `feature/stripe-payments`
  - Started: 2024-01-13
  - What's Done:
    - ✅ Stripe API configuration
    - ✅ Payment Intent creation
    - ✅ Webhook signature verification
    - ✅ Success/failure handling
  - What Remains:
    - ⬜ Frontend Stripe Elements
    - ⬜ Refund handling
    - ⬜ Receipt emails
    - ⬜ Integration tests

- [ ] **Feature 8**: Order History & Reordering
  - Status: 📋 Planned
  - Dependencies: Feature 7 (payments)
  - Estimate: Medium complexity

### Phase 3: Customer Experience (Planned)

- [ ] **Feature 9**: Product Reviews & Ratings
  - Status: 📋 Planned
  - Dependencies: None

- [ ] **Feature 10**: Wishlist Functionality
  - Status: 📋 Planned
  - Dependencies: None

- [ ] **Feature 11**: Discount Codes & Promotions
  - Status: 📋 Planned
  - Dependencies: Feature 7 (payment integration)

- [ ] **Feature 12**: Search with Filters
  - Status: 📋 Planned
  - Dependencies: Feature 2 (product catalog)

### Phase 4: Admin & Operations (Future)

- [ ] **Feature 13**: Sales Dashboard
- [ ] **Feature 14**: Bulk Product Import
- [ ] **Feature 15**: Shipping Integration

## Current Sprint Focus

**Sprint 5 (Jan 8-22, 2024):**
- Primary: Feature 7 - Stripe Payment Integration
- Secondary: Address T-015 (N+1 query fix)

## Architecture Notes

Key decisions made during feature development:

| Feature | Decision | Rationale |
|---------|----------|-----------|
| F1 | django-allauth for auth | Handles OAuth, email verify, password reset |
| F2 | MPTT for categories | Efficient tree queries for nested categories |
| F5 | Optimistic locking | Prevent race conditions in inventory updates |
| F6 | Celery for emails | Don't block request on SMTP |
| F7 | Stripe over PayPal | Better API, webhook reliability |

## Blocked Items

None currently.

## Next Steps After Feature 7

1. Complete Feature 7 integration tests
2. Merge Feature 7 to main
3. Address T-015 (N+1 query performance)
4. Start Feature 8 planning (order history)
