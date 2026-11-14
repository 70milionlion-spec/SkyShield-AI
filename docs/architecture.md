# System Architecture — SkyShield AI

## 1. Product definition
SkyShield AI is a fictional browser-based 3D simulation game with AI-assisted classification of synthetic game entities, tracking-state management, and game-event prioritization. All entity attributes and interactions are fictional game data. No real-world targeting, guidance, interception, or weapon-performance calculations are in scope.

## 2. Zero-Cost Strict constraints
1. Total permitted spend: USD 0.00.
2. No payment card or payment method may be added.
3. No paid trial, automatic upgrade, paid API, paid domain, paid GPU, or paid storage.
4. Do not enable usage-based billing.
5. Stop using a service before any limit can create a charge.
6. Provider free tiers are conditional and may change; re-check official terms immediately before signup/deployment.
7. If a provider requires a payment method or exposes a billable overage route that cannot be disabled, reject it.

## 3. Architecture pattern
Use a modular browser-first architecture with static cloud delivery. Avoid mandatory always-on backend services in the initial release.

### Runtime components
- Web UI: React + TypeScript.
- 3D presentation: Three.js (React Three Fiber may be adopted if its integration proves useful).
- Simulation core: deterministic, seeded, fictional game-state generator and game rules in TypeScript.
- AI inference: browser-side inference using a validated exported model format, or a lightweight JavaScript-compatible model representation.
- Local persistence: IndexedDB; small preferences may use localStorage.
- Model training: Scikit-learn in a free-quota notebook environment, with CPU fallback where feasible.
- Source control: Git repository.
- Static hosting: Cloudflare Pages Free is a candidate, subject to account/signup and current plan verification.

### Deferred optional components
- Python + FastAPI hosted backend.
- Hosted PostgreSQL (including Supabase).
- Hosted WebSocket service.
These are not required for the first playable release. Reconsider only after no-card signup, quota behavior, and zero-billing guarantees are verified. If backend services are introduced later, keep the browser simulation functional when they are unavailable.

## 4. Data flow
1. User selects a fictional scenario and game settings.
2. Simulation core creates entities and emits synthetic state updates.
3. Feature adapter maps simulation state to the model's documented input schema.
4. Browser inference classifies the synthetic entity/event.
5. Game rules consume the classification and produce a fictional priority label.
6. UI displays entity state, confidence, model version, and decision explanation.
7. Session events and metrics are persisted in IndexedDB.
8. Export/import JSON is provided for backup and reproducibility.

## 5. Separation of responsibilities
- Rendering layer: camera, lighting, meshes, materials, visual effects.
- Simulation layer: seeded game events, time progression, fictional movement, collisions.
- AI adapter: schema validation, feature mapping, model invocation.
- Game decision layer: bounded game-only priority rules.
- Persistence layer: IndexedDB repositories and export/import.
- UI layer: dashboard, controls, radar-style visualization, evaluation views.

The ML model must not directly control rendering or low-level physics. It returns typed predictions; game rules interpret them.

## 6. Determinism and reproducibility
Every scenario run should store:
- `session_id`
- `scenario_id`
- `seed`
- `simulation_version`
- `model_version`
- `created_at`
- `settings_snapshot`

The same seed and simulation version should reproduce the same synthetic scenario where practical.

## 7. Performance strategy
- Keep the render loop independent of model inference.
- Avoid sending every animation frame to any server.
- Use bounded update rates for AI evaluation.
- Use instancing and low-poly assets where appropriate.
- Provide a reduced-quality mode for weaker devices.
- Measure browser frame rate and inference latency; do not publish unmeasured performance claims.

## 8. Security and privacy
- No secrets in frontend bundles.
- No credentials stored in source control.
- Validate imported session files.
- Do not collect personal data unless required and explicitly designed.
- Use HTTPS for hosted assets.
- Treat model files and imported JSON as untrusted input.
