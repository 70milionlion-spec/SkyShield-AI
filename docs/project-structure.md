# Proposed Repository Structure

```text
SkyShield-AI/
├── apps/
│   └── web/
│       ├── public/
│       └── src/
│           ├── app/
│           ├── components/
│           ├── dashboard/
│           ├── simulation/
│           │   ├── scene/
│           │   ├── entities/
│           │   ├── engine/
│           │   └── effects/
│           ├── ai/
│           │   ├── adapters/
│           │   ├── inference/
│           │   └── schemas/
│           ├── persistence/
│           └── services/
├── packages/
│   ├── shared-types/
│   ├── simulation-core/
│   └── game-rules/
├── ml/
│   ├── data/
│   ├── preprocessing/
│   ├── training/
│   ├── evaluation/
│   └── artifacts/
├── docs/
├── tests/
├── .gitignore
├── README.md
└── LICENSE
```

## Module boundaries
- `simulation-core`: deterministic fictional state generation and simulation clock.
- `game-rules`: game-only rules and scoring.
- `shared-types`: shared TypeScript contracts.
- `ai/adapters`: maps game state to the model feature schema.
- `ai/inference`: loads and invokes the exported model.
- `persistence`: IndexedDB repositories and JSON backup/import.
- `ml`: training and evaluation workflows, separated from browser runtime.
