# TunVeCTM — Topic Modeling of Tunisian Dialect on Social Media

Topic modeling pipeline for user-generated **Tunisian dialect** text (Arabizi and Arabic script) from social media, using **Contextualized Topic Models (CTM)** built on several combined embedding strategies.

This repo accompanies:
- 📝 *TunVeCTM: A Topic Modeling Approach of Tunisian Dialect on Social Media*
- 📝 *Topic Modeling of User-Generated Arabic on Social Media: A Systematic Literature Review*
- 🎓 Master's Thesis: *Topic Modeling of Tunisian Dialect on Social Media: A Contextual Approach using Combined Embeddings* — ISG Tunis, 2025

## 🧠 Overview

Tunisian dialect on social media is highly informal and code-switched (Arabic script, Latin script/Arabizi, French loanwords), which makes standard topic modeling tools a poor fit. This project addresses that by:

1. Applying dialect-specific preprocessing (custom stopword removal, character elongation normalization, Arabizi digit-to-letter conversion)
2. Generating and comparing **7 embedding strategies**, each feeding a Combined Topic Model (CombinedTM)
3. Evaluating each configuration with topic coherence metrics (**C_V**, **NPMI**) across a grid of topic counts

## 📁 Repository Structure

Each embedding combination has its **own self-contained notebook** — every notebook repeats the shared preprocessing steps so it can be run independently, without needing to run the others first.

```
tunvectm/
├── notebooks/
│   ├── 01_tunbert_baseline.ipynb    # TunBERT contextual embeddings (baseline)
│   ├── 02_tunbert_fasttext.ipynb    # TunBERT + FastText (subword robustness)
│   ├── 03_e5_tunbert.ipynb          # E5 (multilingual) + TunBERT
│   ├── 04_sbert_tunbert.ipynb       # SBERT (multilingual) + TunBERT
│   ├── 05_tunbert_doc2vec.ipynb     # TunBERT + Doc2Vec (corpus-trained)
│   ├── 06_arabertopic.ipynb         # AraBERT only — MSA baseline (no TunBERT)
│   └── 07_rober2vectm.ipynb         # XLM-RoBERTa (Arabic) + Doc2Vec
├── data/
│   └── README.md                    # where to put the corpus & stopwords file
├── requirements.txt
├── .gitignore
└── README.md
```

## 🔬 Embedding Combinations & Best Results

| Notebook | Combination | Best C_V | Best NPMI |
|---|---|---|---|
| 01 | TunBERT (baseline, no CTM training) | — | — |
| 02 | TunBERT + FastText | 0.544 | 0.583 |
| 03 | E5 + TunBERT | 0.553 (15 topics) | 0.675 (100 topics) |
| 04 | SBERT + TunBERT | **0.602** (6 topics) | 0.675 (100 topics) |
| 05 | TunBERT + Doc2Vec | **0.623** (6 topics) | 0.678 (95 topics) |
| 06 | AraBERTopic (MSA baseline) | 0.577 (100 topics) | **0.701** (100 topics) |
| 07 | Rober2vecTM (XLM-R + Doc2Vec) | 0.542 (7 topics, fixed) | 0.443 (7 topics, fixed) |

TunBERT + Doc2Vec (notebook 05) gives the strongest low-topic-count coherence; AraBERTopic (notebook 06) — despite not being dialect-specific — edges it out at high topic counts on both metrics. See each notebook's "Results" section for interpretation notes and caveats.

## ⚙️ Setup

```bash
git clone https://github.com/<your-username>/tunvectm.git
cd tunvectm
pip install -r requirements.txt
```

Add the required data files (see `data/README.md`), then open any notebook independently:

```bash
jupyter notebook notebooks/01_tunbert_baseline.ipynb
```

> Developed and tested on **Google Colab** with GPU acceleration — recommended for embedding generation and CTM training. Each notebook installs its own dependencies in its first cell.

## 📊 Evaluation

Each embedding combination (notebooks 02–07) is scored across a grid of topic counts (5 to 100, except notebook 07 which trains at a fixed 7 topics) using:
- **C_V Coherence** — semantic coherence based on word co-occurrence
- **NPMI** — normalized pointwise mutual information

## 🌐 Languages

Built for Tunisian Arabic dialect (Tunizi/Arabizi and Arabic script), with references to Modern Standard Arabic (AraBERT) and multilingual models as baselines.

## ✍️ Author

**Laila Lajili** — [LinkedIn](https://linkedin.com/in/laila-lajili) · laila.lagili20@gmail.com

## 📄 License

This project is shared for research and educational purposes. Add a license file (e.g. MIT) if you'd like to formally open-source it.
