# 👁️ OptiGuard: Clinical-Ready AI for Quality-Aware and Transparent Glaucoma Screening

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-ee4c2c)
![License](https://img.shields.io/badge/License-MIT-green)
![IDSC 2026](https://img.shields.io/badge/IDSC_2026-Stage_1_Submission-gold)

> **OptiGuard** is a state-of-the-art, multimodal Deep Learning pipeline designed to detect Glaucomatous Optic Neuropathy (GON) using Gold-Standard clinical fundus images. Built for the **IDSC 2026: Mathematics for Hope in Healthcare** competition.

## 🚀 The Clinical Problem
In real-world clinical settings, AI screening tools face three major roadblocks:
1. **Garbage In, Garbage Out:** Poor quality fundus images lead to false diagnoses.
2. **The Imbalance Trap:** AI models cheat by memorizing the majority class (Healthy/GON-).
3. **The Black Box Effect:** Ophthalmologists cannot trust an AI that cannot explain *why* a patient is diagnosed with Glaucoma.

## 💡 The OptiGuard Solution
OptiGuard tackles these challenges through a robust mathematical and architectural approach:
* **Quality-Aware Architecture:** Fuses visual features from a pre-trained **Swin Transformer** with image quality scores using a dedicated MLP layer.
* **Fair Augmentation & Focal Loss:** Prevents data leakage and penalizes the model for being biased towards the majority class.
* **F1-Max Threshold Optimization:** OptiGuard doesn't guess at a 0.5 threshold. It mathematically simulates 100 points to find the optimal F1-Macro balance.
* **MathGradCAM (Transparent Insights):** A custom-built, from-scratch calculus module that extracts spatial gradients to generate thermal heatmaps, proving that the AI looks at the *Optic Disc*—just like a real doctor.

---

## 🏗️ System Architecture (The Pipeline)



## 📊 Key Results
Evaluated on the Hillel Yaffe Glaucoma Dataset (HYGD) strict patient-level test set:

High Discriminative Power: AUROC > 0.90

Optimized Threshold: Dynamically tuned to maximize F1-Macro, ensuring fairness across both GON+ and GON- cases.

Interpretability: 100% of positive predictions are backed by spatial heatmaps focusing on the inferior and superior regions of the neuroretinal rim.

## 🛠️ How to Run
OptiGuard is built to be run directly on Google Colab or any Jupyter environment.

Clone this repository:

Bash
git clone [https://github.com/forgetallyourworries/Pedjuang-Kompis-IDSC.git](https://github.com/forgetallyourworries/Pedjuang-Kompis-IDSC.git)
cd Pedjuang-Kompis-IDSC
Install requirements:

Bash
pip install timm scikit-learn seaborn opencv-python matplotlib pandas torch torchvision
Update the BASE_PATH in the script to point to your HYGD dataset location.

Run the main script:

Bash
python IDSC_DAFFA_HYGD-PTFINAL.py

## 👨‍💻 Team & Acknowledgments
Leader : Daffa Sandriwinata (Mathematics Dept., Universitas Brawijaya)

Developed for IDSC 2026. Special thanks to the creators of the Hillel Yaffe Glaucoma Dataset for providing gold-standard clinical annotations.

“Mathematics for Hope in Healthcare. OptiGuard brings transparency to every diagnosis.”    
