# Exploring Filter Bubbles in YouTube Recommendations

This mini-project investigates how YouTube’s recommender system organizes content starting from neutral seed queries.  
By analyzing diversity and overlap of recommended videos, the project highlights structural patterns that resemble *filter bubbles* — situations where users are exposed to narrow and repetitive content, limiting perspectives.

📄 [Mini-report PDF](Mini-Report_YouTube_Seed_Analysis.pdf)
The mini-report PDF is included for quick reference in portfolio submissions, providing a concise overview of methods, results, and key figures without requiring the notebook.

---

## Project Objective
- Collect videos for three neutral seeds: **healthy cooking**, **beginner guitar**, and **stretching exercises**.
- Build a simple similarity graph using TF-IDF (title + description) and cosine similarity.
- Cluster videos with KMeans to identify latent topics.
- Compute three main metrics:
  - **Diversity** (normalized entropy per seed)
  - **Overlap** (Jaccard between seeds, by video IDs)
  - **Entropy vs Step** (growth of diversity during exploration)
- Visualize results as graphs and charts.

---

## Connection to Filter Bubbles
This project serves as a lightweight prototype for auditing algorithmic *filter bubbles*.  
Our results illustrate the effect:
- *Healthy cooking* produced almost no diversity, forming a tightly closed bubble.  
- *Stretching exercises* showed broader variation.  
- Across seeds, overlap was **zero**, suggesting strong isolation between content domains.  

Even without personalization, these findings reveal how YouTube’s recommender can reinforce bounded information environments — a central concern in AI ethics and media governance.

---

## How to Run (Google Colab)

1. Open the notebook in **Google Colab**. [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Jaderfonseca/youtube-filter-bubbles/blob/main/pipeline_clean.ipynb)

2. Provide a valid **YouTube Data API v3** key:
```python
from getpass import getpass

API_KEY = getpass("Paste your YouTube API key (input is hidden): ").strip()
assert API_KEY, "Empty API_KEY"
- This project requires a valid **YouTube Data API v3 key**.  
You can create one in the [Google Cloud Console](https://console.cloud.google.com/) by enabling the YouTube Data API v3 under your project and generating an API key.
```

3. Run the notebook cells in order(**In Colab**):
   - Data collection (search + pool)
   - Text preprocessing
   - TF-IDF + similarity
   - Clustering
   - Metrics + plots  

All outputs (CSV + PNG) are automatically saved into the 'data/' and 'figures/' folders.

---

## Folder Structure
```

data/
 ├── raw/
 │   ├── videos_raw.csv
 │   └── edges_raw.csv
 ├── clean/
 │   ├── videos_clean.csv
 │   └── edges_clean.csv
 ├── processed/
 │   ├── videos_with_clusters.csv
 │   ├── cluster_seed_counts.csv
 │   ├── similarity_matrix.npy
 │   ├── tfidf_vectorizer.joblib
 │   ├── diversity_per_seed.csv
 │   ├── entropy_vs_step.csv
 │   └── jaccard_seeds.csv
figures/
 ├── graph_lcc.png
 ├── jaccard_seeds.png
 ├── diversity_per_seed.png
 └── entropy_vs_step.png
```

---

## Key Figures

- **Largest connected component** → `figures/graph_lcc.png`  
- **Jaccard similarity (video IDs)** → `figures/jaccard_seeds.png`  
- **Diversity by seed** → `figures/diversity_per_seed.png`  
- **Entropy vs Step** → `figures/entropy_vs_step.png`  

---

## ⚠️ Limitations

- Small scale: only 3 seed queries (~150 videos each).  
- Text-only features (title + description) were analyzed, without transcripts or engagement metrics.  
- Diversity and entropy metrics depend on sampling and API limits; results may vary across runs.  
- Jaccard similarity captures only video/channel overlap, not deeper thematic relationships.  
- Clustering (TF-IDF + KMeans) provides a coarse partition, useful for exploration but not production-level audits.  

---

## License
For academic/portfolio use only.
