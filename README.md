# Autonomous Robot Grid Navigation (BFS vs. Sweep)

A Python 3 simulation where a robot navigates a 10x10 grid with obstacles to collect targets, starting at `(0,0)`.

---

## Navigation Strategies

* **BFS (Breadth-First Search):**
  * Finds the shortest unweighted path to the closest item (`*`) using `collections.deque`.
  * Navigates around obstacles (`#`).
  * Stops when all items are collected or after reaching **80 steps**.

* **Sweep (Boustrophedon Coverage):**
  * Scans row-by-row, alternating directions (left-to-right / right-to-left).
  * Uses `sweep_obstacle` to bypass obstacles (moves up/down and resumes the scan when clear).

---

## Grid Specification (`world.txt`)

* **Dimensions:** Fixed 10x10 matrix (UTF-8).
* **Symbols:**
  * `.` : Empty cell
  * `#` : Obstacle
  * `*` : Collectible item

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
