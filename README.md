# Autonomous Robot Grid Navigation: BFS vs. Sweep

An autonomous robot pathfinding and exploration simulation built in Python 3. The agent operates on a 10x10 discrete 2D grid with obstacles, aiming to collect scattered items using two distinct movement algorithms: **Breadth-First Search (BFS)** and a **Heuristic Serpentine Sweep**.

---

## Overview

The robot starts at coordinate `(0, 0)` and navigates an environment populated with obstacles and collectible items. The program reads a custom `.txt` world file, parses the grid, executes the chosen exploration strategy, and tracks real-time telemetry (steps, robot coordinates, score, and termination conditions).

### Key Features
* **Dual Navigation Modes:** Switch between optimal graph search (BFS) and deterministic area coverage (Sweep).
* **Dynamic Telemetry:** Prints periodic status updates every 10 steps and whenever an item is collected.
* **Autonomous Obstacle Handling:** Dedicated rerouting logic for bypassing non-traversable cells during continuous scanning.

---

## Movement Strategies

### 1. Breadth-First Search (BFS)
* Computes the **shortest unweighted path** to the nearest collectible item (`*`) using a queue data structure (`collections.deque`).
* Ensures optimal step efficiency while navigating around obstacles (`#`).
* Repeats iteratively from the robot's current position to the next nearest target.
* **Termination:** All items are successfully collected, no path is reachable, or the hard execution limit of **80 steps** is reached.

### 2. Serpentine Sweep (Boustrophedon Coverage)
* Explores the grid systematically row-by-row in an alternating horizontal pattern (left-to-right, then right-to-left).
* Shifts down to the subsequent row upon hitting a grid boundary.
* **Obstacle Handling (`sweep_obstacle`):** When encountering a barrier (`#`), the robot dynamically routes up or down to bypass the obstacle and returns to its original row trajectory once the path clears.

---

## Grid Specification

The environment is represented as a text file (`world.txt`) with exactly **10 rows and 10 columns**:

| Symbol | Description | Traversable |
| :---: | :--- | :---: |
| `.` | Free space | Yes |
| `#` | Obstacle | No |
| `*` | Collectible Item | Yes |

### Sample `world.txt` Layout
```text
. . . . . . . . . .
. # # . . . * . . .
. . . . . # . . . .
. . * . . # . . . .
. . . . . . . # . .
. . # # # . . # . .
. . . . . . . . . .
. . . . * . . . . .
. . . . . . # # . .
. . . . . . . . * .
