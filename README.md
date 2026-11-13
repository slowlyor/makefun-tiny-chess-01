# makefun-tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/slowlyor/makefun-tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/slowlyor/makefun-tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine that fits in 4 KB of Python. `main.py` is the whole engine: a 0x88 board, negamax alpha-beta search with quiescence and check evasions, a transposition table, null-move pruning, PVS with late-move reductions, killer-move ordering, and piece-square-table evaluation with a separate endgame king table. The source is packed as an lzma payload with a short unpacker so the file stays under the 4,096-byte cap. It plays the make.fun gauntlet through the env at `MAKEFUN_ENV_URL`, searching to a fixed node budget and never reading a clock, so every replay makes the same moves.

## Run it

```sh
# needs a make.fun tiny-chess-01 env (the gauntlet server) reachable:
MAKEFUN_ENV_URL=http://store:8080 python3 main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=v8j9bb4h&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
