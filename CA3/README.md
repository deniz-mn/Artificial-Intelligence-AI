# 🎓 CA3 · Student Grade Classification

🧠 **Machine Learning** · 🌳 **Tree models** · 📊 **Model evaluation**

Predict a student's final Artificial Intelligence grade category from demographic, social, and academic attributes. This project follows a tabular classification workflow and compares library models with a decision tree implemented from scratch.

## 🎯 Assignment goals

The [assignment specification](AI-S04-CA3.pdf) covers data cleaning, categorical encoding, feature scaling, an 80/20 train-test split, model training, hyperparameter tuning, and evaluation. It asks for Gaussian naive Bayes, decision trees, random forests, XGBoost, and a custom entropy-based decision tree, followed by a comparison of their predictions.

Evaluation topics include accuracy, precision, recall, F1, confusion matrices, and macro, micro, and weighted averaging. Tree visualization and feature importance help explain the predictions.

## 📁 Files and data

| File | Purpose |
| --- | --- |
| [Assignment PDF](AI-S04-CA3.pdf) | Dataset description, required models, and evaluation criteria |
| [AI_CA3.ipynb](Code/AI_CA3.ipynb) | Preprocessing, training, tuning, and evaluation |
| [Grades.csv](Code/Grades.csv) | Included dataset: 397 records and 25 columns |
| [Project report](Code/AI_CA3_rep.pdf) | Submitted analysis |

The data contains attributes such as age, university, study time, absences, parental education, and previous course grades. `finalGrade` is the target and is removed from the input features.

## 🏷️ Target categories

The notebook's exact boundary rules are:

| Encoded class | Display label | Final grade |
| --- | --- | --- |
| `0` | A | Greater than 17 |
| `1` | B | Greater than 14 and at most 17 |
| `2` | C | Greater than 10 and at most 14 |
| `3` | D | At most 10 |

## 🛠️ Workflow and models

1. Inspect categorical values and remove `motherJob`, `fatherJob`, and `reason`.
2. Encode categorical columns and min-max normalize `age`, `EPSGrade`, and `DSGrade`.
3. Convert the target into four classes and create a seeded 80/20 split.
4. Train and compare the following models.

| Model | Notebook approach |
| --- | --- |
| Gaussian naive Bayes | `GaussianNB` baseline |
| Decision tree | Five-fold `GridSearchCV` over depth and minimum split/leaf sizes |
| Random forest | `RandomForestClassifier(random_state=42)` |
| XGBoost | Five-fold grid search over six hyperparameters using weighted F1 |
| Custom ID3 tree | Entropy and information gain, recursive categorical splits, depth/sample/gain stopping rules |

Outputs include classification charts, confusion matrices, a plotted decision tree, and feature-importance charts.

## 🚀 Getting started

From the repository root:

```bash
python -m pip install jupyterlab pandas numpy matplotlib scikit-learn xgboost
cd CA3/Code
python -m jupyterlab AI_CA3.ipynb
```

Before running the notebook, replace the machine-specific path in the first CSV-loading cell with:

```python
df = pd.read_csv("Grades.csv")
```

Then run the cells in order. The XGBoost grid contains **729 parameter combinations**, each evaluated with five-fold cross-validation, so this section can take substantially longer than the baseline models.

## 📝 Notes on the submitted version

- Scaling currently happens before splitting the dataset. The PDF asks for preprocessing statistics fitted on training data only; the current order can leak test-set information.
- The PDF requests random-forest tuning with `RandomizedSearchCV`. The notebook imports it but trains the forest without that search.
- The random-forest confusion-matrix cell uses `y_pred`, while its predictions are stored in `y_pred_tree`. Use the latter when evaluating the forest.
- The custom tree returns `None` for unseen feature values. Its evaluation drops those cases, so its reported scores cover a subset of the test set and are not directly comparable to full-test-set scores.
- The notebook focuses on macro/weighted summaries and per-class metrics; it does not provide every analysis requested in the PDF. Stored outputs should be interpreted with the above limitations in mind.
