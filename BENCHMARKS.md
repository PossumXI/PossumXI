# Arobi / Ullumii benchmarks

Every number on this page comes from a dated run, with per-call logs kept as proof. Comparisons use the same tasks for
every subject. Each subject runs under its own published plan. Negative and inconclusive results are listed too.

Q is Arobi's HORIZON-class model. Its underlying foundation model is not disclosed.

---

## 1. Rubik's cube

**Engine:** [rubiks-bench](https://github.com/Fin-Murphy/rubiks-bench) at commit `4841865`, unmodified, run privately.
Every subject plays the same 8 scrambles: depth 3 (seeds 1, 2), depth 5 (seeds 0, 1, 2), depth 8 (seeds 0, 1) and
depth 12 (seed 0). The move budgets are 20, 30, 45 and 60.

### 1a. Ullumii with a solver skill (tool-assisted orchestration), 2026-10-20

Q is offered one skill, `cube.solve`, backed by a classical two-phase solver. On each turn Q decides whether to call
the skill or to submit moves, and the harness plays every move through the unmodified engine. **This measures
orchestration (picking the right tool and acting on its result), not move-by-move reasoning.**

| Game | Result | Moves | Model calls | Wall s | Tokens |
|---|---|---:|---:|---:|---:|
| depth 3, seed 1 | solved | 3 | 2 | 3.4 | 1,959 |
| depth 3, seed 2 | solved | 3 | 2 | 4.0 | 1,951 |
| depth 5, seed 0 | solved | 5 | 2 | 4.3 | 1,919 |
| depth 5, seed 1 | solved | 5 | 2 | 2.7 | 1,920 |
| depth 5, seed 2 | solved | 5 | 2 | 26.8 | 2,064 |
| depth 8, seed 0 | solved | 8 | 2 | 3.4 | 1,985 |
| depth 8, seed 1 | solved | 8 | 2 | 3.8 | 2,043 |
| depth 12, seed 0 | solved | 18 | 3 | 14.0 | 4,417 |

**8 of 8 solved, 0 invalid moves, 0 failed calls.** The 26.8 s game was one slow model answer, not extra calls.

### 1b. Frontier coding agents reasoning move by move, 2026-10-18/19

**Codex CLI** (gpt-6.1-sol, own plan):

| Game | Result | Moves | Wall s | Input tokens (cached) | Output tokens |
|---|---|---:|---:|---:|---:|
| depth 3, seed 1 | solved | 3 | 43.5 | 225,003 (203,264) | 1,174 |
| depth 3, seed 2 | solved | 3 | 32.9 | 181,281 (169,344) | 1,081 |
| depth 5, seed 0 | solved | 5 | 74.8 | 350,819 (337,920) | 2,948 |
| depth 5, seed 1 | solved | 5 | 94.7 | 487,742 (462,336) | 3,649 |
| depth 5, seed 2 | solved | 9 | 97.2 | 543,050 (495,488) | 3,167 |
| depth 8, seed 0 | solved | 8 | 74.7 | 390,868 (354,944) | 3,058 |
| depth 8, seed 1 | solved | 8 | 78.3 | 463,013 (439,680) | 3,250 |
| depth 12, seed 0 | solved | 22 | 101.8 | 917,133 (859,264) | 3,364 |

8 of 8 solved, 0 invalid moves. Plan usage was about 1–2 points of the weekly window per 8-game ladder, roughly
0.13–0.25% per game. Codex reports whole percents only, so treat this as a range.

**Claude Code** (claude-opus-5-5, own plan, capped at 25% of a 5-hour window):

| Game | Result | Moves | Wall s | Output tokens (thinking) |
|---|---|---:|---:|---:|
| depth 3, seed 1 | solved | 3 | 24.8 | 1,379 |
| depth 3, seed 2 | solved | 3 | 35.9 | 2,270 |
| depth 5, seed 0 | solved | 5 | 217.4 | 20,552 (20,040) |
| depth 5, seed 1 | move budget used up | 30 of 30 | 959.4 | 94,552 (92,333) |

3 of 4 solved, 0 invalid moves. The run stopped at its preset plan-usage cap, so games 5–8 were not played and are not
counted.

### 1c. How to read this

These are **different approaches to the same task**. Two frontier agents reason move by move, while Ullumii delegates
the search to a solver skill and acts on the result. On the 8 games where both Ullumii and Codex played, Ullumii used
about 2k tokens per game against Codex's 181k–917k input tokens. On all 8 games, Ullumii also took less wall-clock
time. The method is what differs, and the comparison shows what good tool orchestration buys you. It does not show that
one model out-reasons another.

---

## 2. Visual reasoning (preregistered), 2026-10-17

The hypotheses, pass thresholds and a held-out image set were written down before the first model call. The 60 held-out
images (10 task types, 6 each) were generated beforehand and first used in the final round. The ground truth is exact,
and every answer was scored by fixed rules.

**Result: 51 of 60 correct = 85.0%, 95% interval 73.9–91.9%.**

| Task | Correct |
|---|---|
| Counting shapes of one colour | 6/6 |
| Reading a bar's value | 6/6 |
| Comparing two bars | 6/6 |
| Geometry (angle or area) | 6/6 |
| Adding up a receipt | 6/6 |
| Finding the highest row of a table | 6/6 |
| Locating a symbol in a grid | 6/6 |
| Whether a setting is on or off | 6/6 |
| Reading an analog clock | 3/6 |
| Shortest path through a maze | 0/6 |

- Each answer took a median of 5.2 s (90th percentile 16.6 s) and cost about USD 0.0001.
- **Elimination:** 9 candidate models were screened on 120 separate images. Six common techniques were each tested
  against a preset bar with an exact McNemar test: step-by-step prompting, describe-then-reason, a counting detector,
  majority vote of three, zoomed tiles, and a decision model for multiple-choice questions. **None helped.** Two tools
  for the weakest tasks were also rejected. A clock-pointing tool gained only +7.5 points, below its 10-point bar. A maze
  solver scored 40%, below its 60% bar, and every miss was a timeout. The two finalists landed within each other's
  intervals, and the preregistered tiebreak (lower 90th-percentile time) chose the faster one, which is also about
  seven times cheaper.
- **Limits:** clocks and mazes are not reliable. Photos, scans, handwriting and non-English text were not tested.
  Samples are small (6 per task), so 6/6 means "no misses seen", not "never wrong".

---

## 3. Q response latency, 2026-10-18

The same 150-word question was sent through the public endpoint twice in each mode.

| Mode | First visible word | Whole answer |
|---|---:|---:|
| Buffered | 5.5 s / 3.9 s | 5.5 s / 3.9 s |
| **Streamed** | **1.6 s / 1.0 s** | 5.1 s / 2.9 s |

Earlier the same day, before streaming and the effort tuning, the same question took 17.4 s.

---

## 4. Arobi readiness benchmark (live)

This benchmark is a signed report generated from live production probes, and anyone can rerun it at
[aura-genesis.org/benchmarks/arobi-spine](https://aura-genesis.org/benchmarks/arobi-spine). On 2026-10-29 it scored
**100/100**: 8 probes passed, 0 failed and 0 warned. One probe is deliberately not public, because private
infrastructure stays closed.

- The probes cover the chain head and finality, public ledger visibility, the evidence seal, verifier replay, policy
  gates, gated context, entitlement, and checkout.
- Reported at that time: chain head 1,574,418, 1,630 redacted receipts anyone can inspect, and seal and replay checks
  in about 1.7 s each.
- The score measures how ready the proof paths are. It does **not** claim that we outperform frontier models.

---

## What we don't claim

- **Q reasoning move by move on the cube.** Q made no solve in this mode. The reasoning lane ran out of output tokens
  while thinking, and the public path times out silent requests at about 100 s. No solve rate is claimed.
- **Large-context work.** Research is ongoing, and no context-size claim will be made until its measured rounds pass.
- **Certification.** No benchmark here is a safety certification or an independent third-party certification.

© Arobi Technology Alliance, Inc. Results are published for information. The underlying harnesses and source code are proprietary.
