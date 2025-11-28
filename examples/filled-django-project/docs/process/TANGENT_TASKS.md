# ShopFlow Tangent Tasks

Tangents discovered during feature development. Each includes a breadcrumb back to where we were when it was discovered.

## ID Convention

Tangents use `TAN-XXX` format (simple increment): `TAN-001`, `TAN-002`, `TAN-003`

When a tangent is converted to a feature, mark it as "Converted to FEAT-X.Y" in the resolution.

---

## Current Tangents

### TAN-015: N+1 Query in Product List View
**Origin Feature**: FEAT-5.0 (Inventory Tracking)
**Discovered**: 2024-01-08
**Breadcrumb**: Was adding inventory counts to product list when noticed N+1 on category lookups
**Priority**: Medium
**Status**: Discovered

**Description**:
Each product triggers a separate category query when rendering the product list.

**Context**:
```python
# apps/products/selectors.py - line 24
def get_products_for_category(category_id: int) -> QuerySet[Product]:
    return Product.objects.filter(category_id=category_id)
    # Missing: .select_related('category').prefetch_related('images')
```

**Suggested Action**:
Add `select_related` and `prefetch_related` to product querysets.

**Affected Areas**:
- `ProductListView`
- `CategoryDetailView`
- API endpoints

**Notes**:
- Test with Django Debug Toolbar to verify fix
- Should be addressed before FEAT-8.0 (more list views)

---

### TAN-018: Missing Index on orders.status
**Origin Feature**: FEAT-6.0 (Order Status Emails)
**Discovered**: 2024-01-12
**Breadcrumb**: Was querying pending orders for email batch when noticed slow query
**Priority**: Medium
**Status**: Discovered

**Description**:
Order filtering by status does full table scan. Status filtering is common (admin dashboard, email batches).

**Context**:
Query plan showed sequential scan on orders table when filtering by status.

**Suggested Action**:
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

**Notes**:
- Also consider composite index on (status, created_at) for date-filtered queries
- Can be combined with any upcoming migration

---

### TAN-012: Cart Expiration Not Implemented
**Origin Feature**: FEAT-4.0 (Cart Persistence)
**Discovered**: 2024-01-03
**Breadcrumb**: Finished guest cart persistence, realized carts never expire
**Priority**: Low
**Status**: Discovered

**Description**:
Guest carts are created with session keys but never cleaned up when sessions expire. Will accumulate stale data over time.

**Context**:
- Carts table will grow indefinitely
- No impact on users, just data hygiene

**Suggested Action Options**:
1. Celery periodic task to delete old carts (preferred)
2. Database scheduled job
3. Lazy cleanup on cart access

**Notes**:
- Consider 30-day expiration for guest carts
- Don't delete if cart has pending order
- Low priority - not user-facing

---

## Completed Tangents

### TAN-011: Decimal Precision for Prices ✅
**Origin Feature**: FEAT-3.0 (Shopping Cart)
**Resolved**: 2024-01-08 (during FEAT-5.0)
**Resolution**: Fixed as part of inventory tracking work

**Original Issue**:
Inconsistent decimal precision for price fields across models.

**How Resolved**:
Standardized on `DecimalField(max_digits=10, decimal_places=2)` across all price/money fields.

---

### TAN-008: Email Template Duplication ✅
**Origin Feature**: FEAT-6.0 (Order Status Emails)
**Resolved**: 2024-01-12 (same feature)
**Resolution**: Fixed during feature implementation

**Original Issue**:
Each email template had duplicated header/footer HTML.

**How Resolved**:
Created `templates/emails/base.html` with shared layout. All email templates now extend base.

---

### TAN-005: Inconsistent Error Response Format ✅
**Origin Feature**: FEAT-2.0 (Product Catalog)
**Resolved**: 2024-01-03 (during FEAT-4.0)
**Resolution**: Converted to standard fix

**Original Issue**:
API endpoints returned errors in different formats (some with `error` key, some with `detail`).

**How Resolved**:
Created `apps/core/exceptions.py` with custom exception handler. All API errors now use consistent format with `error`, `code`, and optional `details` fields.

---

## Deferred Tangents

*No deferred tangents.*

---

## Summary

| Category | Count | IDs |
|----------|-------|-----|
| Performance | 2 | TAN-015, TAN-018 |
| Data Hygiene | 1 | TAN-012 |

**Recommended order**:
1. TAN-015 (N+1 queries) - Address after FEAT-7.0, before FEAT-8.0
2. TAN-018 (index) - Can be done with any migration
3. TAN-012 (cart cleanup) - Low priority, Phase 3+
