# makefun-tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/slowlyor/makefun-tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/slowlyor/makefun-tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine that fits in 4 KB of Python. `main.py` is the whole engine: a 0x88 board, negamax alpha-beta search with quiescence and check evasions, a transposition table, null-move pruning, PVS with late-move reductions, killer-move ordering, and piece-square-table evaluation with a separate endgame king table. The source is packed as an lzma payload with a short unpacker so the file stays under the 4,096-byte cap. It plays the make.fun gauntlet through the env at `MAKEFUN_ENV_URL`, searching to a fixed node budget and never reading a clock, so every replay makes the same moves.

## Engine

The board is a 0x88 array, so off-board tests are a single `& 136` check. Search is negamax alpha-beta with quiescence (captures only, plus full check evasions when in check), backed by a transposition table keyed on Zobrist hashes. Null-move pruning, principal-variation search with late-move reductions, and killer-move ordering keep the tree small enough for pure Python. Evaluation is incremental piece-square tables — material plus placement, scored as the board changes — with a separate endgame king table that blends in once both queens are gone. Every move searches to a fixed budget of 40,000 nodes and never consults a clock, which makes games exactly reproducible; on the kit's practice gauntlet it reached Elo 1464.

## Run it

```sh
# needs a make.fun tiny-chess-01 env (the gauntlet server) reachable:
MAKEFUN_ENV_URL=http://store:8080 python3 main.py
```

## Development

`main.py` in this repository is the deliverable, but it is not written by hand: it is the kit-compressed pack of a readable source file, `engine.py`, which is kept beside the repository (uncommitted) so the engine stays reviewable. The pack is produced with the kit CLI's own compressor — `node cli/makefun.mjs compress engine.py --out main.py`, run from the kit — which wraps the source in an lzma payload plus a short unpacker; decoding the payload reproduces `engine.py` byte for byte. Any change to the engine is made in `engine.py` first and then re-packed, never edited into `main.py` directly.

---

<sub>Entered on [make.fun](https://make.fun/?ref=v8j9bb4h&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
