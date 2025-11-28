# ShopFlow Feature Plan

## ID Conventions

**Features** use `FEAT-X.Y` format with optional letter suffix for sub-features:
- `FEAT-1.0`, `FEAT-2.0`, `FEAT-3.0` for main features
- `FEAT-1.5` for insertions (e.g., tangent converted to feature between 1.0 and 2.0)
- `FEAT-2.0A`, `FEAT-2.0B` for sub-features

**Tangents** use `TAN-XXX` format (simple increment):
- `TAN-001`, `TAN-002`, `TAN-003`
- When converted to a feature, mark as "Converted to FEAT-X.Y"

## Commit Conventions

```
feat:     New feature or functionality
fix:      Bug fix
refactor: Code restructuring without behavior change
docs:     Documentation changes
test:     Test additions or modifications
chore:    Build, config, dependency updates
```

---

## Completed Features

### FEAT-1.0: User Registration & Authentication ✅
**Branch**: `feature/user-auth` (merged)
**Commit**: `a1b2c3d`
**Completed**: 2023-11-20
**Summary**: User registration, login, OAuth providers via django-allauth

---

### FEAT-2.0: Product Catalog & Categories ✅
**Branch**: `feature/product-catalog` (merged)
**Commit**: `e4f5g6h`
**Completed**: 2023-11-28
**Summary**: Product models, category tree with django-mptt, admin interface

---

### FEAT-3.0: Basic Shopping Cart ✅
**Branch**: `feature/shopping-cart` (merged)
**Commit**: `i7j8k9l`
**Completed**: 2023-12-10
**Summary**: Cart model, add/remove items, quantity updates, cart display

---

### FEAT-4.0: Cart Persistence ✅
**Branch**: `feature/cart-persistence` (merged)
**Commit**: `m0n1o2p`
**Completed**: 2024-01-03
**Summary**: Guest cart via sessions, cart merging on login

---

### FEAT-5.0: Inventory Tracking ✅
**Branch**: `feature/inventory` (merged)
**Commit**: `q3r4s5t`
**Completed**: 2024-01-08
**Summary**: Stock quantities, optimistic locking, low stock alerts

---

### FEAT-6.0: Order Status Emails ✅
**Branch**: `feature/order-emails` (merged)
**Commit**: `u6v7w8x`
**Completed**: 2024-01-12
**Summary**: Email templates, Celery tasks for async sending, base template

---

## Current Feature

### FEAT-7.0: Stripe Payment Integration
**Branch**: `feature/stripe-payments`
**Status**: 🔄 In Progress (80%)
**Priority**: High
**Dependencies**: FEAT-4.0 (cart), FEAT-5.0 (inventory)

**Scope**:
- Payment Intent creation and handling
- Webhook endpoint with signature verification
- Frontend checkout with Stripe Elements
- Refund handling
- Receipt emails

**Progress**:
- [x] Stripe API configuration
- [x] Payment Intent creation endpoint
- [x] Webhook signature verification
- [x] Success/failure event handling
- [ ] Frontend Stripe Elements integration
- [ ] Refund webhook handling
- [ ] Receipt email trigger
- [ ] Integration tests

---

## Planned Features

### FEAT-8.0: Order History & Reordering
**Priority**: High
**Dependencies**: FEAT-7.0
**Estimated Effort**: Medium

**Scope**:
- Order history page for customers
- Order detail view
- "Reorder" functionality (add previous order items to cart)

---

### FEAT-9.0: Product Reviews & Ratings
**Priority**: Medium
**Dependencies**: FEAT-1.0, FEAT-2.0
**Estimated Effort**: Medium

**Scope**:
- Review submission form
- Star ratings
- Review moderation in admin
- Average rating display on products

---

### FEAT-10.0: Wishlist Functionality
**Priority**: Medium
**Dependencies**: FEAT-1.0, FEAT-2.0
**Estimated Effort**: Small

**Scope**:
- Add to wishlist button
- Wishlist page
- Move to cart functionality

---

### FEAT-11.0: Discount Codes & Promotions
**Priority**: Medium
**Dependencies**: FEAT-7.0
**Estimated Effort**: Large

**Scope**:
- Discount code model
- Code validation at checkout
- Percentage and fixed discounts
- Usage limits and expiration

---

### FEAT-12.0: Search with Filters
**Priority**: Low
**Dependencies**: FEAT-2.0
**Estimated Effort**: Medium

**Scope**:
- Full-text search
- Category filtering
- Price range filtering
- Sort options

---

## Feature Ideas (Backlog)

- **FEAT-13.0**: Sales Dashboard - Admin analytics and reporting
- **FEAT-14.0**: Bulk Product Import - CSV/Excel import for products
- **FEAT-15.0**: Shipping Integration - Carrier API integration

---

## Blocked Items

None currently.
