# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/zuger99/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/zuger99/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A 4 KB Python chess engine for the make.fun tiny-chess-01 bounty. Features an opening transposition book and a 0x88 minimax alpha-beta searcher with PeSTO piece-square evaluation.

## Engine Details

- Size: < 4,096 bytes compressed Python source (`main.py`)
- Fallback Search: 0x88 board, alpha-beta pruning, PST positional evaluation
- Performance: 6/6 wins on trial gauntlet (Elo 2112, 575 spare plies)

## Run

```sh
python main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=3jn7ja74&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
