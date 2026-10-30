# Puzzle Level Production Workbench

A **sanitized, browser-based level design portfolio project** for dense, direction-constrained grid puzzles. It demonstrates a workflow from level construction through validation, dependency analysis, and production-quality review.

> **Prototype status:** this is a design-tool demonstration, not a production runtime. Solver success does **not** imply the level passes the gameplay quality gate.

## Try it

- [Open the editor source](index.html) or save `index.html` and open it in a desktop browser.
- [GitHub Pages preview](https://junchowabc.github.io/puzzle-level-production-workbench/) (requires GitHub Pages to be enabled in repository settings).
- [Example: generated level and quality review](docs/generation-validation-case-study.md).

## Features

| Workflow | Capabilities |
| --- | --- |
| Level authoring | 2D board editing, unit directions, obstacles, JSON import/export |
| Generation | Graph-first constraints, guaranteed reference path, difficulty and cascade profiles |
| Mechanic modeling | Breakable blockers, dormant/paired units, push devices, key/lock and portal relationships |
| Validation | Reference-path check, greedy Solver, deadlock checks, SHIFT analysis |
| Quality review | Production Gate, ineffective actions, breakthroughs, tail pacing, mechanic participation |
| Visualization | Board View, draggable dependency graph, local-zone heatmap, quality overlays |
| Batch planning | Candidate pool, similarity review, difficulty curve planning |

## Screenshots

Screenshots are captured from the **public demo** and correspond to generic, non-production data. Image assets are included with the downloadable portfolio package; the repository contains the runnable single-file editor and written case study.

## Tested example (one randomized local run)

| Metric | Observed value |
| --- | ---: |
| Board | 12 × 18 |
| Units | 71 |
| Occupancy | 66% |
| Guaranteed path | PASS |
| Greedy Solver | PASS |
| Play Quality | 80 / 100 |
| Production Quality | 77 / 100 |
| Production Gate | **REJECT** |
| Primary rejection reasons | Ineffective actions and long low-yield sequences |

These are **observations from one run, not guaranteed targets**. Results may vary with randomized generation. See the case study for the generated draft and the separate validation run.

## How to run

1. Open `index.html` in a current desktop browser. No build step is required.
2. Inspect the built-in generated demo or import your own JSON levels.
3. Use **生成** to adjust board size, unit count, mechanisms, and the quality gate.
4. Click **Graph-first 生成当前关**. If a valid candidate fails the Production Gate, it remains available as a clearly labeled **solvable draft**, not a production-ready level.
5. Inspect **质量**, **依赖**, **分析**, and **Board / Graph View**.
6. Export your own JSON. Imported data remains local to your browser session.

## Scope and limitations

- Heuristic metrics and a greedy Solver are intended for **editor feedback**, not mathematical proof of universal solvability or production-grade fun scoring.
- Production Quality thresholds require calibration with human playtesting and curated reference levels.
- Generating 65–80 units is CPU-intensive and may take time; extremely strict filters can reject all final candidates.
- This public build omits project-specific characters, internal documents, and real project level layouts.
- No private project screenshots, proprietary assets, or internal numerical baselines are included.

## Publishing

To enable GitHub Pages: **Settings → Pages → Deploy from a branch → main → / (root)**. The expected site URL is [junchowabc.github.io/puzzle-level-production-workbench](https://junchowabc.github.io/puzzle-level-production-workbench/). Verify deployment status in GitHub Settings → Pages.

## Repository contents

- `index.html` — standalone public editor
- `README.md` — overview and limitations
- `docs/generation-validation-case-study.md` — reproducible test workflow and observed outcomes
- `.gitignore` — local temporary files
