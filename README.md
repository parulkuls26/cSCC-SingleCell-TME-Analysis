# Single-Cell RNA-seq Analysis of Cutaneous Squamous Cell Carcinoma (cSCC)

**Author:** Parul Kulshreshtha

A sequential single-cell RNA-seq analysis workflow integrating matched Normal skin and cutaneous squamous cell carcinoma (cSCC) samples, encompassing Harmony batch correction, cell type annotation, and tumour microenvironment characterisation.

---

## Introduction

Cutaneous squamous cell carcinoma (cSCC) is the second most common skin cancer and a malignancy of significant clinical concern due to its capacity for local invasion, perineural spread, and metastasis in immunocompromised individuals. Despite its relatively favourable prognosis in most cases, aggressive subtypes and the complexity of the tumour microenvironment (TME) represent major challenges for therapeutic intervention.

Single-cell RNA sequencing (scRNA-seq) has transformed our understanding of cSCC biology by resolving the transcriptional heterogeneity of individual cells within the tumour and its surrounding stroma. Landmark work by Ji et al. (2020) identified tumour-specific keratinocyte (TSK) populations expressing epithelial-mesenchymal transition (EMT) markers — including VIM, ITGA5, and MMP10 — with no counterpart in normal skin, alongside a profoundly immunosuppressive microenvironment characterised by exhausted T cells, regulatory T cells (Tregs), myeloid-derived suppressor cells (MDSCs), and immunoregulatory dendritic cells expressing PD-L1 and IDO1. Cancer-associated fibroblasts (CAFs) further contribute to this suppressive niche, with myCAF and iCAF subtypes playing distinct pro-invasive and inflammatory roles respectively.

This repository presents a complete downstream scRNA-seq analysis of matched Normal skin and cSCC patient samples (P2–P5), building on a previously completed preprocessing workflow. The analysis applies Harmony integration to correct for sample-level batch effects, followed by re-clustering, differential expression analysis, cell type annotation guided by the Ji et al. (2020) cSCC cellular framework, and comparative analysis of cell type composition between conditions.

---

## Repository Structure

```
.
├── data/
│   └── adata_no_integration.h5ad     # Preprocessed AnnData input (30,470 cells × 2,000 HVGs)
├── notebooks/
│   └── cSCC_Integration_Analysis.ipynb   # Main analysis notebook
├── outputs/
│   ├── figures/                      # UMAP plots, dot plots, feature plots, composition charts
│   └── tables/                       # Marker gene tables, cell type proportions
├── biological_context/
│   └── cell_type_annotation_guide.md # Marker gene reference and annotation rationale
├── README.md
└── requirements.txt
```

---

## Analysis Overview

This notebook addresses the following analytical questions, building on the preprocessed `adata_no_integration.h5ad` object. No preprocessing steps are repeated.

| Section | Description |
|---------|-------------|
| **Q2** | Harmony batch correction applied to PCA embeddings; impact on cell mixing and biological signal evaluated |
| **Q3** | Neighbourhood graph, UMAP, and Leiden clustering recomputed on Harmony-corrected embeddings; resolution selection |
| **Q4** | Side-by-side comparison of integrated vs non-integrated UMAPs; interpretation of batch vs biological variation |
| **Q5** | Differential expression analysis; cluster annotation using skin, immune, and cSCC-specific marker genes |
| **Q6** | Cell type composition compared between Normal and cSCC; immune subpopulation characterisation and functional interpretation |

---

## Data

| Property | Detail |
|----------|--------|
| Samples | 8 biological samples across 4 patients (P2–P5) |
| Design | Matched Normal skin and cSCC per patient |
| Input object | `adata_no_integration.h5ad` (30,470 cells × 2,000 HVGs) |
| Split samples | P3 and P4 cSCC concatenated from two technical files prior to loading |
| Batch variable | Patient ID (`P2`–`P5`) used for Harmony correction |

---

## Cell Types Annotated

| Compartment | Cell Types |
|-------------|-----------|
| **Epithelial** | Basal KCs, Suprabasal KCs, Active tumour KCs, Tumour-Specific Keratinocytes (TSKs) |
| **Stromal** | Fibroblasts, myCAFs, iCAFs, Endothelial cells, Melanocytes, Schwann/neural cells |
| **Immune — T cell** | CD4 T cells, CD8 T cells, Exhausted CD4/CD8 T cells, Regulatory T cells (Tregs) |
| **Immune — Myeloid** | Langerhans cells, cDC1 (CLEC9A+), cDC2 (CD1C+), pDCs, Macrophages, MDSCs, Mast cells |
| **Immune — Other** | B cells, Plasma cells |

---

## Requirements

```bash
pip install -r requirements.txt
```

Core dependencies:

```
scanpy
anndata
harmonypy
pandas
numpy
matplotlib
seaborn
leidenalg
python-igraph
```

---

## References

- Ji AL et al. Multimodal Analysis of Composition and Spatial Architecture in Human Squamous Cell Carcinoma. *Cell*. 2020;182(2):497–514.
- Wang et al. Multi-omics analysis unveils the role of cancer-associated fibroblasts in cutaneous squamous cell carcinoma. *Cancer Cell International*. 2025.
- Li X et al. Signatures of EMT, immunosuppression, and inflammation in primary and recurrent human cSCC at single-cell resolution. *Theranostics*. 2022;12(17):7532–7549.
- Elyada E et al. Cross-Species Single-Cell Analysis of Pancreatic Ductal Adenocarcinoma Reveals Antigen-Presenting CAFs. *Cancer Discov*. 2019;9(8):1102–1123.
- Villani AC et al. Single-cell RNA-seq reveals new types of human blood dendritic cells, monocytes, and progenitors. *Science*. 2017;356(6335):eaah4573.
- Zou DD et al. Single-cell sequencing highlights heterogeneity and malignant progression in actinic keratosis and cSCC. *eLife*. 2023;12:e85270.

---

## License

This repository is for academic and educational purposes. Please cite the original references and data sources when using or adapting this work.
