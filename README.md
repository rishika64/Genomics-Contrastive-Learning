# 🧬 Enhancing Gene–Disease Prediction using Contrastive Learning and Graph Neural Networks

This repository contains the code, data, and models used to train and evaluate a novel contrastive learning framework for predicting gene–disease associations by integrating **multi-omics data** (DNA, RNA, and protein) in a shared latent space.

---

## 🚀 Overview

Despite advances in genomics, many gene–disease relationships remain undiscovered due to the fragmented nature of biological data. Our model bridges this gap by:

- Integrating **DNA**, **RNA**, and **protein-level** features
- Using **contrastive learning** inspired by **CLIP** (Contrastive Language–Image Pretraining)
- Embedding gene and disease nodes in a **shared latent space**
- Leveraging **transformer-based Graph Neural Networks (GNNs)** for biological representation learning
- Validating against leading models: **HAN**, **LUPI-GNN**, and **MGREL**

The model achieves **AUPRC: 0.95** and **F1-score: 0.93**, outperforming state-of-the-art baselines and showing promising potential for **precision medicine** and **biomedical discovery**.

---

## 🧪 Datasets

We use the following datasets:

- **Gene–Disease Associations**: OMIM, DisGeNET, ClinVar
- **Gene–Gene Interactions**: HumanNet-FN
- **Disease Similarity**: OMIM TX/CS (TF-IDF + cosine similarity)
- **Gene Features**: RNA expression (GTEx, GWAS), DNA sequence features
- **Protein Features**: Protein-protein interaction networks (BioGRID)

The processed dataset includes:
- 15,675 genes
- 6,070 diseases
- 31,770 confirmed associations
- 733,836 gene–gene edges
- 645,945 disease–disease edges

> **Note:** Due to licensing restrictions, raw datasets are not distributed in this repo. Please download them from their respective sources and place them under `data/raw/`.

---

## 🧠 Methodology

### ⚙️ Model Architecture
- **Two-tower contrastive GNN** inspired by CLIP
- Each tower processes either **gene** or **disease** nodes
- Multi-layer **Transformer encoders** for long-range dependencies
- **Multi-omics integration** via separate encoders per modality
- InfoNCE loss to align positive gene–disease pairs and separate negatives

### 🔍 Negative Sampling Strategy
- Based on **cosine similarity** + **KMeans clustering**
- Ensures low similarity negatives, reduces false negatives

### 📊 Evaluation Metrics
- **AUPRC** (Area Under Precision-Recall Curve)
- **F1-Score**
- **Clustering Analysis** (UMAP/t-SNE of embedding space)
- **Ablation Study** on omics modality combinations (DNA, RNA, protein)

---

## 📈 Results

| Model      | AUPRC | F1-Score |
|------------|--------|----------|
| HAN        | 0.74   | 0.75     |
| LUPI-GNN   | 0.79   | 0.81     |
| MGREL      | 0.93   | 0.91     |
| **Ours**   | **0.95** | **0.93** |

- RNA+Protein was the most informative combination
- Latent space showed distinct **disease-related gene clusters**
- **Case study on GSK3B** revealed novel links with Alzheimer’s, Parkinson’s, and Schizophrenia

---

## 🧪 Case Study Example

The model was tested on **GSK3B** – a key regulatory kinase – and successfully predicted associations with:

- Alzheimer’s Disease
- Parkinson’s Disease
- Schizophrenia

These associations were previously underexplored, but backed by **literature evidence and clustering proximity** to known disease genes in the latent space.

---

## 🔧 Installation & Usage

### 🔐 Clone the repo
```bash
git clone https://github.com/rishika64/Genomics-Contrastive-Learning.git
cd Genomics-Contrastive-Learning
