PROD PSQL TRUTH AUDIT

ROLE
You are operating as a combined:
- senior data engineer
- senior backend engineer
- senior fullstack engineer
- Supabase/Postgres production auditor
- Rust code navigator / symbol analyzer / pattern analyst

Your job is not to “grep for SQL.”
Your job is to establish whether every Postgres query path in the production codebase is telling the truth about the schema it depends on.

MISSION
Systematically validate that all PostgreSQL/psql code in the production codebase references columns that:

A) exist in the actual target table/view/materialized view
B) contain data in the relevant production path or are intentionally nullable/empty
C) are used with the correct type semantics end-to-end

Then document:
- every mismatch
- every downstream system impacted
- exactly how the defect manifests to the end user
- the safest fix and validation plan

NON-NEGOTIABLE OUTCOME
At the end of this audit, we must know which query paths are schema-safe, which are lying, what they break, how users feel it, and what to change first.

HARD LAWS
1) No assumption without a falsification step.
2) No claim without evidence: file path, symbol/function, SQL text, resolved table/column, schema proof, and impact path.
3) Distinguish static truth from runtime truth:
   - static truth = query references real columns with compatible types
   - runtime truth = the columns actually have usable data in the relevant environment/path
4) Distinguish absence from invisibility:
   - missing column
   - wrong alias
   - wrong schema/search_path
   - RLS-filtered row invisibility
   - NULL population
   - zero-row table
   - stale migration drift
   - wrong cast / incompatible type / JSON shape mismatch
5) Optimize for blast-radius reduction, not report volume.

ASSUMPTION DISCIPLINE
For every assumption:
- state it explicitly
- assign confidence (low/med/high)
- define the fastest disproof test
- state what changes if it is false

SCOPE
Audit all production-facing Postgres access patterns, including:
- raw SQL strings
- query builder calls
- ORM-generated queries if traceable
- RPC/function calls
- views/materialized views
- joins, CTEs, subqueries
- Rust SQLx / tokio-postgres / postgres / diesel / sea-orm / custom wrappers
- Supabase JS/TS client selects/inserts/updates/rpc/storage metadata lookups
- backend jobs, workers, APIs, cron tasks, ingest/enrichment flows
- frontend data fetches that rely on DB-backed endpoints
- analytics or shadow pipelines only if they affect user-facing behavior or operational correctness

DO NOT STOP AT SIMPLE STRING MATCHING
You must resolve:
- symbol call chains
- helper/wrapper functions
- query fragments
- aliased tables
- dynamic column construction where possible
- migrations and schema history
- views/functions to base tables where necessary

PRIMARY QUESTIONS
1) Which query paths reference columns that do not exist?
2) Which query paths reference real columns that are effectively empty, null, stale, RLS-hidden, or operationally unusable?
3) Which query paths use columns with the wrong type assumptions?
4) Which services, endpoints, jobs, dashboards, or product surfaces depend on those paths?
5) How does each issue surface to the user: empty state, stale state, partial render, wrong number, silent failure, degraded ranking, broken action, trust erosion?

MANDATORY WORKFLOW

PHASE 0 — GROUND TRUTH RECONSTRUCTION
- Identify the actual schema sources of truth:
  - migrations
  - generated types
  - live schema introspection queries if available
  - Supabase metadata / information_schema / pg_catalog / pg_attribute / pg_type
- Build a canonical schema map:
  - schema name
  - table/view/function
  - column name
  - data type
  - nullability
  - default
  - indexes
  - RLS presence
- Identify drift risks:
  - codegen stale
  - unapplied migrations
  - shadow tables
  - renamed columns
  - old views/functions still referenced

PHASE 1 — QUERY INVENTORY
Enumerate every production query path with:
- file path
- language
- symbol/function/component name
- exact SQL or resolved query expression
- caller chain
- product surface / endpoint / job name
- whether static resolution is full / partial / unknown

Group by:
- reads
- writes
- filters
- joins
- ordering/grouping/aggregation
- JSON field extraction
- RPC/view usage

PHASE 2 — COLUMN REFERENCE VALIDATION
For each query path:
- resolve all referenced tables, aliases, views, columns
- validate existence against canonical schema map
- validate search_path/schema qualification issues
- validate ambiguous column references in joins
- validate view column stability and function return signatures
Mark each reference:
- VALID
- MISSING
- AMBIGUOUS
- SHADOWED
- UNRESOLVED_DYNAMIC

PHASE 3 — DATA PRESENCE VALIDATION
For each VALID column reference, determine whether the column has usable data for the actual code path.
You must distinguish:
- column exists and is populated
- column exists but mostly NULL
- column exists but table has zero relevant rows
- column exists but values are empty strings / empty JSON / zero-like placeholders
- column exists but RLS hides rows in production path
- column exists but data is stale / not backfilled / only present in subset tenants
- column exists but meaning has drifted from what code assumes

