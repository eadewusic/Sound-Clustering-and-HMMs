# Sound Clustering, Dimensionality Reduction & HMMs on Unlabelled Sound Data

This project applies clustering techniques to a dataset of unlabeled sound recordings. The objective was to extract meaningful features, reduce the high dimensionality of the data, and apply clustering algorithms to discover potential groupings within the dataset.

I used **Mel Spectrogram** features for representation, followed by **dimensionality reduction techniques** like **PCA** and **t-SNE** for better visual interpretability. Finally, I applied and evaluated **K-Means** and **DBSCAN** clustering methods.

## Tasks Performed

### 1. Data Loading & Feature Extraction
- Loaded `.wav` files from the `unlabelled_sounds` dataset.
- Extracted **Mel Spectrogram** features using Librosa and reduced each file’s spectrogram to a 128-length feature vector (mean across time).
- Created a structured DataFrame containing filenames and features.

### 2. Preprocessing
- Standardized the feature set using `StandardScaler` for better clustering performance.
- Explored raw feature plots using pairplots — clusters were not visually separable in high-dimensional space.

### 3. Dimensionality Reduction Techniques
- Applied **PCA (Principal Component Analysis)**:
  - Reduced the dataset to 3 principal components.
  - Preserved global variance structure but did not yield clear cluster separation.
- Applied **t-SNE (t-Distributed Stochastic Neighbor Embedding)**:
  - Captured local structure and provided visually clearer separability.
  - Used for exploratory visual analysis.

### 4. Clustering Algorithms

#### K-Means Clustering
- Used **Elbow Method** and **Silhouette Score** to determine optimal number of clusters (`k = 2`).
- Performance:
  - Silhouette Score: ~0.23 (moderate separability)
  - Davies-Bouldin Index: ~1.63 (average separation)
  - Inertia: ~29 million (sum of distances to centroids)

#### DBSCAN Clustering
- Tuned `eps` and `min_samples` hyperparameters.
- Most points were labeled as noise (`-1`), and few clusters were formed.
- DBSCAN struggled due to uniform feature space density post-PCA.

## Evaluation & Comparison

**Metrics:**
- Silhouette Score
- Davies-Bouldin Index

| Method     | Silhouette Score | Davies-Bouldin Index | Observations |
|------------|------------------|-----------------------|--------------|
| K-Means    | ~0.23            | ~1.63                 | Formed moderate clusters |
| DBSCAN     | Low / Invalid    | N/A                   | Failed due to density-based assumptions |

**Analysis:**
- **PCA vs t-SNE**: t-SNE offered better visual insights but was not used for clustering due to non-linearity.
- **K-Means vs DBSCAN**: K-Means outperformed DBSCAN on this dataset.

## Key Insights

- **Dimensionality reduction is essential** when dealing with high-dimensional feature spaces like audio spectrograms.
- **K-Means** worked better due to the relatively globular nature of clusters in PCA space.
- **DBSCAN** is sensitive to density and may fail when clusters are not clearly dense or separated.

## Conclusion

K-Means with PCA provided the most compact and separable clusters. DBSCAN struggled with sparse density after PCA. Dimensionality reduction significantly improved clustering performance and interpretability.

## Project Structure

- `data/`: contains all `.wav` audio files
- `images/`: all visualizations (e.g., PCA/t-SNE clusters)
- `notebook/`: Full notebook with explanations, visualizations, and modular code
