# Deployment Plan — Zero-Cost Strict

## 1. Initial deployment target
Static frontend hosting only. Cloudflare Pages Free is a candidate because the application can be delivered as static assets. Verify current account requirements, terms, and limits before creating an account or project.

Official limits reference: https://developers.cloudflare.com/pages/platform/limits/

## 2. Explicitly excluded until verified
- Render hosted API: excluded from strict baseline. Its free web services have usage limits and documentation describes possible supplementary bandwidth billing; do not rely on it for a no-charge guarantee.
- Supabase: excluded from baseline until signup requirements and no-card eligibility are verified for the user's account and region.
- Paid domains, paid object storage, paid databases, paid compute, and paid GPU: prohibited.

## 3. No-billing deployment checklist
Before any provider signup or deployment:
1. Confirm signup can complete without entering a payment method.
2. Confirm the selected product is explicitly on the free plan.
3. Confirm there is no automatic trial or paid upgrade.
4. Confirm usage beyond quota is blocked rather than billed.
5. Disable optional paid add-ons and usage-based products.
6. Record current limits and official documentation date.
7. If any item cannot be confirmed, do not use that provider.

## 4. Static deployment flow
1. Build the frontend as static files.
2. Run local tests and production build.
3. Review bundle size and asset sizes.
4. Deploy only after account eligibility and free-plan terms are verified.
5. Test HTTPS, browser compatibility, and offline/local fallback behavior.

## 5. Backend strategy
The first release uses browser-side inference and IndexedDB. A hosted FastAPI backend is not a prerequisite. A future backend can be run locally for development or added to a provider only after the strict no-card and no-billing checklist passes.

## 6. Availability disclaimer
Free services can change terms, suspend inactive projects, or impose quotas. The project must remain usable locally if its static hosting or optional services become unavailable.
