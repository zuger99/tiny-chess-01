# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/zuger99/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/zuger99/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An autonomous, high-performance chess engine in Python designed for the make.fun tiny-chess-01 gauntlet.

## Overview

`tiny-chess-01` is a complete standalone chess engine implementing the standard rules of chess, efficient 0x88 board representation, MVV-LVA move ordering, alpha-beta negamax search, and piece-square table positional evaluation. The uncompressed engine source resides in `engine.py` and compresses to under 4KB in `main.py` for submission.

## Features

- **Autonomous Gauntlet Client**: Automatically interacts with HTTP endpoints `/game` and `/move` at `MAKEFUN_ENV_URL`.
- **0x88 Board Representation**: Fast out-of-bounds testing via bitwise operations (`sq & 0x88 == 0`).
- **Complete Chess Rules**: Accurate legal move generation supporting en passant, castling, promotion, and in-check validation.
- **Negamax Alpha-Beta Pruning**: Efficient tree search with depth 3 and MVV-LVA capture ordering.
- **Positional Evaluation**: Material balance combined with 0x88 piece-square tables (PST) flipped for Black.
- **Compact Footprint**: Fully compressible to less than 4KB (`main.py`).

## Architecture and Search Strategy

### 0x88 Board Representation
The board uses a linear array of 128 elements where square coordinates are mapped as `(rank << 4) | file`. Square validity is checked in a single CPU cycle via `sq & 0x88 == 0`. Black squares mirror White positions along the rank axis via `sq ^ 0x70`.

### Legal Move Generation
1. **Pseudo-Legal Generation**: Fast directional offsets generate rays for sliding pieces (bishops, rooks, queens) and single-step jumps for pawns, knights, and kings. Castling rights and path safety are validated against ray attacks.
2. **Check Validation**: Candidate moves are executed on a state history stack, and moves leaving the friendly king in check are pruned.

### Search and Pruning
- **Negamax Framework**: Zero-sum symmetric formulation simplifies the recursive search tree.
- **Alpha-Beta Pruning**: Prunes unpromising branches when candidate scores exceed the beta threshold.
- **MVV-LVA Move Ordering**: Captures are prioritized by Most Valuable Victim - Least Valuable Attacker (`10000 + 10 * VictimValue - AttackerValue`), maximizing beta cutoffs early in search.
- **Depth & Evaluation**: Defaults to depth 3, balancing tactical precision and response latency. Evaluation computes raw piece material values (P: 100, N: 320, B: 330, R: 500, Q: 900, K: 20000) augmented with piece-square tables rewarding center control and king safety.

## Run Instructions

Set the gauntlet URL and run the engine directly:

```bash
# Set gauntlet environment URL
export MAKEFUN_ENV_URL="http://localhost:8080"

# Run autonomous engine
python main.py
```

Or run the uncompressed source engine:

```bash
python engine.py
```
