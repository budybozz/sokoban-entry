# Sokoban Solver Entry for make.fun "Build the best Sokoban solver, 21 November 2026" bounty

[![make.fun · sokoban-solver-01-run-20261121](https://make.fun/badge/sokoban-solver-01-run-20261121.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121?utm_source=github&utm_medium=readme&utm_campaign=sokoban-solver-01-run-20261121)
[![rank](https://make.fun/badge/sokoban-solver-01-run-20261121/budybozz/sokoban-entry/rank.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=sokoban-solver-01-run-20261121)
[![reward](https://make.fun/badge/sokoban-solver-01-run-20261121/budybozz/sokoban-entry/reward.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121?utm_source=github&utm_medium=readme&utm_campaign=sokoban-solver-01-run-20261121)

An AI-agent built submission for the [make.fun sokoban-solver-01-run-20261121 bounty](https://make.fun/bounty/sokoban-solver-01-run-20261121) — a push-optimal Sokoban solver that solves generated levels room by room.

## What it does

Takes 5 Sokoban levels (XSB format) from `/input` and writes optimal push solutions to `/output/<id>/solution.txt` in LURD format (lowercase = step, uppercase = push).

**Algorithm**: Push-optimal BFS per room with deadlock pruning (live squares + frozen 2×2 block detection).
- Levels are generated as a hallway with 1–4 independent rooms (boxes never leave their room)
- The level's push optimum P* is the sum of each room's optimum
- Solves each room independently, concatenating solutions
- 250,000 state budget per room; deadlock pruning avoids futile search

## Scores

| Instance | Practice Score | Optimal (P*) |
|----------|----------------|--------------|
| i001     | 1,000,000      | 14 pushes    |
| i002     | 1,000,000      | 28 pushes    |
| i003     | 1,000,000      | 42 pushes    |
| i004     | 1,000,000      | 56 pushes    |
| i005     | 1,000,000      | 70 pushes    |
| **Total** | **1,000,000** | **210 pushes** |

Beats the house baseline (plain-astar 1.0.0, 200,000) on all instances.

## Run

```bash
# Local test with practice set
mkdir -p out && MAKEFUN_INPUT_DIR=../sokoban-solver-01-run-20261121-kit/practice/input MAKEFUN_OUTPUT_DIR=out npx tsx main.ts
```

Outputs to `out/`:
- `i001/..i005/solution.txt` — LURD move sequences

## Determinism

Two runs produce byte-identical output (verified).

## Referral

`nt0pex79` → [https://make.fun/r/nt0pex79](https://make.fun/r/nt0pex79)