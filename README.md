# TunVeCTM — Topic Modeling of Tunisian Dialect on Social Media

Topic modeling pipeline for user-generated **Tunisian dialect** text (Arabizi and Arabic script) from social media, using **Contextualized Topic Models (CTM)** built on several combined embedding strategies.

This repo accompanies:
- 📝 *TunVeCTM: A Topic Modeling Approach of Tunisian Dialect on Social Media*
- 📝 *Topic Modeling of User-Generated Arabic on Social Media: A Systematic Literature Review*
- 🎓 Master's Thesis: *Topic Modeling of Tunisian Dialect on Social Media: A Contextual Approach using Combined Embeddings* — ISG Tunis, 2025

## 🧠 Overview

Tunisian dialect on social media is highly informal and code-switched (Arabic script, Latin script/Arabizi, French loanwords), which makes standard topic modeling tools a poor fit. This project addresses that by:

1. Applying dialect-specific preprocessing (custom stopword removal, character elongation normalization, Arabizi digit-to-letter conversion)
2. Generating and comparing several embedding strategies as input to a **Combined Topic Model (CombinedTM)**
3. Evaluating each configuration with topic coherence metrics (**C_V**, **NPMI**) across a grid of topic counts

## 🔬 Embedding Combinations Benchmarked

| Combination | Description |
|---|---|
| TunBERT | Baseline contextual embeddings |
| TunBERT + FastText | Contextual + subword embeddings |
| E5 + TunBERT | Multilingual E5 sentence embeddings + TunBERT |
| SBERT + TunBERT | Multilingual SBERT + TunBERT |
| TunBERT + Doc2Vec | Contextual + document-level embeddings |
| AraBERTopic | AraBERT-based topic modeling baseline |
| Rober2vecTM | XLM-RoBERTa (Arabic fine-tuned) + Doc2Vec |

## 📁 Repository Structure

```
tunvectm/
├── tunvectm_cleaned.ipynb   # Main notebook: preprocessing, embeddings, CTM, evaluation
├── data/
│   └── README.md            # Instructions for placing the corpus & stopwords file
├── requirements.txt
├── .gitignore
└── README.md
```

## ⚙️ Setup

```bash
git clone https://github.com/<your-username>/tunvectm.git
cd tunvectm
pip install -r requirements.txt
```

Then add the required data files (see `data/README.md`) and open the notebook:

```bash
jupyter notebook tunvectm_cleaned.ipynb
```

> Developed and tested on **Google Colab** with GPU acceleration — recommended for embedding generation and CTM training.

## 📊 Evaluation

Each embedding combination is scored across a grid of topic counts (5 to 100) using:
- **C_V Coherence** — semantic coherence based on word co-occurrence
- **NPMI** — normalized pointwise mutual information

## 🌐 Languages

Built for Tunisian Arabic dialect (Tunizi/Arabizi and Arabic script), with references to Modern Standard Arabic (AraBERT) and multilingual models as baselines.

## ✍️ Author

**Laila Lajili** — [LinkedIn](https://linkedin.com/in/laila-lajili) · laila.lagili20@gmail.com

## 📄 License

This project is shared for research and educational purposes. Add a license file (e.g. MIT) if you'd like to formally open-source it.
