# Architecture Decision Log

## ADR-001 — Zero-Cost Strict
**Decision:** Project spending ceiling is USD 0.00. No payment method, paid trial, paid add-on, automatic upgrade, or usage-based billing is allowed.

## ADR-002 — Browser-first runtime
**Decision:** The initial game runtime and ML inference path should work in the browser where feasible. This reduces reliance on an always-on hosted backend.

## ADR-003 — Static cloud hosting
**Decision:** Use a static hosting free tier as the first public deployment candidate. Cloudflare Pages Free is a candidate, subject to no-card signup and current limits verification.

## ADR-004 — IndexedDB as primary persistence
**Decision:** Use IndexedDB for initial session persistence and JSON export/import. Hosted PostgreSQL is deferred.

## ADR-005 — FastAPI hosting deferred
**Decision:** Do not use Render or another hosted API provider in the baseline until a no-card, no-billing path is verified. Render's documented free service limitations include potential supplementary bandwidth billing.

## ADR-006 — ML training separated from inference
**Decision:** Train models in a free-quota notebook environment or CPU environment; export versioned artifacts for browser inference.

## ADR-007 — Safety boundary
**Decision:** All AI labels, priority logic, motion, and collisions remain fictional gameplay mechanics. No real-world targeting, guidance, interception, or weapon-performance calculations.
