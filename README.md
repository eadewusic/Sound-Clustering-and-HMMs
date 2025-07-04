# Sound Clustering, Dimensionality Reduction & HMMs on Unlabelled Sound Data

This project applies clustering techniques to a dataset of unlabeled sound recordings. The objective was to extract meaningful features, reduce the high dimensionality of the data, and apply clustering algorithms to discover potential groupings within the dataset.

I used **Mel Spectrogram** features for representation, followed by **dimensionality reduction techniques** like **PCA** and **t-SNE** for better visual interpretability. Finally, I applied and evaluated **K-Means** and **DBSCAN** clustering methods.

## Tasks Performed

### 1. Data Loading & Feature Extraction
- Loaded `.wav` files from the `unlabelled_sounds` dataset.
- Extracted **Mel Spectrogram** features using Librosa and reduced each file’s spectrogram to a 128-length feature vector (mean across time), along with other spectral features (ZCR, Spectral Centroid, Rolloff).
- Created a structured DataFrame containing filenames and features.

### 2. Preprocessing
- Standardized the feature set using `StandardScaler` for better clustering performance.
- Explored raw feature plots using pairplots - clusters were not visually separable in high-dimensional space, highlighting the need for dimensionality reduction.

### 3. Dimensionality Reduction Techniques
- Applied **PCA (Principal Component Analysis)**:
  - Reduced the dataset to 3 principal components.
  - Preserved global variance structure but did not yield clear cluster separation visually.
- Applied **t-SNE (t-Distributed Stochastic Neighbor Embedding)**:
  - Captured local structure and provided visually clearer separability.
  - Used for exploratory visual analysis due to its effectiveness in revealing hidden cluster structures.

### 4. Clustering Algorithms

#### K-Means Clustering
- Used **Elbow Method** and **Silhouette Score** to determine optimal number of clusters (`k = 3`).
- Performance:
  - Silhouette Score: 0.1647 (lower separability)
  - Davies-Bouldin Index: 1.9167 (higher, indicating worse separation)
  - Inertia: 1041413.5147 (sum of squared distances to centroids)

#### DBSCAN Clustering
- Tuned `eps` and `min_samples` hyperparameters.
- Performance:
  - Silhouette Score: 0.4265 (significantly higher, indicating better separability)
  - Davies-Bouldin Index: 0.8918 (much lower, indicating better separation)
  - Formed 9 distinct, higher-quality clusters while also identifying a large portion of the data as noise (`-1`).

## Evaluation & Comparison

**Metrics:**
- Silhouette Score
- Davies-Bouldin Index
- Inertia (for K-Means)

| Method | Silhouette Score | Davies-Bouldin Index | Inertia (K-Means only) | Observations |
|---|---|---|---|---|
| K-Means | 0.1647 | 1.9167 | 1041413.5147 | Formed spherical clusters; moderate performance |
| DBSCAN | 0.4265 | 0.8918 | N/A | Formed 9 distinct, higher-quality clusters; identified noise |

**Analysis:**
- **PCA vs t-SNE**: t-SNE offered better visual insights by preserving local structures, making it more suitable for exploratory visual analysis compared to PCA which focused on global variance.
- **K-Means vs DBSCAN**: DBSCAN significantly outperformed K-Means on this dataset, as indicated by its higher Silhouette Score and much lower Davies-Bouldin Index. This suggests DBSCAN better identifies natural, dense groupings.

## Key Insights

- **Dimensionality reduction is essential** when dealing with high-dimensional feature spaces like audio spectrograms, improving interpretability and potentially clustering quality.
- **DBSCAN** proved more effective for this dataset, successfully identifying more natural and distinct groupings, and explicitly handling noise.
- **K-Means**, with its inherent assumption of forming spherical clusters and partitioning all data points, was less effective in discerning the underlying cluster structure for this data, leading to lower quality clusters.

## Conclusion

DBSCAN provided more compact and separable clusters, demonstrating its effectiveness for this dataset despite identifying a portion of the data as noise. Dimensionality reduction significantly improved clustering performance and interpretability, with t-SNE offering superior visual insights for cluster separability.

## Project Structure

- `data/`: contains all `.wav` audio files
- `images/`: all visualizations (e.g., PCA/t-SNE clusters)
- `notebook/`: Full notebook with explanations, visualizations, and modular code

## Part 2: Hidden Markov Model (HMM) Capstone Use Case

- Peruse the one-page PDF [here](https://drive.google.com/drive/folders/1PS7tw9MweZD22TX1H2XogSpWQ9a0mdE8?usp=drive_link).
