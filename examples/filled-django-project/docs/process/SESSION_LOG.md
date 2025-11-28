# ShopFlow Session Work Log

## Recent Sessions

### 2024-01-15 - Stripe Webhook Implementation
**Feature**: FEAT-7.0 - Stripe Payment Integration
**Branch**: `feature/stripe-payments`

**Accomplished**:
- Implemented webhook endpoint with signature verification
- Added handling for `payment_intent.succeeded` and `payment_intent.payment_failed`
- Created Celery task for async payment processing
- Updated Order model to track payment status

**Discovered**:
- TAN-018: Missing index on orders.status (slow queries when filtering)

**Decisions Made**:
- Use Celery for webhook processing to return 200 quickly to Stripe
- Store Stripe payment_intent_id on Order for reconciliation

**Next Steps**:
- Implement frontend Stripe Elements integration
- Add refund webhook handling

---

### 2024-01-13 - Payment Intent Creation
**Feature**: FEAT-7.0 - Stripe Payment Integration
**Branch**: `feature/stripe-payments`

**Accomplished**:
- Set up Stripe API configuration with environment variables
- Created PaymentService in apps/payments/services.py
- Implemented Payment Intent creation endpoint
- Added basic error handling for Stripe API errors

**Discovered**:
- Need to handle idempotency keys for retry safety

**Decisions Made**:
- Store Stripe keys in environment variables (not settings.py)
- Use PaymentIntent API (not Charges) for SCA compliance

**Next Steps**:
- Implement webhook endpoint for async events
- Add signature verification

---

### 2024-01-12 - Order Status Emails Complete
**Feature**: FEAT-6.0 - Order Status Emails
**Branch**: `feature/order-emails` (merged)

**Accomplished**:
- Created email templates for order confirmation, shipped, delivered
- Implemented Celery tasks for async email sending
- Added email preferences to User model
- Created base email template for consistent styling (resolved TAN-008)

**Discovered**:
- TAN-015: N+1 query in product list (noticed while testing order confirmation)

**Decisions Made**:
- Use Celery for all email sending (don't block requests)
- HTML emails with plain text fallback

**Next Steps**:
- Start FEAT-7.0: Stripe Payment Integration

---

### 2024-01-08 - Inventory Tracking Complete
**Feature**: FEAT-5.0 - Inventory Tracking
**Branch**: `feature/inventory` (merged)

**Accomplished**:
- Added stock_quantity field to Product model
- Implemented optimistic locking for inventory updates
- Created inventory adjustment service
- Added low stock alerts
- Fixed TAN-011 (decimal precision) during this work

**Discovered**:
- Potential race condition in concurrent checkouts (solved with optimistic locking)

**Decisions Made**:
- ADR-005: Use optimistic locking instead of database locks
- Track inventory adjustments in separate table for audit trail

**Next Steps**:
- Start FEAT-6.0: Order Status Emails

---

### 2024-01-03 - Cart Persistence Complete
**Feature**: FEAT-4.0 - Cart Persistence
**Branch**: `feature/cart-persistence` (merged)

**Accomplished**:
- Implemented guest cart using session keys
- Cart merging when guest logs in
- Cart serialization for API responses
- Fixed TAN-005 (error response format) during this work

**Discovered**:
- TAN-012: Carts never expire, will accumulate stale data

**Decisions Made**:
- Merge guest cart into user cart on login (don't replace)
- Keep cart items even if product price changes (show warning)

**Next Steps**:
- Start FEAT-5.0: Inventory Tracking

---

## Archived Sessions

*Sessions older than 30 days moved to archives. See git history for full context.*
