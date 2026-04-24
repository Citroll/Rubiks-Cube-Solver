# Rubik's Cube Solver

A high-performance solver for Rubik's Cubes using the Iterative Deepening A* (IDA*) algorithm with advanced cube theory optimizations.

![Java](https://img.shields.io/badge/Java-17+-orange?style=flat-square)
![Algorithm](https://img.shields.io/badge/Algorithm-IDA*-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-green?style=flat-square)

## 📖 Overview

This project implements an efficient Rubik's Cube solver capable of finding optimal or near-optimal solutions for scrambled 3x3 Rubik's Cubes. The solver uses **Iterative Deepening A* (IDA*)**, a memory-efficient search algorithm combined with pattern databases and heuristics for fast solution discovery.

Built as the final project for SFU's CMPT 225 (Data Structures and Algorithms) course.

## 🎯 Key Features

- **IDA* Search Algorithm**: Combines the memory efficiency of iterative deepening with the optimality of A*
- **Optimized Heuristics**: Uses pattern databases and cube theory to guide the search
- **Fast Computation**: Solves scrambled cubes within a reasonable search depth (up to 20 moves)
- **Flexible I/O**: Reads cube configurations from files and outputs solutions in standard notation
- **Comprehensive Testing**: 40 test cases covering various scramble difficulties
- **Performance Metrics**: Tracks execution time for algorithm optimization analysis

## 🧩 How It Works

### Cube Representation
The cube is represented using a 3x3x3 array of characters, where each character represents a sticker color:
- **O** = Orange (U face)
- **W** = White (F face)
- **G** = Green (L face)
- **Y** = Yellow (R face)
- **B** = Blue (B face)
- **R** = Red (D face)

```
      UUU
      UUU
      UUU
LLLFFFRRRBBB
LLLFFFRRRBBB
LLLFFFRRRBBB
      DDD
      DDD
      DDD
```

### Cube State Components
The solver tracks the cube state using three main components:

1. **Corners** (8 pieces): Each corner has a position and orientation
   - Positions: UFL, URF, UBR, ULB, DLF, DFR, DRB, DBL
   - Orientation: 0, 1, or 2 rotations

2. **Edges** (12 pieces): Each edge has a position and orientation
   - Positions: UR, UF, UL, UB, DR, DF, DL, DB, FR, FL, BL, BR
   - Orientation: 0 or 1 flips

3. **Centers** (6 faces): Fixed reference points for each face

### Move Set
Standard Rubik's Cube notation:
- **Basic Moves**: U, D, L, R, F, B (face rotations)
- **Variants**: 
  - Default (90° clockwise)
  - Prime notation `'` (90° counter-clockwise)
  - Double notation `2` (180°)
- **Total**: 18 possible moves per state

### Search Algorithm: IDA*
The solver uses Iterative Deepening A* which:
1. Starts with a depth limit from the heuristic estimate
2. Performs depth-first search up to that limit
3. Increases depth limit and repeats if no solution found
4. Guarantees finding solutions while minimizing memory usage

## 📋 Getting Started

### Prerequisites
- Java 17 or higher
- A text editor or IDE
- Command line/terminal access

### Compilation

```bash
# Navigate to the project directory
cd Rubiks-Cube-Solver1

# Compile all Java files
javac -cp src -d src src/rubikscube/*.java
```

### Running the Solver

```bash
# Basic usage
java -cp src rubikscube.Solver <input_file> <output_file>

# Example
java -cp src rubikscube.Solver testcases/scramble01.txt output.txt
```

### Input Format

Create a text file with the cube configuration in this format:

```
   OOO
   OOO
   OOO
GGGWWWBBBYYY
GGGWWWBBBYYY
GGGWWWBBBYYY
   RRR
   RRR
   RRR
```

Each line represents three rows of the unfolded cube. Colors are represented by single characters.

### Output Format

The solution is written to the output file as a sequence of moves:

```
UR'URR2
```

This represents: U move, then R' (counter-clockwise), then U, then R twice.

## 📊 Project Structure

```
Rubiks-Cube-Solver1/
├── src/
│   └── rubikscube/
│       ├── Solver.java          # Main entry point
│       └── Solve.java            # Core solving algorithm
├── testcases/
│   ├── base.txt                 # Solved cube (baseline)
│   ├── scramble01.txt - scramble40.txt  # 40 test cases
│   └── sol01.txt - sol03.txt    # Expected solutions
├── scripts/
│   └── use-java21.ps1           # Java version configuration
├── output.txt                   # Example output file
└── README.md                    # This file
```

## 🧪 Testing

The project includes 40 test cases of varying difficulty:

```bash
# Run a single test case
java -cp src rubikscube.Solver testcases/scramble01.txt output.txt

# Run multiple tests (script)
for i in {1..40}; do
  java -cp src rubikscube.Solver testcases/scramble$i.txt output$i.txt
done
```

Each test case contains:
- **Input**: A scrambled cube configuration
- **Expected**: A reference solution (for validation)

## 📈 Performance

The solver is optimized for:
- **Speed**: Finds solutions quickly using informed heuristics
- **Memory**: IDA* uses minimal memory compared to breadth-first search
- **Solution Quality**: Aims for near-optimal or optimal move sequences

Execution time is tracked and reported:
```
Execution time in milliseconds: 1234.5
```

## 🧠 Algorithm Details

### Heuristic Functions
The solver employs pattern databases to estimate distance to the solved state:
1. **Corner Permutation**: How many corners are out of place
2. **Edge Permutation**: How many edges are out of place
3. **Orientation Cost**: Cost of reorienting corners and edges

### State Space
- Total possible Rubik's Cube states: ~4.3 × 10¹⁹
- Solved state: Exactly one configuration
- Search depth: Typically 1-20 moves for solvable configurations

### Optimizations
- **Pruning**: Eliminates branches that exceed depth limits
- **Memoization**: Caches heuristic values to avoid recalculation
- **Move Ordering**: Explores promising moves first to find solutions faster

## 🎓 Learning Outcomes

This project demonstrates:
- **Algorithm Design**: Implementing complex search algorithms
- **Data Structures**: Using arrays, queues, and custom objects for state management
- **Optimization Techniques**: Heuristics, pruning, and memoization
- **Cube Theory**: Understanding permutations, orientations, and movement mechanics
- **Performance Analysis**: Measuring and optimizing execution time
- **File I/O**: Reading and writing data efficiently in Java

## 🔧 Java Version Notes

This project was developed for Java 17+. If using Java 21 or later, see the included `scripts/use-java21.ps1` for configuration details.

## 📚 References

- **Rubik's Cube Notation**: Standard Western notation for cube moves
- **IDA* Algorithm**: Hart, Nilsson, & Raphael (1968) - A*, extended with iterative deepening
- **Pattern Databases**: Culberson & Schaeffer - Heuristic search techniques
- **Rubik's Cube Math**: Group theory applications to permutation puzzles

## 🤝 Contributing

This was a course project completed for CMPT 225. The repository is maintained as a portfolio piece. For questions or suggestions, please contact the project author.

## 📝 License

This project is provided as-is for educational purposes.

---

**Note**: This is an educational project created to demonstrate data structures and algorithms concepts learned in CMPT 225 at Simon Fraser University. The solver implements academic techniques for combinatorial puzzle solving.
