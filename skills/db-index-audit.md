---
id: db-index-audit
name: DB Index Audit
description: Find missing and unused indexes before they page you
triggers: [query, index, slow, database, audit]
---
# DB Index Audit

1. **Read the queries, not the schema.** Collect every query shape in the
   codebase (ORM query methods + raw SQL) before touching indexes.
2. **EXPLAIN the top 5.** Enough structure: look for sequential scans on
   filtered columns and nested-loop joins over unsorted inputs.
3. **Write-amp budget.** Every index taxes every insert; on hot tables
   prefer one composite index over three single-column ones.
4. **Prove the win.** Compare `EXPLAIN ANALYZE` timings before/after and
   record them in the PR; drop indexes the planner stopped using.
