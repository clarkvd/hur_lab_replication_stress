# Fluorescence Image Analysis Pipeline

This repository contains four Jupyter notebooks for automated segmentation and quantification of nuclei from multi-channel fluorescence microscopy images. Each notebook processes `.npy` image arrays, segments nuclei from a nuclear stain channel (DAPI or Sytox), and exports per-nucleus measurements to CSV.

---

## Notebooks

### `Image_1.ipynb` — RNAfish Signal Intensity Quantification
**Channels:** anti-47S, DAPI, IFNB1  
**Groups:** Mock 32H, GS 32H, Mock 48H, GS 48H  
Segments nuclei and quantifies mean/total RNAfish signal intensity per cell across all three channels. Transcriptional foci are detected using a watershed-based algorithm. Outputs `image1_results.csv`.

### `Image_2.ipynb` — IRF3 Nuclear Intensity Distribution
**Channels:** IRF3, DAPI  
**Groups:** Mock 24H, GS 24H, GS 32H, GS 48H  
Quantifies IRF3 nuclear intensity distribution by comparing mean IRF3 fluorescence inside each nucleus to a surrounding cytoplasmic ring. Classifies each nucleus as nuclear or non-nuclear. Outputs `image2_results.csv`.

### `Image_3.ipynb` — Micronuclei Frequency and IRF3 Nuclear Signal in MN+ vs MN− Cells
**Channels:** IRF3, Sytox  
**Groups:** Mock 32H Rep1, GS 32H Rep1, Mock 32H Rep2, GS 32H Rep2  
Segments nuclei from the Sytox channel and quantifies micronuclei frequency alongside IRF3 nuclear signal, stratifying cells by micronucleus status (MN+ vs MN−). Micronuclei are detected in the perinuclear region and filtered by morphology and IRF3 intensity. Outputs `image3_results.csv`.

### `Image_4.ipynb` — Cell Cycle Marker Intensity Quantification
**Channels:** IRF3, DAPI, Ki67  
**Groups:** Mock 32H, GS 32H  
Quantifies Ki67 cell cycle marker intensity per cell alongside IRF3 nuclear localization. Computes a per-nucleus Spearman correlation between DAPI and Ki67 intensities. Outputs `image4_results.csv`.

---

## Input Format

Each notebook reads `.npy` files from a specified input directory. Files must be 3-dimensional arrays of shape `(C, H, W)`, where `C` is the number of channels (as listed above), and `H`/`W` are the image height and width in pixels. Input folders follow the naming convention `imageN_npy` and outputs are written to `imageN_results.csv`.

## Output Format

Each notebook writes a CSV file containing one row per nucleus with per-nucleus measurements (intensity metrics, morphology, and classification labels) suitable for direct import into R or Python for statistical analysis.

## Dependencies

```
opencv-python
numpy
pandas
scikit-image
scipy
```

Install with:

```bash
pip install opencv-python numpy pandas scikit-image scipy
```
