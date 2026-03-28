# Trace

> *It looks like news, but behaves like knowledge.*

---

## What is Trace?

Trace is a **claim-and-evidence layer** for high-velocity, contested public information.

The problem it solves: claims are buried inside narrative, evidence is scattered across many sources, and articles stay static while reality keeps moving. Trace extracts the falsifiable claims inside any source — a tweet, article, filing, or thread — structures multi-perspective evidence around each one, and keeps a live "current understanding" that updates as new evidence arrives.

In plain terms:

1. You encounter a source (post, article, report)
2. Trace exposes the claims inside it
3. Each claim becomes **inspectable**, **challengeable**, and **continuously updateable**
4. Over time, those claims accumulate into a reusable knowledge network

**One-line definition:** Trace converts fast-moving public information into auditable, contributable, continuously updated knowledge objects.

---

## Core Architecture

### Backend (Python / Flask)

| Module | Role |
|---|---|
| `app.py` | REST API — claims CRUD, evidence CRUD, signal ingest, auto-find, history |
| `db.py` | SQLite persistence — claims, evidence, challenges, understanding versions, snapshots |
| `signal.py` | Tweet fetch (xfetch), claim extraction, 9-angle web search + 4-angle Twitter search, novelty scoring |
| `ai.py` | Claude API — claim canonicalization, verdict computation, understanding generation |
| `scaffold.py` | Evidential chain scaffold for identity/attribution claims |

### Frontend (React + Vite)

Single-app, four views:

- **Source View** — article + extracted claims, with/without Trace overlay toggle
- **Timeline** — daily watch grouped by date, scanning standards panel
- **Traced Claims** — signal intake form, searchable/filterable claims grid with confidence sparklines
- **Knowledge Graph** — 4-layer force-directed graph (Entity → Event → Claim → Source), pan/zoom/inspect

### Evidence System

Trace classifies evidence into a **7-relation taxonomy** — not just "supports" or "contradicts":

| Relation | Verdict weight | What it means |
|---|---|---|
| `confirms` | +1.0× | Independent source asserts the same fact with its own data |
| `refutes` | −1.0× | Data or reasoning directly opposes the claim |
| `qualifies` | neutral | Claim holds only under unstated conditions |
| `contextualizes` | neutral | Baseline/comparison/history that neither confirms nor denies |
| `reframes` | −0.5× | Accepts the data but attributes a different cause/mechanism |
| `methodology` | −0.3× | Critiques how the claim was established |
| `precedent` | neutral | Prior case with known outcome that informs plausibility |

Quality controls built into the pipeline:

- **3-test contradiction gate** — load-bearing test, escape-hatch test, domain test before assigning `refutes`
- **Novelty scoring** — 21 identical sources contribute roughly the same weight as 3–4 distinct ones; prevents echo-chamber amplification
- **Self-referential filter** — removes the source tweet itself from the evidence pool
- **key_point informativeness filter** — drops evidence whose summary has >60% word overlap with the claim

---

## Development Status

### What's built

| Component | Status |
|---|---|
| 7-relation evidence taxonomy + DB schema | ✅ Complete |
| 9-angle web search + 4-angle Twitter search | ✅ Complete |
| Contradiction quality gate (3-test) | ✅ Complete |
| Novelty scoring + evidence clustering display | ✅ Complete |
| Self-referential evidence filter | ✅ Complete |
| Source View with Trace overlay | ✅ Complete |
| Timeline (daily watch) | ✅ Complete |
| Traced Claims grid + signal intake | ✅ Complete |
| Knowledge Graph (4-layer force-directed) | ✅ Complete |
| Evidential chain scaffold (identity/attribution claims) | ✅ Complete |

### What's next

- Live end-to-end test on fresh claim with full 9-angle search + novelty scoring
- Evidence reward layer (contributor incentives)
- Multi-user challenge windows
- Distribution / partnership integration

---

## Stealth Notice

**This project is currently in active stealth development — local builds only, not yet open to the public.**

The codebase will be made available at a later stage. What you see here is a preview stub.

If you'd like to see the POC in action, have a collaboration inquiry, or want to discuss the evidence graph approach — **reach out directly:**

→ [Open a conversation via GitHub Issues](https://github.com/rainineye/Trace-POC/issues/new) or DM [@rainineye](https://github.com/rainineye)

---

*Last updated: March 2026*
