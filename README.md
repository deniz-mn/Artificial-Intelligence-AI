# 🧠 Artificial Intelligence · Course Projects

🐍 **Python** · 📓 **Jupyter Notebooks** · 🔎 **Search** · 🌳 **Machine Learning** · 🔥 **Deep Learning**

Five hands-on Artificial Intelligence projects covering state-space search, evolutionary optimization, adversarial games, supervised learning, neural networks, and text clustering. Each project includes its assignment PDF, source code, and an English guide explaining the task, implementation, setup, and limitations of the submitted version.

## 🗺️ Explore the projects

| Project | Topic | What you will find |
| --- | --- | --- |
| [📦 CA1 · Portal Warehouse](CA1/README.md) | Search algorithms | BFS, DFS, IDS, A\*, and weighted A\* for a box-pushing puzzle with portals; a game simulator and optional graphical interface |
| [🧬 CA2 · Genetic Optimization & Pentago](CA2/README.md) | Evolutionary and adversarial search | Fourier coefficient optimization with a genetic algorithm, plus minimax and alpha-beta search for Pentago |
| [🎓 CA3 · Student Grade Classification](CA3/README.md) | Supervised learning | Gaussian naive Bayes, decision trees, random forests, XGBoost, and a custom ID3 tree |
| [🖼️ CA4 · Fully Connected Networks vs. CNNs](CA4/README.md) | Deep learning and computer vision | CIFAR-10 classification with PyTorch, training curves, nearest neighbors, t-SNE, and feature maps |
| [🎵 CA5 · Song Lyrics Clustering](CA5/README.md) | Unsupervised learning and NLP | Text preprocessing, sentence embeddings, K-Means, DBSCAN, agglomerative clustering, and PCA |

## 📁 Repository layout

```text
Artificial-Intelligence-AI/
├── README.md
├── CA1/                  # Search and portal warehouse puzzle
├── CA2/                  # Genetic algorithm and Pentago
├── CA3/                  # Student grade classification
├── CA4/                  # Fully connected and convolutional networks
└── CA5/                  # English song lyrics clustering
```

Each `CA` folder contains a `README.md`, an assignment PDF, and a `Code/` directory. Reports are also included for CA1, CA2, and CA3. Project guides link directly to their notebooks, data, reports, and supporting assets.

## 🚀 Getting started

Clone the repository and choose a project:

```bash
git clone https://github.com/deniz-mn/Artificial-Intelligence-AI.git
cd Artificial-Intelligence-AI
```

Open the corresponding project guide from the table above and follow its dependency and setup instructions. The projects use different packages, so install the dependencies for the project you want to explore.

For example, to open the CA1 notebook:

```bash
python -m pip install jupyterlab
cd CA1/Code
python -m jupyterlab notebook.ipynb
```

Run notebooks from their project's `Code/` directory so relative file paths resolve correctly. Execute the required definition and setup cells in order, following the project-specific notes before running experiments.

## 🧰 Tools used

| Area | Libraries and tools |
| --- | --- |
| Notebook environment | Python, JupyterLab |
| Numerical computing and visualization | NumPy, pandas, Matplotlib |
| Classical machine learning | scikit-learn, XGBoost |
| Neural networks | PyTorch, torchvision, torchsummary |
| Text processing and embeddings | NLTK, SentenceTransformers |
| Game interfaces | Raylib in CA1; optional, unfinished Pygame interface in CA2 |

## 📦 Data and execution notes

| Project | Input availability and preparation |
| --- | --- |
| CA1 | Maps, sprites, and audio are included. Read the guide before using the solver or batch-execution cells. |
| CA2 | Target functions and the game board are generated in code; no external dataset is needed. |
| CA3 | `Grades.csv` is included. Replace the notebook's machine-specific CSV path before running. |
| CA4 | CIFAR-10 is downloaded on first use. Trained checkpoints are not included. Correct or skip the malformed checkpoint-loading cell before a full run. |
| CA5 | `musicLyrics.csv` is not included. Supply the assignment dataset and update its path. NLTK resources and the sentence model require initial downloads. |

A GPU is useful for CA4's two 60-epoch training runs. Some search and tuning experiments can also be time-consuming, particularly deeper Pentago search and the CA3 XGBoost grid search.

## 📝 About these submissions

These are educational project submissions with saved notebook outputs. The project guides distinguish assignment requirements from the implemented behavior and document known execution or evaluation issues. Read those notes before interpreting results or comparing models. Full notebook execution and model retraining were not performed during the documentation review.
