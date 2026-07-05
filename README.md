# 🧩 CubeCraft — Rubik's Cube Solver

CubeCraft is a C++ Rubik's Cube solver with multiple solving algorithms, several cube representations, and an OpenCV-based webcam scanner for scanning a physical cube.

## Features

- Multiple cube representations for benchmarking and experimentation
- Solving algorithms including BFS, DFS, IDDFS, and IDA*
- Corner pattern database heuristic for faster IDA* solving
- OpenCV webcam scanner for scanning and solving a physical cube
- Cross-platform build support with CMake

## Requirements

- CMake 3.20 or newer
- A C++14-compatible compiler
- OpenCV 4.x for the webcam scanner

## Build

```bash
cmake -B build -S .
cmake --build build
```

## Usage

Run the built executable from the `build` directory:

```bash
./build/rubiks_cube_solver
```

If you want to use the terminal demo mode instead of the webcam scanner, check `main.cpp` for the available solver test sections.

## Project Structure

- `main.cpp` — entry point for the solver and scanner demo
- `Model/` — Rubik's Cube representations
- `Solver/` — solving algorithms
- `PatternDatabases/` — corner pattern database implementation
- `Scanner/` — OpenCV webcam scanner
- `Databases/` — precomputed heuristic data
- `bits/` — portable standard library header
- `CMakeLists.txt` — build configuration

## Credits

- Original solver by Lakshya Mittal
- Scanner and modifications by Pranav Harresh
- Maintained by Kunal Tailor

## License

Open source and available for educational purposes.
