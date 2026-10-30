# Case study: Generate → Validate → Review

This case study documents **one local browser QA session** of the sanitized public editor. The demonstration board is generated randomly, so metrics vary between sessions. The values below are observations, **not guaranteed results, published targets, or validated player-experience findings**.

## Objective

Evaluate whether the tool can generate a densely packed, direction-constrained puzzle with a valid reference path, then separate **technical solvability** from **gameplay quality**.

## Environment and workflow

- Browser: headless Chromium, desktop viewport 1780 × 1050.
- Delivery: single-file HTML application with no server requirements.
- Start: load the built-in public demo, inspect and export its JSON.
- Inspect: switch to **质量**, select the local-zone overlay, then examine **Dependency Graph**.
- Generate: set 34 basic units, 4 auto-exit units, 2 large units, and the **lenient** quality gate.
- Validate: check generation result, then click **验证当前关** for an independent UI validation.
- Check browser errors: no page JavaScript exceptions occurred in this run.

## Step 1 — Initial public demo

| Indicator | Observed |
| --- | ---: |
| Board | 12 × 18 |
| Units | 71 |
| Occupancy | 66% |
| Initially free exits | 13 |
| Dependency depth | 8 |
| Mechanic density | 8% |
| Detected explicit deadlocks | 0 |
| Guaranteed reference path | PASS |
| Greedy Solver | PASS |
| Play Quality | 80 |
| Production Quality | 77 |
| Production Gate | **REJECT** |

The board meets the prototype's reference-path and greedy Solver checks, but its Production Gate is not satisfied. This is intentional: **a playable candidate is not automatically a publishable level**.

### More detailed quality observations

- Local solution zones: 6
- Ineffective-action estimate: 49%
- Key breakthroughs: 4
- Midgame release peak: 34% through the reference solution
- Tail-action share: 24%
- Mechanic participation: 67%
- Longest low-yield sequence: 23

These are internal heuristic indicators; their design value depends on calibration with real playtests.

## Step 2 — Generate an alternative

The editor was configured with:

- Basic units: **34**
- Auto-exit units: **4**
- Large units: **2**
- Quality gate: **lenient**

A generated candidate was returned as a **solvable draft** rather than discarded.

| Indicator | Observed |
| --- | ---: |
| Units | 40 |
| Occupancy | 38% |
| Initially free exits | 7 |
| Dependency depth | 11 |
| Mechanic density | 14% |
| Explicit deadlocks | 0 |
| Guaranteed reference path | PASS |
| Greedy Solver | PASS |
| Play Quality | 62 |
| Production Quality displayed immediately after generation | 70 |
| Gate | **REJECT** |

The generator's status listed rejection reasons: **ineffective actions, midgame peak timing, long low-yield sequences, and Play Quality**.

## Step 3 — Independent validation

Clicking **验证当前关** produced:

| Check | Result |
| --- | --- |
| Structural validation | PASS |
| Greedy Solver | PASS |
| Production Gate | REJECT |
| Production Quality, independently recomputed | 64 |
| Play Quality | 62 |
| Local solution zones | 4 |
| Ineffective-action estimate | 60% |
| Key breakthroughs | 2 |
| Midgame release peak | 0% |
| Tail-action share | 22% |
| Mechanic participation | 67% |
| Reported rejection reasons | Ineffective actions; midgame peak; long low-yield sequences; Play Quality |

**Important caveat:** the post-generation score and the subsequent validation score differ. This is a known scoring-consistency limitation of the prototype and should be corrected before treating the quality score as a reliable production KPI. Solver PASS and Quality Gate REJECT agree across both observations.

## What this demonstrates

1. **Authoring and inspection:** direction-based units and mechanics can be inspected through a board view and dependency graph.
2. **Constraint-aware generation:** the prototype can retain a reference-path candidate and produce a 40-unit example.
3. **Separation of gates:** Solver PASS confirms the prototype found a playable path, while the Production Gate can still reject pacing and low-value interactions.
4. **Actionable diagnosis:** the tool reports specific weaknesses instead of a single undifferentiated PASS/FAIL score.

## Known limitations and next engineering priorities

- Reconcile quality scores between generator preview and validation.
- Improve low-yield sequencing and midgame release peak placement in candidate generation.
- Benchmark 65–80-unit generation over repeatable seeds and several hardware tiers.
- Compare automated Quality scores against human playtest ratings rather than assuming they predict fun.
- Distinguish greedy-search success from exhaustive solvability guarantees.

## Reproduce the review

1. Open `index.html` in a desktop browser.
2. Explore the initial `Demo Level`.
3. Switch to **质量** and select the **局部解区** visualization.
4. Switch to **Graph View** to inspect dependency links.
5. Open **生成**; enter 34 / 4 / 2 units and select **宽松**.
6. Click **Graph-first 生成当前关**. A candidate that is solvable but below the quality threshold should be labeled a **草稿**.
7. Click **验证当前关**, compare the two status summaries, and record the observed quality rejection reasons.

No project-specific source level files or proprietary design documents are needed.
