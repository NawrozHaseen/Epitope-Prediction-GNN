# Epitope Prediction Using Graph Neural Networks

> A graph neural network approach to B-cell conformational epitope prediction, comparing **GraphSAGE** and **GraphEPN** on the Epitope3D benchmark dataset, using ESM-2 embeddings, physicochemical properties, and DSSP-derived structural features with FocalLoss to handle severe class imbalance.

---

## 📄 Project Report

The full academic paper for this project is available here:

📥 **[Project Report (PDF)](https://drive.google.com/file/d/1j_GjFpsHXwpvVmkc7Ulb966BJ82kpyxa/view?usp=sharing)**

> *Epitope Prediction Using Graph Neural Networks* — Sadnan Sanim, Nahid Shahriar Rafi, Nawroz Haseen Tumul, Md. Mezbaul Habib Ullash — BRAC University

---

## 📁 Repository Structure
```
├── CSE437_EpitopePredictionUsingGNN.ipynb   # Main notebook (all model versions)
└── README.md
```

The notebook contains five sections, each as a self-contained model version:
- **GraphSAGE V1** — Initial GraphSAGE implementation
- **GraphSAGE V2** — ✅ Best GraphSAGE (recommended)
- **GraphEPN V1** — Initial GraphEPN implementation
- **GraphEPN V2** — Intermediate GraphEPN
- **GraphEPN V3** — ✅ Best GraphEPN (recommended)

---

## 🗂️ Dataset

This project uses the **Epitope3D** benchmark dataset for conformational B-cell epitope prediction.

**Dataset source:** [https://biosig.lab.uq.edu.au/epitope3d/data](https://biosig.lab.uq.edu.au/epitope3d/data)

From the Epitope3D data page, download the following files:

| File | Description |
|------|-------------|
| `epitope3d_dataset_180_Train.csv` | Training labels (180 proteins) |
| `epitope3d_dataset_20_Test.csv` | Test labels (20 proteins) |
| `epitope3d_epi_chain_PDB/` | PDB structure files for training set |
| `epitope3d_testing_PDB/` | PDB structure files for test set |

Each CSV maps a **PDB ID** to an **Epitope List** of residue-level annotations in the format `residueid_residuename_chain` (e.g., `10_VAL_A`). The PDB files provide the 3D atomic coordinates used to construct protein graphs.

---

## 🚀 How to Run

The notebook is designed to run on **Google Colab** with a GPU runtime. Follow the steps below.

### Step 1 — Download the Notebook

Download `CSE437_EpitopePredictionUsingGNN.ipynb` from this repository by clicking the file, then clicking the **⬇ Download raw file** button (top-right).

---

### Step 2 — Prepare the Dataset on Google Drive

The notebook reads all dataset files from your Google Drive. You need to upload them before running.

1. Download the four dataset files/folders from the [Epitope3D data page](https://biosig.lab.uq.edu.au/epitope3d/data)
2. Go to [Google Drive](https://drive.google.com) and create a folder called `437 proj` in the root of **My Drive**
3. Upload the following into that folder, preserving the names exactly:
   - `epitope3d_dataset_180_Train.csv`
   - `epitope3d_dataset_20_Test.csv`
   - `epitope3d_epi_chain_PDB/` (folder of training PDB files)
   - `epitope3d_testing_PDB/` (folder of test PDB files)

Your Drive structure should look like this:
```
My Drive/
└── 437 proj/
    ├── epitope3d_dataset_180_Train.csv
    ├── epitope3d_dataset_20_Test.csv
    ├── epitope3d_epi_chain_PDB/
    └── epitope3d_testing_PDB/
```

> ⚠️ The notebook expects files at exactly these paths. If you place them elsewhere, update the path variables at the top of each model section accordingly:
> ```python
> pdb_train_dir = "/content/drive/MyDrive/437 proj/epitope3d_epi_chain_PDB"
> pdb_test_dir  = "/content/drive/MyDrive/437 proj/epitope3d_testing_PDB"
> train_csv     = "/content/drive/MyDrive/437 proj/epitope3d_dataset_180_Train.csv"
> test_csv      = "/content/drive/MyDrive/437 proj/epitope3d_dataset_20_Test.csv"
> ```

---

### Step 3 — Upload the Notebook to Google Colab

1. Go to [Google Colab](https://colab.research.google.com)
2. Click **File → Upload notebook**
3. Select the `.ipynb` file you downloaded in Step 1

---

### Step 4 — Set Runtime to GPU

1. Go to **Runtime → Change runtime type**
2. Select **GPU** (T4 GPU is sufficient)
3. Click **Save**

> ⚠️ GPU is strongly recommended. ESM-2 embedding generation and GNN training are significantly slower on CPU.

---

### Step 5 — Mount Google Drive & Run

1. Run the first cell — it will prompt you to **mount Google Drive** and authorize access
2. Run the installation cells to install all required packages
3. Navigate to the model section you want to run (**GraphSAGE V2** or **GraphEPN V3** are recommended)
4. Run the cells **in order** from top to bottom within that section

> ⚠️ Each model section is self-contained. You do not need to run all sections — just mount Drive, install packages, then run your chosen model section.

---

## 📊 Results Summary

| Model | Accuracy | AUROC | F1-Score (Epitope) |
|-------|----------|-------|---------------------|
| GraphSAGE (Best) | 0.6685 | 0.6025 | 0.2128 |
| GraphEPN (Best) | 0.6590 | 0.5870 | 0.2209 |

GraphEPN achieves slightly higher epitope F1 (0.2209 vs 0.2128), while GraphSAGE achieves slightly higher overall AUROC (0.6025 vs 0.5870).

---

## 📦 Key Dependencies

All packages are installed automatically by the notebook. Key libraries include:

- `torch`, `torch_geometric` — GNN models (GraphSAGE, GraphEPN)
- `fair-esm` — ESM-2 protein language model embeddings
- `graphein` — Protein graph construction from PDB files
- `biopython`, `biotite` — Protein structure processing
- `scikit-learn` — Evaluation metrics
- `plotly`, `kaleido` — Visualization

---

## 📌 Notes

- The notebook may take a significant amount of time to run end-to-end due to ESM-2 embedding generation for each protein graph
- Each model section is independent — you can run just one without running the others
- All results are printed inline; loss convergence and ROC curve plots are generated at the end of each model section

---

## 👥 Authors

**Sadnan Sanim, Nahid Shahriar Rafi, Nawroz Haseen Tumul, Md. Mezbaul Habib Ullash**
BRAC University
Course: CSE437
