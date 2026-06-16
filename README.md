# 🧩 CubeCraft — Rubik's Cube Solver

A high-performance Rubik's Cube solver written in C++ featuring multiple solving algorithms (BFS, DFS, IDDFS, IDA*) and a real-time **OpenCV webcam scanner** to scan and solve a physical cube.

---

## ✨ Features

- **Multiple Cube Representations** — 3D Array, 1D Array, and Bitboard for benchmarking
- **4 Solving Algorithms** — BFS, DFS, IDDFS, and IDA* with Corner Pattern Database heuristic
- **Webcam Scanner** — Scan a real Rubik's Cube using OpenCV and get the solution moves
- **Corner Pattern Database** — Pre-computed heuristic database (~50MB) for optimal IDA* solving
- **Cross-Platform** — Built with CMake, runs on macOS, Linux, and Windows

---

## 🏗️ Project Structure

```
CubeCraft/
├── main.cpp                     # Entry point — scanner + solver demo
├── CMakeLists.txt               # Build configuration
│
├── Model/                       # Rubik's Cube representations
│   ├── RubiksCube.h/.cpp        # Abstract base class
│   ├── RubiksCube3dArray.cpp    # 3D array representation
│   ├── RubiksCube1dArray.cpp    # 1D array representation
│   └── RubiksCubeBitboard.cpp   # Bitboard representation (fastest)
│
├── Solver/                      # Solving algorithms
│   ├── BFSSolver.h              # Breadth-First Search
│   ├── DFSSolver.h              # Depth-First Search
│   ├── IDDFSSolver.h            # Iterative Deepening DFS
│   └── IDAstarSolver.h          # IDA* with pattern database heuristic
│
├── PatternDatabases/            # Corner pattern database implementation
│   ├── CornerPatternDatabase.*  # Corner-based heuristic
│   ├── CornerDBMaker.*          # Database generator
│   ├── PatternDatabase.*        # Base pattern database
│   ├── NibbleArray.*            # Compact 4-bit storage
│   ├── PermutationIndexer.h     # Permutation indexing for corners
│   └── math.*                   # Combinatorial math utilities
│
├── Scanner/                     # OpenCV webcam scanner
│   ├── CubeScanner.h            # Scanner interface
│   └── CubeScanner.cpp          # Color detection & face capture
│
├── Databases/                   # Pre-computed databases
│   └── cornerDepth5V1.txt       # Corner pattern database (~50MB)
│
└── bits/
    └── stdc++.h                 # Portable standard library header
```

---

## 📋 Prerequisites

- **CMake** ≥ 3.20
- **C++14** compatible compiler (Clang, GCC, MSVC)
- **OpenCV** 4.x (for webcam scanner)

### Install on macOS (Homebrew)

```bash
brew install cmake opencv
```

### Install on Ubuntu/Debian

```bash
sudo apt install cmake libopencv-dev
```

---

## 🔨 Build

```bash
# Configure
cmake -B build -S .

# Build
cmake --build build
```

---

## 🚀 Usage

### Webcam Scanner Mode (default)

The default mode opens your webcam to scan a physical Rubik's Cube:

```bash
./build/rubiks_cube_solver
```

**How to scan:**
1. Hold each face of your cube in front of the webcam
2. Align it within the 3×3 grid overlay
3. Press **SPACE** to capture
4. Press **N** to accept the scanned face, or **R** to rescan
5. Scan all 6 faces in order: **UP → LEFT → FRONT → RIGHT → BACK → DOWN**
6. The solver outputs the solution moves automatically

### Terminal Demo Mode

To run all solvers with random shuffles (no webcam needed), uncomment the solver test sections in `main.cpp`.

---

## 🧠 Algorithms

| Algorithm | Type | Optimal? | Max Depth | Speed |
|-----------|------|:--------:|:---------:|-------|
| **BFS** | Breadth-First Search | ✅ Yes | ~6 moves | Slow (memory heavy) |
| **DFS** | Depth-First Search | ❌ No | Configurable | Fast but may not find shortest |
| **IDDFS** | Iterative Deepening DFS | ✅ Yes | ~7 moves | Moderate |
| **IDA*** | IDA* + Corner DB Heuristic | ✅ Yes | 13+ moves | Fast with heuristic |

### How IDA* Works

1. Uses a pre-computed **Corner Pattern Database** that stores the minimum moves needed to solve just the 8 corners of the cube
2. This serves as an **admissible heuristic** — it never overestimates the actual number of moves
3. Combined with iterative deepening, IDA* efficiently finds optimal solutions for deeply shuffled cubes

---

## 🎨 Cube Layout

The cube net is displayed in this format:

```
         W W W          ← UP face
         W W W
         W W W

G G G    R R R    B B B    O O O
G G G    R R R    B B B    O O O    ← LEFT, FRONT, RIGHT, BACK
G G G    R R R    B B B    O O O

         Y Y Y
         Y Y Y          ← DOWN face
         Y Y Y
```

**Colors:** W = White, R = Red, G = Green, B = Blue, O = Orange, Y = Yellow

---

## 📝 Notation

Standard Rubik's Cube move notation:

| Move | Description |
|------|-------------|
| `U` / `U'` / `U2` | Up face: clockwise / counter-clockwise / 180° |
| `D` / `D'` / `D2` | Down face |
| `L` / `L'` / `L2` | Left face |
| `R` / `R'` / `R2` | Right face |
| `F` / `F'` / `F2` | Front face |
| `B` / `B'` / `B2` | Back face |

---

## 🤝 Credits

- Original solver by **Lakshya Mittal** (2021)
- Scanner & modifications by **Pranav Harresh** (2025)
- Maintained by **Kunal Tailor**

---

## 📄 License

This project is open source and available for educational purposes.