# Quality and Testing Strategy

## 1. Testing layers
- Unit tests: simulation rules, feature mapping, schema validation, scoring.
- Component tests: controls, dashboards, status indicators.
- Integration tests: simulation-to-AI adapter and IndexedDB persistence.
- Model tests: schema compatibility, class mapping, confidence sanity checks.
- Reproducibility tests: fixed seed produces repeatable scenario state.
- Browser tests: rendering, resizing, input handling, fallback behavior.
- Performance tests: frame rate and inference latency measured on named devices.

## 2. ML evaluation
For multiclass classification:
- Accuracy
- Per-class Precision and Recall
- Macro F1 (primary comparison metric where class imbalance exists)
- Confusion Matrix
- Inference latency (P50 and P95)
- Model size

For tracking research, evaluate the tracking module separately using suitable sequence-based metrics only if a genuine annotated sequence benchmark is used.

## 3. Leakage prevention
- Split by `scenario_id` or generation batch, not random rows.
- Keep all frames/events from one scenario in one split.
- Fit preprocessing only on training data.
- Keep test data untouched until final evaluation.
- Record dataset and split versions.

## 4. Acceptance criteria
- No invalid schema values pass validation.
- Fixed seeds reproduce scenario generation within defined deterministic boundaries.
- Session export/import round-trips without loss of required fields.
- AI output always references a model version.
- Model metrics are generated from held-out data.
- No performance claim is published without measured output.
- Core gameplay remains available when optional cloud services are unavailable.

## 5. Reporting
Each experiment records: experiment ID, date, code revision, dataset version, split version, model parameters, metrics, runtime environment, and notes.
