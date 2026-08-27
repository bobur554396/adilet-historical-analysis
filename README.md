# Comparative & Historical Analysis of the Legal Codes of the Republic of Kazakhstan

Reproducible NLP + ML pipeline over the five major codes of Kazakhstan — Criminal (УК), Administrative Offenses (КоАП), Civil (ГК), Labor (ТК), and Tax (НК) — covering 3,062 current articles (631,280 tokens) and 563 historical versions (1996–2025).

Accompanies the manuscript submitted to *Вестник КазАТК*: "A Computational Framework for Comparative and Historical Analysis of the Legal Codes of the Republic of Kazakhstan."

## Notebooks

| # | Notebook | Purpose |
|---|----------|---------|
| 01 | `01_cross_code_comparative_analysis.ipynb` | Corpus statistics across the five codes |
| 02 | `02_cross_reference_network_analysis.ipynb` | Citation graph (within / cross-code) |
| 03 | `03_penalty_sanction_analysis.ipynb` | Regex + grammar penalty extraction (УК vs. КоАП) |
| 04 | `04_topic_modeling_comparison.ipynb` | LDA topics and cross-code Jaccard overlap |
| 05 | `05_ngram_collocation_analysis.ipynb` | Bigram / trigram analysis |
| 06 | `06_ml_classification_baseline.ipynb` | TF–IDF + LR / SVM / RF / NB classifiers |
| 07 | `07_embeddings_similarity.ipynb` | E5-multilingual embeddings, UMAP + HDBSCAN |
| 08 | `08_historical_overview.ipynb` | 563 historical versions, amendment timeline |
| 09 | `09_article_lifecycle.ipynb` | Added / excluded / updated / deleted events |
| 10 | `10_text_diff_analysis.ipynb` | Word-Jaccard severity of 8,225 modifications |
| 11 | `11_penalty_evolution.ipynb` | 685 penalty-value transitions over time |

Run notebooks in order. `01` → `07` operate on the current-version corpus; `08` → `11` operate on the historical-version corpus.

## Headline results

- **98.48 %** test accuracy — 5-class code classification (Linear SVM, TF–IDF 1–2-grams)
- **94.92 %** test accuracy — 3-class penalty-type classification (Random Forest)
- **12 clusters / 91.5 %** avg purity — HDBSCAN over E5 embeddings
- **6,436** citation edges, **92.0 %** intra-code
- **4,524** penalty records (current) · **685** transitions (historical)
- **86 %** of 8,225 text modifications are cosmetic or minor

## Data

Texts were collected from *adilet.zan.kz*. Article JSON carries hierarchical metadata, a paragraph list with link targets, and an amendment-history `notes` field. Cross-references are read from the hyperlinks embedded in the portal markup, not from regular expressions over the wording.

Each notebook writes its outputs to `output/<NN>/`. A compact subset of those files, the summary tables behind the numbers reported in the paper, is included here under `artifacts/<NN>/` (21 files, ~150 KB). Large binaries are left out of the repository: article embeddings (`.npy`), pickled penalty frames (`.pkl`), the 23 MB full penalty history, and the interactive UMAP page.

## Stack

Python · spaCy (`ru_core_news_sm`) · scikit-learn · `intfloat/multilingual-e5-base` · UMAP · HDBSCAN · NetworkX.
