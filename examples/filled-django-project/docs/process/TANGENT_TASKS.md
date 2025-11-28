# ShopFlow Tangent Tasks

Tangents discovered during feature development. Each includes a breadcrumb back to where we were when it was discovered.

## Active Tangents

### T-015: N+1 Query in Product List View
**Discovered During**: Feature 5 (Inventory Tracking)
**Breadcrumb**: Was adding inventory counts to product list when noticed N+1 on category lookups
**Priority**: Medium
**Impact**: Performance - each product triggers separate category query

**Problem:**
```python
# apps/products/selectors.py - line 24
def get_products_for_category(category_id: int) -> QuerySet[Product]:
    return Product.objects.filter(category_id=category_id)
    # Missing: .select_related('category').prefetch_related('images')
```

**Solution:**
Add `select_related` and `prefetch_related` to product querysets.

**Notes:**
- Affects: `ProductListView`, `CategoryDetailView`, API endpoints
- Test with Django Debug Toolbar to verify fix

---

### T-018: Missing Index on orders.status
**Discovered During**: Feature 6 (Order Status Emails)
**Breadcrumb**: Was querying pending orders for email batch when noticed slow query
**Priority**: Medium
**Impact**: Performance - status filtering does full table scan

**Problem:**
Order filtering by status is common (admin dashboard, email batches) but no index exists.

**Solution:**
```python
# Migration needed
class Migration(migrations.Migration):
    operations = [
        migrations.AddIndex(
            model_name='order',
            index=models.Index(fields=['status'], name='order_status_idx'),
        ),
    ]
```

**Notes:**
- Also consider composite index on (status, created_at) for date-filtered queries

---

### T-012: Cart Expiration Not Implemented
**Discovered During**: Feature 4 (Cart Persistence)
**Breadcrumb**: Finished guest cart persistence, realized carts never expire
**Priority**: Low
**Impact**: Data - stale carts accumulate in database

**Problem:**
Guest carts are created with session keys but never cleaned up when sessions expire.

**Solution Options:**
1. Celery periodic task to delete old carts
2. Database trigger / scheduled job
3. Lazy cleanup on cart access

**Notes:**
- Consider: 30-day expiration for guest carts, never for logged-in users
- Need to handle cart→order conversion (don't delete if order pending)
- Low priority - not user-facing, just data hygiene

---

## Resolved Tangents

### T-011: Decimal Precision for Prices ✅
**Discovered During**: Feature 3 (Shopping Cart)
**Resolved**: Feature 5 (Inventory Tracking)
**Resolution**: Standardized on `DecimalField(max_digits=10, decimal_places=2)`

---

### T-008: Email Template Duplication ✅
**Discovered During**: Feature 6 (Order Status Emails)
**Resolved**: Same feature
**Resolution**: Created `templates/emails/base.html` for shared layout

---

### T-005: Inconsistent Error Response Format ✅
**Discovered During**: Feature 2 (Product Catalog)
**Resolved**: Feature 4 (Cart Persistence)
**Resolution**: Created `apps/core/exceptions.py` with standard error handler

---

## Tangent Categories

| Category | Count | Priority Focus |
|----------|-------|----------------|
| Performance | 2 | T-015, T-018 (address before Phase 3) |
| Data Hygiene | 1 | T-012 (low priority) |
| Code Quality | 0 | - |
| Security | 0 | - |

## When to Address Tangents

- **Between features**: Good time to knock out medium-priority tangents
- **Performance issues**: Address before they compound
- **Security issues**: Address immediately (none currently)
- **Low priority**: Batch together when convenient

## Notes

- T-015 should be addressed after Feature 7, before Feature 8
- T-018 can be combined with any migration work
- T-012 can wait until Phase 3 or later
