## Lab 3: N-Puzzle problem

## Overview
This implements a solver for the n-puzzle problem using the **A\*** search algorithm.
The n-puzzle problem is a sliding puzzle consisting of a grid with numbered elements and one empty space. The goal is to rearrange the tiles from an initial configuration to a target configuration (goal state).


---

## Key Features
1. **A\* Algorithm Implementation**:  
   Uses the A\* search strategy to find the optimal solution path by minimizing the cost function `f(n) = g(n) + h(n)`, where:
   - `g(n)` is the cost to reach the current state.
   - `h(n)` is the heuristic estimate of the cost to reach the goal state.

2. **Heuristic Functions**:
   - **Manhattan Distance**: Measures the sum of the distances of tiles from their goal positions
   - **Linear Conflict**: Adds penalties for tiles that are in their correct row or column but are blocking each other

3. **Optimizations**:
   - Precomputed goal positions to speed up heuristic calculations
   - State representation using `tobytes()` for efficient storage and comparison

4. **Configurable Puzzle Dimensions**:  
   Supports n-puzzle configurations of any size by modifying the `PUZZLE_DIM` variable



---


## Limitations
A challenge encountered was solving large puzzles such as 4x4, 5x5 and so on. 
Several attempts were made using both Manhattan distance alone and a combination of Manhattan distance with Linear Conflict. However, when using the second approach, there were improvements in terms of memory usage, but it remained almost impossible to solve large puzzles within a reasonable amount of time. 
For this reason, when dealing with large puzzles, the number of random steps in the initialization phase was reduced, and only in this way was it possible to find a solution within reasonable time limits. 
By reducing the randomness in the initialization phase, I perform a check to ensure that the puzzle is solvable before attempting to solve it.

---

## Performance
The solver is efficient for small puzzles (3x3). 
For larger puzzles, the time and memory requirements increase due to the combinatorial complexity of the state space.

---
## Results
| Puzzle Dimension |Puzzle Size | Quality (Number of Actions) | Cost (Total Actions Evaluated) | Solving Time|
|-------------|-------------|------------------------|--------------|-----------------------------|
| 3 |8-puzzle    |       17             |    144      |                   0.001 s       |
| 4 |15-puzzle   |       47            |      2905789    |             40.68 s              |
| 5 |24-puzzle   |        21          |     2053     |               0.02 s            |

Using 100,000, 1000, 100 random steps respectively for each puzzle size.