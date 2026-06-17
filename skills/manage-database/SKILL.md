---
name: manage-database
description: 'Database operations, ORM integration, troubleshooting, and performance optimization. Use when: setting up databases, choosing ORM frameworks (SQLAlchemy, Prisma, Sequelize), diagnosing database issues, optimizing queries and indexes, and monitoring performance.'
argument-hint: 'Specify the task: setup, ORM choice, diagnosis, optimization, or performance tuning'
---

# Database Management

## When to Use

- **Setup & Migration**: Creating databases, designing schemas, applying migrations
- **ORM/Framework Selection**: Choosing between SQLAlchemy, Prisma, Sequelize, TypeORM, etc.
- **Troubleshooting**: Diagnosing connection issues, N+1 queries, deadlocks, constraint violations
- **Performance**: Query optimization, indexing strategies, query analysis
- **Monitoring**: Health checks, slow query logs, connection pool management

## Quick Checklist

### Database Setup
- [ ] Choose database system (PostgreSQL, MySQL, MongoDB, SQLite)
- [ ] Configure connection string with env vars
- [ ] Set up user permissions and role restrictions
- [ ] Enable backups and replication if needed
- [ ] Create initial schema with DDL or migration tool

### ORM Selection
- [ ] **SQLAlchemy** (Python): Mature, flexible, supports many databases
- [ ] **Prisma** (Node.js/TypeScript): Type-safe, schema-first, good DX
- [ ] **Sequelize** (Node.js): Simple ORM, eager/lazy loading control
- [ ] **TypeORM** (TypeScript): Decorator-based, flexible, dataloader patterns
- [ ] **Django ORM** (Python): Opinionated, tight framework integration

### Connection Best Practices
- [ ] Use connection pooling (configure min/max pool size)
- [ ] Set connection timeout and idle timeout
- [ ] Enable SSL/TLS for remote databases
- [ ] Implement exponential backoff for retries
- [ ] Monitor active connections and pool exhaustion

### Query Optimization
- [ ] Identify slow queries via slow query logs
- [ ] Check execution plan (`EXPLAIN ANALYZE`)
- [ ] Add indexes on frequently filtered/joined columns
- [ ] Avoid SELECT * — only fetch needed columns
- [ ] Use eager loading or batch loading to prevent N+1 queries
- [ ] Consider query caching (Redis, Memcached) for read-heavy data

### Schema Design
- [ ] Use appropriate data types (VARCHAR length, DECIMAL precision)
- [ ] Add primary keys and foreign keys with constraints
- [ ] Denormalize cautiously for read performance
- [ ] Use enum types for fixed-value columns
- [ ] Plan for partitioning or sharding early

### Common Issues & Fixes

| Issue | Cause | Solution |
|-------|-------|----------|
| Connection timeouts | Pool exhausted, network issues | Increase pool size, check network, reduce query time |
| Slow queries | Missing indexes, full table scans | `EXPLAIN`, add indexes, optimize queries |
| N+1 queries | Loading related data in loops | Use eager loading, JOINs, or batch loading |
| Deadlocks | Conflicting transaction locks | Lock order, shorter transactions, avoid hot rows |
| Constraint violations | Foreign key, unique, not null | Check data integrity, migrations |
| Memory spikes | Large result sets | Paginate, use cursors, streaming |

### Monitoring Checklist
- [ ] Set up slow query log (threshold: 1s for production)
- [ ] Monitor connection pool utilization
- [ ] Track query execution times with APM (DataDog, New Relic)
- [ ] Alert on replication lag (if applicable)
- [ ] Review index bloat and maintenance needs

### Migration Workflow
- [ ] Use migration tool (Alembic, Flyway, Liquibase)
- [ ] Write reversible migrations
- [ ] Test migrations on staging database first
- [ ] Back up production before running migrations
- [ ] Monitor performance after schema changes