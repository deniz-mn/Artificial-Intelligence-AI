# 🧬 CA2 · Genetic Optimization & Pentago AI

🧠 **Artificial Intelligence** · 🧬 **Genetic algorithms** · 🎲 **Adversarial search**

This project combines two approaches to intelligent decision-making: evolving Fourier coefficients to approximate functions, and searching a Pentago game tree with minimax and alpha-beta pruning.

## 🎯 Assignment goals

The [assignment specification](AI-CA2.pdf) has two parts:

1. **Fourier approximation:** evolve 41 coefficients for a constant term and 20 sine/cosine harmonics. Define a chromosome, initialize a population, choose fitness functions, and implement selection, crossover, mutation, and survivor selection. Compare approximation quality and convergence across functions and parameter choices.
2. **Pentago:** implement minimax and a board evaluation heuristic, add alpha-beta pruning, and compare search depth, runtime, visited nodes, and wins against a random opponent. The PDF requests repeated experiments, including a final 100-game evaluation.

## 📁 Files

| File | Purpose |
| --- | --- |
| [Assignment PDF](AI-CA2.pdf) | Requirements and analysis questions for both parts |
| [CA2-Files.ipynb](Code/CA2-Files.ipynb) | Genetic algorithm, plots, Pentago engine, and search algorithms |
| [Project report](Code/report_CA2_AI.docx) | Submitted report in Word format |

## 🧬 Part 1: Fourier approximation

Each chromosome stores `a0`, 20 cosine coefficients, and 20 sine coefficients. The notebook reconstructs the target using a Fourier model over `(-π, π)`.

| Component | Included implementation |
| --- | --- |
| Population | Uniform sampling within `[-A, A]`, where `A` is the maximum absolute sampled target value |
| Fitness | MSE-based, RMSE-based, and normalized RMSE-based scores |
| Parent selection | Roulette-wheel helper and tournament selection; the main loop uses tournaments |
| Crossover | Single-point, multi-point, and uniform-style variants |
| Mutation | Gaussian perturbation followed by clipping to the coefficient bounds |
| Elitism | Keep the best 10 individuals per generation |

Initial settings are **100 individuals**, **500 generations**, **0.03 mutation rate**, and **100 samples**. A later comparison cell changes the run to 200 generations and 500 samples. Nine target functions include trigonometric mixtures, polynomials, Gaussian, square-wave, and sawtooth examples.

The comparison produces target-versus-approximation plots, absolute-error plots, RMSE values, and `fourier_approximation_comparison.png` when executed.

## 🎲 Part 2: Pentago

Pentago uses a **6 × 6 board** divided into four **3 × 3 blocks**. Each turn places a piece and rotates one block 90 degrees clockwise or counterclockwise. The objective is five consecutive pieces horizontally, vertically, or diagonally.

`PentagoGame` includes legal move generation, rotation, winner detection, a line-based heuristic, minimax, and alpha-beta search. `get_computer_move()` currently selects moves through **alpha-beta pruning**.

The supplied experiment plays **six games at depth 2** against a random opponent. Result codes are `-1` for a computer win, `0` for a draw, and `1` for an opponent win.

## 🚀 Getting started

From the repository root:

```bash
python -m pip install jupyterlab numpy matplotlib
cd CA2/Code
python -m jupyterlab CA2-Files.ipynb
```

Run the genetic algorithm cells in order to reproduce the approximation experiments. To explore the game independently, run the imports in the Minmax section and the `PentagoGame` class definition, then:

```python
game = PentagoGame(ui=False, print=False, depth=2)
result = game.play()
print(result)
```

No external dataset is required. Search becomes expensive as depth increases; start with the supplied depth before expanding the experiment.

## 📝 Notes on the submitted version

- `best_fit_history` is initialized but never populated, so the returned history cannot currently produce a convergence curve.
- The first two fitness helpers read global `tSamples` and `fSamples` instead of their arguments. Keep these globals synchronized when experimenting with those helpers.
- Both minimax and alpha-beta are present, but the final experiment only runs the alpha-beta path. A direct benchmark of the two requires changing the move-selection call and collecting results.
- The optional Pygame interface is unfinished: its import is commented out and some UI methods reference missing font attributes or unsupported calls. Use `ui=False` for the supplied experiment.
- The genetic algorithm and random opponent are stochastic; seed both `random` and `numpy.random` when comparing runs.
