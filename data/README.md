# 📦 Dataset Documentation

This directory manages the 3D point cloud dataset used for training, evaluation, and phenotyping benchmarks.

---

## 🌾 Dataset Overview

- **Source:** Consumer smartphone scans (iPhone 11) using photogrammetry/LiDAR techniques.
- **Format:** Stanford Polygon format (.ply) containing 3D spatial coordinates \((X, Y, Z)\) and semantic labels.
- **Classes:**
  - Class 0: Pot & Background
  - Class 1: Rice Plant (*Oryza sativa*)

---

## 📥 Download Full Dataset

The full dataset is available on Kaggle:
- **Kaggle Link:** [Rice 3D Segmentation Dataset (Label_Pot_Plant)](https://www.kaggle.com/datasets/haquanghung/rice-3d-segmentation-dataset)

After downloading, extract the folder Label_Pot_Plant into this directory:

`	ext
data/
├── Label_Pot_Plant/
│   ├── C1.1_26410.ply
│   ├── C1.1_26416.ply
│   ├── C1.1_26423.ply
│   └── ...
└── sample/
    ├── sample_plant.ply      # Quick test sample: segmented plant point cloud
    └── sample_pot.ply        # Quick test sample: segmented pot point cloud
`

---

## 🔍 Data Pre-processing & Feature Engineering

1. **Surface Normal Estimation:** Local covariance analysis with \(k = 20\) nearest neighbors.
2. **Relative Elevation (\(\Delta Z\)):** Normalized height above ground/pot rim to provide spatial priors.
3. **Point Cloud Sampling:** Farthest Point Sampling (FPS) / Random subsampling to 4,096 points per chunk.
4. **Data Augmentation:**
   - Random azimuth rotation along the \(Z\)-axis (\([0, 2\pi]\)).
   - Coordinate jittering (\(\mathcal{N}(0, 0.01)\)) and anisotropic scaling (\([0.8, 1.2]\)).