# tiny-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/airdropgodx24/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/airdropgodx24/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

tiny-chess is a complete chess engine in one Python file. To fit the 4,096-byte limit, main.py carries the engine as an lzma-compressed, base85-encoded payload behind a short unpacker, a format the rules explicitly allow. Unpacked, it is an original engine written for this bounty: a 0x88 board with full legal move generation (castling, en passant including the pinned case, promotions), incremental Zobrist hashing, and a negamax alpha-beta search.

The search runs iterative deepening under a fixed budget of 45,000 nodes per move, never a wall clock, so every game replays move for move. Inside it: a transposition table, quiescence over captures, promotions and check evasions, null-move pruning, check extensions, late move reductions, and principal-variation search. Moves are ordered by the table move, then MVV-LVA captures and promotions, then killers. Evaluation is material plus formula piece-square terms: pawn advancement, knight and bishop centrality, the bishop pair, rooks on the seventh rank, and a king that shelters in the corner in the middlegame and centralises in the endgame. Repetition and the fifty-move rule score as draws inside the search.

Measured locally on the kit's practice gauntlet (six house engines anchored at Elo 855 to 1596), the three practice trials scored Elo 1364, 1191 and 1545, a mean of 1367: nine wins, four draws and five losses in 18 games, with checkmate wins over every rung except the 100k-node engine. Repeat runs produced move-for-move identical games. The mean sits above the 1,154 practice floor and level with the sunfish-4k baseline's practice mean of 1365, though single trials swung well either side of it.

## Run it

The harness runs the engine as `python3 main.py` with MAKEFUN_ENV_URL set. To play a practice gauntlet, start the kit's env with a trial's gauntlet and run the same command against its address. To read the engine source, base85-decode the string in main.py and lzma-decompress it (FORMAT_ALONE).

<sub>Entered on [make.fun](https://make.fun/?ref=ty7xpzdw&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
