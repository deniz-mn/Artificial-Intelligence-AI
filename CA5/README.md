# 🎵 CA5 · Clustering English Song Lyrics

🧠 **Unsupervised Learning** · 💬 **Sentence embeddings** · 🎨 **Cluster visualization**

Explore whether English song lyrics form meaningful groups based on their text. The project cleans lyrics, embeds them with a pretrained sentence model, compares three clustering methods, and visualizes their structure with PCA.

## 🎯 Assignment goals

Based on the [assignment specification](AI-S04-CA5.pdf):

- Clean text and explain preprocessing choices such as stop-word removal and lemmatization.
- Extract features using **SentenceTransformers** and **`all-MiniLM-L6-v2`**.
- Compare **K-Means**, **DBSCAN**, and **hierarchical clustering**, including parameter selection and an elbow plot for K-Means.
- Reduce feature dimensions with **PCA** to visualize the resulting clusters.
- Discuss **silhouette** and **homogeneity** metrics, use the applicable measures, and explain any exclusions.
- Inspect two examples per cluster and compare their semantic or topical similarity.

## 📁 Files and required input

| File | Purpose |
| --- | --- |
| [Assignment PDF](AI-S04-CA5.pdf) | Problem statement and analysis requirements |
| [AI_CA5_810102603.ipynb](Code/AI_CA5_810102603.ipynb) | Preprocessing, embedding, clustering, and visualization |

**`musicLyrics.csv` is required but is not included in this repository.** Obtain the assignment dataset and place it in `CA5/Code/`. The notebook expects a column named **`Lyric`** containing English lyrics. It removes missing and blank lyrics before processing.

## 🔄 Pipeline

1. **Clean:** lowercase text, remove punctuation, tokenize, remove English stop words, and apply WordNet lemmatization.
2. **Embed:** encode the cleaned lyrics with `SentenceTransformer('all-MiniLM-L6-v2')`.
3. **Cluster:** fit K-Means, agglomerative clustering, and DBSCAN on the embeddings.
4. **Evaluate:** calculate silhouette scores, excluding DBSCAN noise where a valid multi-cluster result exists.
5. **Inspect:** project embeddings to two dimensions and print sample lyrics from each group.
6. **Experiment:** fit additional clustering models on PCA-reduced data and compare their groupings.

## ⚙️ Experiment settings

| Experiment | Notebook settings |
| --- | --- |
| Elbow search | K-Means with `k=2` through `19` |
| Initial K-Means | `n_clusters=10`, `n_init=10`, `random_state=42` |
| Initial agglomerative model | `n_clusters=10`, default linkage |
| Initial DBSCAN | `eps=0.6`, `min_samples=5`, Euclidean distance |
| PCA | Two components |
| K-Means / agglomerative on PCA data | Three clusters |
| DBSCAN on PCA data | `eps=0.05`, `min_samples=400` |
| Later DBSCAN on original embeddings | `eps=0.7`, `min_samples=6`, displayed in PCA space |

These values describe the submitted experiments; they are not guaranteed optimal settings for another dataset.

## 🚀 Getting started

From the repository root:

```bash
python -m pip install jupyterlab pandas numpy matplotlib scikit-learn torch sentence-transformers nltk
cd CA5/Code
python -m jupyterlab AI_CA5_810102603.ipynb
```

After adding the dataset, replace the machine-specific Windows path in the CSV-loading cell with:

```python
df = pd.read_csv("musicLyrics.csv")
```

Run the cells in order. The notebook downloads the NLTK resources `punkt_tab`, `punkt`, `stopwords`, and `wordnet`. The sentence model also needs a download on first use, so an internet connection is required unless those resources are already cached.

## 📊 Outputs

The notebook produces an elbow curve, silhouette scores, PCA scatter plots, and lyric excerpts grouped by cluster. Comparing the excerpts helps assess whether numerical separation corresponds to meaningful themes.

## 📝 Notes on the submitted version

- Homogeneity is discussed in the assignment but not computed in the notebook. It requires reference class labels, unlike silhouette scoring.
- The hierarchical experiment uses the default linkage; the code does not perform the linkage comparison mentioned in its markdown.
- Sampling two lyrics with `.sample(2)` fails for clusters containing fewer than two rows. Check cluster size before running those inspection cells on another dataset.
- `plot_clusters` is redefined later with a different signature. Run the notebook sequentially, or restart the kernel before rerunning earlier plotting cells.
- The later DBSCAN experiment overwrites `cluster_dbscan`; previously printed silhouette scores describe the earlier fit.
- PCA-based clustering and projecting existing clusters onto PCA axes are different experiments. The notebook includes both, and their results should be interpreted separately.
