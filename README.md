# Explainable CFRP AI

An explainable multimodal deep learning framework for **Carbon Fibre Reinforced Polymer (CFRP)** structural analysis, combining strength prediction, structural integrity assessment, damage segmentation, and Compression After Impact (CAI) strength estimation.

## Overview

Carbon Fibre Reinforced Polymer (CFRP) composites are widely used in aerospace, automotive, and structural applications because of their high specific strength and stiffness. However, their anisotropic and multiscale damage behaviour makes structural health monitoring and mechanical property prediction challenging.

This project presents a unified **physics-informed and explainable multimodal deep learning framework** consisting of four parallel branches:

1. **DNN Ensemble** for tensile and compressive strength regression
2. **Multi-Task MaterialsDNN** for tensile strength, fracture toughness, and structural integrity classification
3. **Hybrid Channel-Spatial Attention U-Net** for pixel-level CFRP damage segmentation
4. **MobileNetV2** for CAI strength prediction directly from RGB images

Explainability is integrated using **SHAP, LIME, and Grad-CAM**.

## Key Contributions

- Physics-informed target generation using a Rosen micro-buckling formulation
- Ensemble learning for CFRP strength regression
- Multi-task learning for structural integrity analysis
- Hybrid channel-spatial attention for damage segmentation
- Transfer learning for image-based CAI strength prediction
- Unified explainability using SHAP, LIME, and Grad-CAM
- Ablation studies evaluating the contribution of major architectural components

## Framework

The proposed framework contains four task-specific branches with a common explainability layer.

```text
                    CFRP Data
                       |
        +--------------+--------------+
        |              |              |
     Tabular         Images        CAI Images
        |              |              |
        v              v              v
  +-----------+  +------------+  +-------------+
  | Branch A  |  | Branch C   |  |  Branch D   |
  | DNN       |  | Attention  |  | MobileNetV2 |
  | Ensemble  |  | U-Net      |  | Regression  |
  +-----------+  +------------+  +-------------+
        |              |              |
 Strength Prediction  Damage       CAI Strength
                      Mask          Prediction
        |
        v
  +-------------------+
  |     Branch B      |
  | Multi-Task DNN    |
  +-------------------+
        |
  +-----+------+------+
  |            |      |
Tensile    Fracture  Integrity
Strength   Toughness Classification

        +-----------------------+
        | Explainability Layer  |
        | SHAP | LIME | GradCAM |
        +-----------------------+
