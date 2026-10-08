# 🖼️ CA4 · Fully Connected Networks vs. CNNs

🧠 **Deep Learning** · 🔥 **PyTorch** · 🔍 **Visual representations**

Compare a fully connected neural network with a convolutional neural network on CIFAR-10, then inspect what the CNN learns through nearest neighbors, t-SNE, and intermediate feature maps.

## 🎯 Assignment goals

The [assignment specification](AI_S04_CA4.pdf) asks for two image classifiers with approximately **33.5 million trainable parameters, within ±0.5 million**, trained for **60 epochs each**. The goal is to compare architectures under similar model-size and training-budget constraints.

The analysis covers loss and accuracy curves, overfitting, test performance, 24 misclassified images, neighbors in learned feature space, a two-dimensional t-SNE projection, and convolutional feature maps.

## 📁 Files

| File | Purpose |
| --- | --- |
| [Assignment PDF](AI_S04_CA4.pdf) | Architecture constraints and experiment requirements |
| [AI_S04_CA4_810102603.ipynb](Code/AI_S04_CA4_810102603.ipynb) | Data loading, both models, training, and visual analysis |

The dataset and trained checkpoints are **not included**. Executing the notebook downloads CIFAR-10 to `Code/data/` and saves `fully-connected.pth` and `cnn.pth` in the notebook's working directory.

## 🗂️ Dataset

CIFAR-10 contains RGB images of size **32 × 32** from ten classes: airplane, automobile, bird, cat, deer, dog, frog, horse, ship, and truck.

| Split | Images |
| --- | --- |
| Training | 45,000 |
| Validation | 5,000 |
| Test | 10,000 |

The notebook normalizes each color channel and uses a batch size of **512**. Its inverse-normalization helper restores images for display.

## 🏗️ Implemented architectures

| Component | Fully connected network | `DeepCNN` |
| --- | --- | --- |
| Input processing | Flatten to 3,072 values | Eight 3 × 3 convolutional layers |
| Hidden structure | 4,096 → 4,096 → 1,024 | Channel stages 64 → 128 → 256, each followed by pooling |
| Classification head | 1,024 → 10 | 4,096 → 5,632 → 1,408 → 512 → 10 |
| Activation | ReLU | ReLU |
| Dropout | 0.30 | 0.55 in the dense head |
| Optimizer | Adam, learning rate 0.001 | AdamW, learning rate 0.001 |
| Loss | Cross-entropy | Cross-entropy |

Each training loop records training/validation loss and accuracy. The CNN's **512-dimensional representation before the final output layer** is used for nearest-neighbor retrieval and t-SNE.

## 🚀 Getting started

From the repository root, install the notebook dependencies in an environment compatible with PyTorch:

```bash
python -m pip install jupyterlab torch torchvision torchsummary numpy matplotlib scikit-learn
cd CA4/Code
python -m jupyterlab AI_S04_CA4_810102603.ipynb
```

The notebook selects CUDA when available and otherwise uses the CPU. A GPU environment is useful for the two 60-epoch training runs. Internet access is needed for the initial dataset download.

Before running all cells, **remove the stray question-mark characters at the end of the `fully-connected.pth` loading line**, or skip that optional loading cell. As submitted, it contains a Python syntax error.

Run data preparation, the fully connected experiment, the CNN experiment, and finally the feature-analysis cells in order. Checkpoint loading requires an existing checkpoint with the corresponding architecture.

## 📊 What to explore

- Training and validation curves for both architectures.
- Test loss and accuracy, plus a grid of incorrect predictions.
- Five nearest training neighbors for each of five correctly classified test examples.
- A t-SNE visualization of 2,000 sampled feature vectors.
- Outputs from the first two convolutional layers, visualized as feature maps.

## 📝 Notes on the submitted version

- The two models use different optimizers and dropout rates, so those choices also affect the comparison.
- The dataset split is not explicitly seeded. Record seeds and environment details for repeatable experiments.
- Several examples are selected by traversal order rather than randomly; the feature-map example uses a fixed training image.
- The learning-rate-scheduler section is an empty placeholder. No scheduler is configured in the current training loop.
- Notebook outputs are saved experiment artifacts; the training runs have not been rerun as part of this documentation update.
