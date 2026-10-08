# 📦 CA1 · Search Algorithms for a Portal Warehouse

🧠 **Artificial Intelligence** · 🔎 **State-space search** · 🐍 **Python & Jupyter**

Help Mike Wazowski organize the scream warehouse! This assignment models a Sokoban-style puzzle: push each numbered box onto its matching goal while navigating walls and paired portals. It explores how uninformed and informed search differ in solution length, explored states, and runtime.

## 🎯 Assignment goals

Based on the [assignment specification](AI-S04-CA1.pdf):

- Model the initial state, legal actions, goal test, and search state efficiently.
- Implement **BFS**, **DFS**, **iterative deepening search (IDS)**, **A\***, and **weighted A\***.
- Compare at least two heuristics, including the limitations of Manhattan distance when portals exist.
- Discuss heuristic admissibility and consistency, and compare runtime, solution paths, and visited-state counts across the supplied maps.
- Seek minimum-move solutions for BFS and ordinary A\*; investigate the speed/quality trade-off of weighted A\*.

## 🗺️ Puzzle rules

| Symbol | Meaning |
| --- | --- |
| `H` | Player position |
| `Bi` | Box with identifier `i` |
| `Gi` | Destination for box `Bi` |
| `Pi` | One endpoint of portal pair `i` |
| `W` | Wall |
| `.` | Empty floor |
| `/` | Separates overlapping elements, such as `G1/H` |

Moves use `U`, `D`, `L`, and `R`. A player can push one box at a time. Entering a portal moves the player or box through its paired endpoint in the same direction. A win requires **every box to reach its own numbered goal**.

## 📁 Files

| File | Purpose |
| --- | --- |
| [Assignment PDF](AI-S04-CA1.pdf) | Problem statement, algorithm requirements, and evaluation questions |
| [notebook.ipynb](Code/notebook.ipynb) | Solver implementations, map tutorial, and experiment runner |
| [game.py](Code/game.py) | Puzzle simulation, movement rules, and solution validation |
| [gui.py](Code/gui.py) | Raylib-based graphical game |
| [Maps](Code/assets/maps/) | Ten maps and a supplied solutions text file |
| [Assets](Code/assets/) | Maps, sprites, and audio |
| [Project report](Code/گزارش%20تمرین%20کامپیوتری%201.pdf) | Submitted analysis |

## 🧩 Implementation

The notebook represents a state using the player position and ordered box positions. It defines `solver_bfs`, `solver_dfs`, `solver_ids`, and `solver_astar`; each returns a move sequence (or `None`) and an expansion counter.

The A\* implementation uses `f = g + weight * h`, with **`weight=2` by default**. Two heuristics add box-to-goal Manhattan distances to either the distance to the first box or the nearest box. IDS currently searches up to depth **25**.

## 🚀 Getting started

From the repository root, install Jupyter and open the notebook from its working directory:

```bash
python -m pip install jupyterlab
cd CA1/Code
python -m jupyterlab notebook.ipynb
```

Run the imports, map-loading helpers, and solver definitions in order. Then use a notebook cell such as:

```python
solve(5, "A*")
```

The runner prints elapsed time, expanded states, and the returned move sequence. To validate a returned sequence independently:

```python
game_map = load_map(5)
moves, expanded = solver_astar(game_map)
if moves is not None:
    print(Game(game_map).is_solution_valid(moves))
```

For the optional graphical interface, run these commands from `CA1/Code`:

```bash
python -m pip install raylib
python gui.py
```

Use the arrow keys and Enter in the menus, then the arrow keys or WASD to move.

## 📝 Notes on the submitted version

- The final `solve_all()` call has no active definition: its definition is inside a triple-quoted string. Skip that cell or restore the definition before using it.
- The GUI's `SOLVERS` dictionary is empty, so its default mode is manual play. Notebook solvers must be connected explicitly to enable graphical AI playback.
- BFS and DFS check for a win before restoring the dequeued state's positions. Validate returned paths before treating their results as correct.
- The default A\* entry is weighted, and the heuristics do not account for portal shortcuts. The code does **not establish the optimality guarantee requested in the PDF**.
- Runtime targets in the PDF are assignment guidance, not measured guarantees for this implementation.
