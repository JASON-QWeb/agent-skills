# Database Optimization

## Description
Database performance optimization techniques covering indexing, query optimization, and schema design patterns.

## Indexing Strategies
```sql
-- Composite index for common queries
CREATE INDEX idx_orders_user_date ON orders(user_id, created_at DESC);

-- Partial index for active records
CREATE INDEX idx_active_users ON users(email) WHERE active = true;

-- Covering index to avoid table lookups
CREATE INDEX idx_products_search ON products(category, name) INCLUDE (price, stock);
```

## Query Optimization
```sql
-- Use EXPLAIN ANALYZE
EXPLAIN ANALYZE SELECT * FROM orders WHERE user_id = 123;

-- Avoid SELECT *
SELECT id, name, email FROM users WHERE active = true;

-- Use CTEs for readability
WITH recent_orders AS (
  SELECT user_id, COUNT(*) as order_count
  FROM orders
  WHERE created_at > NOW() - INTERVAL '30 days'
  GROUP BY user_id
)
SELECT u.name, ro.order_count
FROM users u
JOIN recent_orders ro ON u.id = ro.user_id;
```

## Connection Pooling
```go
db.SetMaxOpenConns(25)
db.SetMaxIdleConns(5)
db.SetConnMaxLifetime(5 * time.Minute)
```

## Best Practices
1. Index columns used in WHERE, JOIN, ORDER BY
2. Monitor slow query logs
3. Use connection pooling
4. Partition large tables
5. Regular VACUUM/ANALYZE
