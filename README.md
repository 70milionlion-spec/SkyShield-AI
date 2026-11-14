# SkyShield AI — Phase 02 Planning Package

**Architecture:** v3.1 — Zero-Cost Strict  
**Status:** Phase 02 documentation baseline  
**Budget ceiling:** USD 0.00  
**Payment card:** prohibited  
**Paid trials / automatic upgrades:** prohibited

## Scope of this package
This package contains the architecture and interface specifications for Phase 02. It does not create accounts, cloud resources, repositories, databases, or deployments. It does not install packages or execute application code.

## Important architecture decision
The first public version is **static-cloud + browser-first**:
- React + TypeScript + Three.js are delivered as static assets through a free static hosting tier, subject to current provider eligibility and limits.
- Simulation state, game rules, and the initial ML inference path run in the browser.
- IndexedDB is the primary persistence mechanism for local sessions and settings.
- Kaggle is an optional free-quota training environment; trained model artifacts are exported and versioned.
- A hosted Python/FastAPI service and hosted PostgreSQL are **deferred** until a provider is verified to support signup and operation without a payment method and without any billable overage path.

This avoids making the zero-cost promise depend on a sleeping/limited API host or a database provider whose no-card signup has not been verified.

## Documents
- `docs/architecture.md` — system architecture and component responsibilities
- `docs/api-contracts.md` — browser module interfaces and future optional API contract
- `docs/data-model.md` — local data model and ER diagram
- `docs/deployment.md` — static deployment and no-billing controls
- `docs/project-structure.md` — repository layout
- `docs/quality-and-testing.md` — test strategy and acceptance criteria
- `docs/decision-log.md` — architecture decisions and deferred items

## Phase 02 acceptance status
Documentation baseline prepared. Actual provider signup, account configuration, repository creation, environment setup, and deployment remain separate actions and are not claimed as completed.
