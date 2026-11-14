# Interface Contracts — SkyShield AI

## 1. Initial release: in-browser module contracts
The first release does not require a network API. Modules communicate through typed interfaces.

### SimulationSnapshot
```ts
type SimulationSnapshot = {
  sessionId: string;
  scenarioId: string;
  seed: number;
  simulationTimeMs: number;
  entities: SimEntity[];
};

type SimEntity = {
  entityId: string;
  entityClass: "aircraft_a" | "aircraft_b" | "drone" | "bird" | "unknown";
  visibilityLevel: number;      // normalized 0..1, fictional
  sceneDensity: number;         // normalized 0..1, fictional
  visualConfidence: number;     // normalized 0..1, synthetic game feature
  trackingState: "new" | "tracked" | "lost" | "recovered";
  behaviorCategory: "pattern_a" | "pattern_b" | "pattern_c";
};
```

### AI inference request/response
```ts
type PredictionRequest = {
  entity: SimEntity;
  simulationVersion: string;
};

type PredictionResult = {
  entityId: string;
  predictedClass: string;
  confidence: number;
  modelVersion: string;
  inferenceLatencyMs: number;
};
```

### Game decision
```ts
type GamePriority = "low" | "medium" | "high";

type GameDecision = {
  entityId: string;
  priority: GamePriority;
  reasonCode: string;
  decisionVersion: string;
};
```

All values above are fictional simulation features. Priority is a gameplay label, not a real-world threat assessment.

## 2. Validation rules
- Numeric normalized features must be finite and within 0..1.
- IDs must be non-empty strings with bounded length.
- Enum values must match the declared set.
- Unknown or missing fields must be handled explicitly.
- Invalid samples are rejected and logged locally; do not silently coerce invalid values.

## 3. Future optional REST API
Only if a compliant no-card provider is verified:
- `GET /api/v1/health`
- `GET /api/v1/models`
- `POST /api/v1/session-exports`
- `GET /api/v1/evaluations/{evaluation_id}`

The API is for optional synchronization and analytics, not required for core gameplay.

## 4. Future WebSocket contract
Deferred. If later implemented, use a versioned message envelope:
```json
{
  "schema_version": "1.0",
  "message_type": "simulation_snapshot",
  "session_id": "session-example",
  "sequence": 1,
  "payload": {}
}
```
No high-frequency raw render frames should be transmitted. Only bounded, compact game-state events may be considered.

## 5. Compatibility
Every model artifact must include a metadata file documenting:
- model version
- training dataset version
- feature schema version
- label schema version
- training code revision
- evaluation split identifier
- metrics and limitations
