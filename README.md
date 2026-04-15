# Chess-Analyser

Interactive chess position analyzer with SFML GUI.

The app lets you place pieces on the board, flip side to move, and evaluate positions with check/checkmate/stalemate detection and short mate search.

## Current Optimization Status

Short answer: not all possible optimizations are finished yet.

What is already optimized in the current codebase:

1. Move simulation uses undo records instead of copying full board state per move.
2. Piece ownership is handled with std::unique_ptr to avoid manual memory management.
3. Legal move generation reuses make/undo flow and avoids expensive full clones.
4. King positions are cached and updated incrementally for fast check validation.
5. Mate search depth is hard-limited to 2 plies in GUI evaluation to keep interaction responsive.

What can still be improved later:

1. Better move ordering (MVV-LVA, killer/history heuristics).
2. Transposition table with Zobrist hashing.
3. Incremental evaluation instead of full-board evaluation every node.
4. More selective search extensions/reductions.
5. Additional profiling-guided micro-optimizations in hot paths.

## Features

1. 8x8 interactive board rendered with SFML.
2. Click-to-cycle piece placement.
3. Side-to-move switch via Space key.
4. Check highlight for both kings.
5. Position evaluation output in GUI.
6. Mate search up to 2 plies.
7. Stalemate and checkmate detection.

## Project Structure

1. main.cpp - app entry point.
2. game.h / game.cpp - GUI, rendering, interaction, position evaluation text.
3. chess.h / chess.cpp - board state, rules, move generation, search, evaluation.
4. piece.cpp - piece movement validation rules.
5. matrix.h - matrix container used by board.
6. images/ and arial.ttf - runtime assets.

## Requirements

1. CMake 3.16+
2. C++17 compiler (GCC/Clang)
3. SFML (graphics, window, system)

Ubuntu/Debian example:

```bash
sudo apt update
sudo apt install -y cmake g++ libsfml-dev
```

## Build and Run

Recommended out-of-source build:

```bash
cmake -S . -B build
cmake --build build -j
./build/ChessAnalyser
```

In-source build (supported in this repository as well):

```bash
cmake .
cmake --build . -j
./ChessAnalyser
```

## GUI Controls

1. Left-click board square: cycle piece on that square.
2. Space: toggle side to move (White/Black).
3. Clear Board button: remove all pieces.

## Notes About Analysis

1. Mate search depth is intentionally capped at 2 plies for speed in interactive mode.
2. Reported score is material-based static evaluation when no forced mate is found.
3. This is a practical analyzer, not a full-strength chess engine.

## Troubleshooting

1. If textures do not load, verify images/ exists next to the executable.
2. If font does not load, place arial.ttf near the executable or use system fallback fonts.
3. If CMake cache conflicts happen, remove generated artifacts and reconfigure:

```bash
rm -rf CMakeCache.txt CMakeFiles cmake_install.cmake Makefile build
cmake -S . -B build
```

## License

No license file is currently provided.
Add a LICENSE file if you plan to distribute this project publicly.
