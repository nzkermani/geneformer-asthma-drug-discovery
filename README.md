# 📦 Geneformer-Based Drug Discovery for Asthma

This project applies a fine-tuned **Geneformer** model to prioritize candidate drugs for asthma using bulk RNA-seq data. The method leverages distributed gene expression embeddings to compare patient disease states with drug-induced transcriptomic signatures.

---

## 🌟 Objectives
- Fine-tune **Geneformer** on asthma phenotypes using bulk RNA-seq.
- Encode patient samples and drug profiles into embedding space.
- Rank drugs by their ability to shift patient embeddings toward a healthy or remission-like reference.

---

## 🧬 Input Data
- **Patient Data:** Bulk RNA-seq from asthmatic patients with clinical labels (e.g., FeNO, eosinophils, responder status).
- **Reference:** Healthy controls or remission cases used to define a target embedding.
- **Drug Profiles:** Drug-induced gene expression from LINCS/CMap (e.g., L1000).

---

## 🧠 Method Summary

### Step 1: Geneformer Fine-Tuning
- Load pretrained Geneformer model.
- Convert bulk RNA-seq into pseudo-cell format (top-N expressed genes).
- Fine-tune model on asthma clinical outcomes.

### Step 2: Embedding Generation
- Use the fine-tuned model to extract embeddings for each asthma patient.
- Encode drug-induced profiles similarly.
- Compute target embedding (e.g., mean of healthy or responder group).

### Step 3: Drug Ranking by Embedding Shift
- For each drug:
    - Compute cosine distance between asthma and reference embedding.
    - Compute cosine distance between drug and reference embedding.
    - Calculate shift score = pre-drug distance – post-drug distance.
- Rank drugs by mean positive shift across patients.

---

## 📊 Visualizations
- UMAP of patient embeddings with and without drug perturbations
- Heatmap of drug shift scores across patients
- Top-10 drug ranking bar plot

---

## 📁 Folder Structure
```
├── data/
│   ├── asthma_bulk_expression.csv
│   ├── drug_profiles_lincs.csv
│   └── metadata.csv
├── notebooks/
│   ├── 01_finetune_geneformer.ipynb
│   ├── 02_generate_embeddings.ipynb
│   └── 03_rank_drugs_by_shift.ipynb
├── models/
│   └── geneformer_finetuned.pt
├── results/
│   └── top_drugs.csv
├── README.md
└── requirements.txt
```

---

## 🔧 Requirements
```bash
transformers>=4.38
numpy
pandas
scikit-learn
matplotlib
seaborn
torch
```

---

## 📌 Citation
Based on: Theodoris et al., *Nature*, 2023 and NVIDIA’s Geneformer implementation.

---

## ✨ License
MIT License
# geneformer-asthma-drug-discovery
