# WumpusLogic — KB Agent with Resolution Refutation

> **AI 2002 – Artificial Intelligence (Spring 2026) · Assignment 6 · NUCES Faisalabad**

A fully web-based, Vercel-deployable **Knowledge-Based Agent** navigating a dynamic Wumpus World grid using **Propositional Logic** and **Resolution Refutation**.

---

## Links

| Resource | URL |
|---|---|
| Live Demo | *[Paste Vercel URL here after deployment]* |
| GitHub | *[Paste GitHub URL here]* |
| LinkedIn Post | *[Paste LinkedIn URL here]* |

---

## Features

### Environment (spec §1)
- **Dynamic Grid Sizing** — User configures Rows × Columns (3×3 to 10×10)
- **Dynamic Hazards** — Pits and Wumpus randomly placed each episode; agent has no prior knowledge
- **Percept Generation** — Breeze near pits, Stench near Wumpus (4-directional adjacency)

### Inference Engine (spec §2)
- **Propositional Logic KB** — Maintains a clause-set in CNF
- **TELL** — On each visit, biconditional percept rules are converted to CNF clauses and added to the KB
- **Resolution Refutation** — Before labelling a cell safe, engine adds negation of query to KB and saturates resolution. Empty clause (⊥) proves original query
- **Proves**: `NOT P_{r,c} AND NOT W_{r,c}` for each unvisited adjacent cell

### Visualization & Metrics (spec §3)
- Agent (blue glow), Safe (green), Visited (teal), Unknown (dark), Pit/Wumpus (red), Gold (yellow)
- Real-time: inference steps, KB clause count, active percepts, score, move count
- Expandable KB viewer showing live CNF clauses

---

## Architecture

```
src/
├── logic.js      # Propositional Logic KB + Resolution Refutation engine
├── world.js      # Wumpus World: createWorld(), stepAgent(), TELL/ASK loop
├── App.jsx       # React UI: Grid, MetricsDash, LogPanel, KBViewer
├── App.css       # Design system (dark terminal aesthetic)
└── index.css     # CSS variables, animations, global reset
```

---

## Local Development

```bash
npm install
npm run dev   # http://localhost:5173
```

## Deploy to Vercel

```bash
npm run build   # outputs to dist/
```

1. Push to GitHub
2. Import repo at vercel.com
3. Framework: **Vite** (auto-detected)
4. Deploy (vercel.json included)