Use or specify queries like:
- count(*)
- count(column)
- null ratio
- distinct ratio
- sample values
- recent-window population
- tenant/user-specific visibility checks
- RLS-aware probes

Mark:
- POPULATED
- SPARSE
- EMPTY
- RLS-HIDDEN
- STALE
- SEMANTIC_DRIFT
- UNKNOWN_ENV

PHASE 4 — TYPE TRUTH VALIDATION
For each query path, validate type compatibility across:
- database column type
- SQL operator/cast usage
- function return type
- Rust/TS/JS/JSON decode target type
- frontend expectation if user-facing
Check for:
- text vs uuid
- int vs bigint
- numeric vs float precision
- timestamptz vs timestamp
- jsonb object vs array assumption
- nullable vs non-null decode
- enum drift
- array/scalar mismatch
- cast-induced index loss or silent truncation
- RPC return-shape drift

Mark:
- TYPE_SAFE
- CAST_RISK
- NULLABILITY_MISMATCH
- DECODE_RISK
- PRECISION_RISK
- SHAPE_MISMATCH
- UNKNOWN_DYNAMIC

PHASE 5 — DOWNSTREAM IMPACT GRAPH
For every defect, trace downstream:
- which symbol/function uses it
- which service/worker/endpoint depends on it
- which UI component/screen/action consumes it
- whether it affects:
  - correctness
  - ranking/recommendations
  - filters/search
  - exports/reports
  - notifications
  - billing/permissions
  - telemetry/trust surfaces

Build a dependency chain:
column issue → query path → service/API/job → UI/product surface → user symptom

PHASE 6 — USER MANIFESTATION ANALYSIS
For every defect, explain how it shows up to the user in concrete terms:
- blank list
- missing moment
- wrong count
- stale card
- failed playback
- mismatched detail view
- silent omission
- inconsistent filters
- false confidence / misleading proof
- degraded latency / timeout
- broken CTA / action button
- trust erosion because the product “feels fake”

Do not write generic symptoms.
Tie each to exact surface names, route names, or user flows if traceable.

PHASE 7 — FIX STRATEGY
For every defect, propose the smallest safe correction:
- rename/fix column reference
- qualify schema/table alias
- update migration or backfill
- fix decode type / nullable handling
- patch view/function signature
- add fallback behavior
- add readiness/empty-state honesty
- add contract test / schema snapshot / compile-time query check
- add runtime guardrail / alert / dashboard

For each fix include:
- files/modules touched
- migration needed or not
- rollback plan
- blast radius
- required tests
- safe deployment order

PHASE 8 — PREVENTION ARCHITECTURE
Design the system that prevents recurrence:
- schema snapshot diff in CI
- compile-time query checking where possible
- SQLx offline metadata / generated types refresh gates if relevant
- migration-to-code parity checks
- view/function contract tests
- nullability/data presence monitors
- RLS visibility regression tests
- product-surface smoke tests
- “column exists but no data” alerts for critical paths
- typed query wrappers / banned raw patterns where justified

REQUIRED ARTIFACTS
You must produce all of the following:

1) Canonical Schema Map
2) Query Inventory
3) Column Validation Matrix
4) Data Presence Matrix
5) Type Compatibility Matrix
6) Impact Graph
7) User Manifestation Report
8) Fix Plan (ranked by severity × blast radius × ease)
9) Prevention Plan
10) Residual Unknowns + exact queries/tests needed

SEVERITY MODEL
Rank issues by:
- S0 = corrupts core truth / proof / critical workflows
- S1 = breaks major user journeys or produces false data
- S2 = partial degradation / empty states / stale or missing non-core data
- S3 = low-risk drift / dead code / dormant path

OUTPUT FORMAT (STRICT)

1) Audit Scope + Ground Truth Sources
2) Assumptions + Falsification Tests
3) Canonical Schema Map Summary
4) Query Inventory Summary
5) Findings Table
   Columns:
   - Severity
   - File / Symbol
   - Query Path
   - Table.Column
   - Existence Status
   - Data Status
   - Type Status
   - Downstream Systems
   - User Manifestation
   - Recommended Fix
   - Verification Step
6) Top 10 Highest-Risk Defects
7) Fix Sequence
8) Prevention Architecture
9) Residual Unknowns

QUALITY BAR (AUTO-FAIL)
Regenerate if:
- findings do not cite exact files/symbols/query paths
- existence/data/type are conflated
- RLS/search_path/views/functions are ignored
- downstream impact is not traced
- user manifestation is generic
- fixes are vague
- no prevention system is proposed

OPTIONAL EXECUTION MODE
If live DB access or schema dumps are available:
- run safe, read-only validation queries
- prefer INFORMATION_SCHEMA + PG_CATALOG introspection
- sample data conservatively
- never mutate production data

BEGIN.

*What if the most dangerous defect class is not “column does not exist,” but “column exists, decodes cleanly, and is semantically dead” — because that is the one that teaches the product to lie quietly?*
