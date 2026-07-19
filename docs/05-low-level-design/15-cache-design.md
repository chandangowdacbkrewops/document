# 14. Cache Design

## Purpose

This chapter defines the Cache Design for the KrewOps Recruitment Platform. Caching improves application performance by reducing database access, minimizing response times, and increasing system scalability. Frequently accessed data is temporarily stored in an in-memory cache to serve repeated requests efficiently.

---

# Objectives

The Cache Design aims to:

- Reduce database load.
- Improve API response time.
- Increase application scalability.
- Reduce latency.
- Improve user experience.
- Optimize frequently accessed data.
- Support distributed deployments.

---

# Cache Architecture

```text
                 Client
                    │
                    ▼
              REST Controller
                    │
                    ▼
               Service Layer
                    │
          Check Cache (Redis)
             │              │
        Cache Hit      Cache Miss
             │              │
             ▼              ▼
      Return Cached     Repository
          Data              │
                             ▼
                        PostgreSQL
                             │
                             ▼
                      Store in Cache
                             │
                             ▼
                        Return Response
```

---

# Cache Components

| Component | Responsibility |
|------------|----------------|
| Application | Reads and writes cache |
| Redis | In-memory distributed cache |
| Repository | Retrieves data from database |
| Database | Persistent storage |

---

# Cache Workflow

```text
Incoming Request
        │
        ▼
Check Redis Cache
        │
   ┌────┴────┐
   │         │
 Hit        Miss
   │         │
   ▼         ▼
Return    Query DB
Cached        │
Data          ▼
          Save to Cache
               │
               ▼
         Return Result
```

---

# Cache Strategy

The platform primarily adopts the **Cache-Aside Pattern**.

Workflow:

1. Check Redis.
2. If present, return cached data.
3. If absent, query PostgreSQL.
4. Store result in Redis.
5. Return response.

This approach keeps the cache synchronized with application reads.

---

# Cached Data

Typical cached objects include:

- User Profile
- Company Details
- Candidate Information
- Job Details
- Roles
- Permissions
- Configuration Data
- Frequently Used Master Data

Frequently changing transactional data is generally not cached.

---

# Cache Key Design

Cache keys should follow a consistent naming convention.

Examples:

```text
user:101

company:25

candidate:420

job:85

role:ADMIN

permission:HR_VIEW

config:application
```

Using descriptive keys simplifies debugging and cache management.

---

# Cache Expiration (TTL)

Every cached entry should have an appropriate Time-To-Live (TTL).

| Data Type | Suggested TTL |
|------------|---------------|
| User Profile | 30 Minutes |
| Company Details | 60 Minutes |
| Job Details | 30 Minutes |
| Roles | 12 Hours |
| Permissions | 12 Hours |
| Configuration | 24 Hours |

TTL values may vary depending on business requirements.

---

# Cache Eviction

Cache entries are invalidated when underlying data changes.

Examples:

```text
Update User
      │
      ▼
Update Database
      │
      ▼
Remove Redis Entry
      │
      ▼
Next Request Reloads Cache
```

This ensures clients receive fresh data.

---

# Cache Patterns

## Cache Aside

```text
Application
     │
     ▼
Redis Cache
     │
     ▼
Database
```

Best suited for read-heavy workloads.

---

## Read Through

```text
Application
      │
      ▼
Cache
      │
      ▼
Database
```

The cache retrieves missing data automatically.

---

## Write Through

```text
Application
      │
      ▼
Cache
      │
      ▼
Database
```

Updates both cache and database simultaneously.

---

## Write Behind

```text
Application
      │
      ▼
Cache
      │
      ▼
Background Sync
      │
      ▼
Database
```

Provides high write performance but introduces eventual consistency.

---

# Distributed Cache

Redis enables distributed caching across multiple application instances.

```text
        Load Balancer
         │        │
         ▼        ▼
 Application   Application
      │            │
      └──────┬─────┘
             ▼
          Redis
             │
             ▼
        PostgreSQL
```

All application instances share the same cache.

---

# Cache Consistency

To maintain consistency:

- Update database first.
- Evict or refresh cache after successful update.
- Avoid stale cache entries.
- Keep cache TTL reasonable.

---

# Cache Failure Handling

If Redis becomes unavailable:

```text
Request
   │
   ▼
Redis Down
   │
   ▼
Query Database
   │
   ▼
Return Response
```

The application should continue functioning without cache availability.

---

# Monitoring

Important cache metrics include:

- Cache Hit Rate
- Cache Miss Rate
- Evictions
- Memory Usage
- Expired Keys
- Response Time
- Connected Clients

Monitoring helps optimize cache performance.

---

# Security

Sensitive information should not be cached unless encrypted.

Guidelines:

- Secure Redis with authentication.
- Enable TLS where applicable.
- Restrict network access.
- Avoid caching passwords or authentication tokens.
- Apply appropriate TTL values.

---

# Best Practices

- Cache frequently accessed data.
- Avoid caching rapidly changing records.
- Use meaningful cache keys.
- Configure sensible TTL values.
- Evict cache after updates.
- Monitor cache hit ratios.
- Design for graceful degradation.
- Prevent cache stampedes using locking or refresh strategies.
- Keep cached objects lightweight.

---

# Benefits

The Cache Design provides:

- Faster API responses.
- Reduced database load.
- Improved scalability.
- Lower latency.
- Better user experience.
- Higher throughput.
- Efficient resource utilization.
- Improved performance under heavy traffic.

---

# Summary

The Cache Design establishes Redis as the distributed caching solution for the KrewOps Recruitment Platform. By implementing the Cache-Aside pattern, standardized cache keys, appropriate expiration policies, cache invalidation strategies, and graceful fallback mechanisms, the platform achieves significant performance improvements while maintaining data consistency, scalability, and high availability.
