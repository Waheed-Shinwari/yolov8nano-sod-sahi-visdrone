Optimizing Small Object Detection in UAV Imagery using SAHI and YOLOv8-Nano
============================================================================

This repository contains the implementation and results for the project **"Optimizing Small Object Detection in UAV Imagery using Slicing Aided Hyper Inference (SAHI) and YOLOv8-Nano."**

The project evaluates the trade-offs between detection accuracy and computational efficiency when applying inference-time tiling (SAHI) to lightweight object detection models in aerial surveillance contexts.

Key Features
------------
- Zero-Shot vs. Fine-Tuned Analysis: Evaluation of COCO-pretrained YOLOv8-Nano vs. a version fine-tuned for 100 epochs on the VisDrone dataset.  
- SAHI Integration: Comprehensive benchmarking of Slicing Aided Hyper Inference with varying tile sizes (480, 640, 800) and overlap ratios.  
- Post-Processing Comparison: Quantitative comparison between Standard Non-Maximum Suppression (NMS) and Weighted Box Fusion (WBF).  
- Ablation Studies: Extensive experiments on confidence thresholds (0.15 vs 0.25) and slice dimensions.  
- Per-Class Metrics: Detailed analysis of performance gains for specific classes (e.g., Pedestrians, Bicycles, Cars).  

Repository Structure
--------------------
```
├── ML_Proj_Finetuned_Yolo_ablation_per_class_analysis.ipynb  Main Colab Notebook
├── plots_and_visuals                                         
├── visdrone.yaml                                             Dataset configuration
├── ablation_master_results.csv                               Ablation study metrics
├── per_class_metrics_comparison.csv                          Per-class AP breakdown
├── results.csv                                               Baseline vs SAHI summary
├── args.yaml                                                 Training hyperparameters
├── LICENSE                                                   Apache License
└── README.md                                                 This file
```

Prerequisites
-------------
- Environment: Google Colab (Recommended) or a local machine with CUDA support.  
- Dataset: VisDrone2019-DET (Training and Validation splits).  
- Libraries:  
  - Python 3.9+  
  - ultralytics (YOLOv8)  
  - sahi (Slicing Aided Hyper Inference)  
  - ensemble-boxes (For WBF)  
  - pycocotools (Evaluation)  

Quick Start (Google Colab)
--------------------------
This project is designed to run out-of-the-box on Google Colab using a T4 GPU.

1. Setup & Installation  
   Open the notebook `ML_Proj_Finetuned_Yolo_ablation_per_class_analysis.ipynb`. The first cell will automatically install required dependencies and mount your Google Drive.  

   ```
   pip install -q ultralytics sahi ensemble-boxes pycocotools opencv-python tqdm
   ```

2. Dataset Preparation  
   - Download VisDrone2019-DET-train.zip and VisDrone2019-DET-val.zip.  
   - Upload these ZIP files to the root of your Google Drive.  
   - Run the "Mount Drive & Extract Dataset" cell in the notebook. It will automatically create the correct directory structure (`images/` and `labels/`).  

3. Training (Optional)  
   If you wish to reproduce the fine-tuned weights, run the training cell.  
   - Model: YOLOv8-Nano  
   - Epochs: 100  
   - Image Size: 640  
   - Batch Size: 16  

   Note: The notebook is pre-configured to evaluate using the fine-tuned weights located in the `/content/drive/MyDrive/Yolov8_VisDrone_Trained/` path.  

4. Inference & Ablation Study  
   Run the main inference loop. This cell iterates through all ablation configurations (Tile sizes: 480/640/800, Overlaps, Post-processing methods) and saves the metrics to CSV files.  

Key Results
-----------
| Configuration | Tile Size | Post-Process | mAP@0.5:0.95 | mAP@0.5 | FPS | AP_small |
|---------------|-----------|--------------|--------------|---------|-----|----------|
| Tile 640 / NMS | 640 | NMS | 21.01 | 35.07 | 4.5 | 13.65 |
| Tile 640 / WBF | 640 | WBF | 21.01 | 35.07 | 4.5 | 13.65 |
| Tile 480 / NMS | 480 | NMS | 21.12 | 35.64 | 4.1 | 15.05 |
| Tile 800 / NMS | 800 | NMS | 20.59 | 33.53 | 6.8 | 12.28 |
| Low Conf (0.15)| 640 | NMS | 21.85 | 37.37 | 4.1 | 14.56 |

Findings
--------
1. Accuracy Peak: Tile size 480 yields the highest mAP (21.12%) and best small object detection (AP_small = 15.05%).  
2. Speed Peak: Tile size 800 is the fastest (6.8 FPS) but suffers in accuracy.  
3. WBF vs NMS: Weighted Box Fusion (WBF) did not provide significant gains over standard NMS in this specific SAHI implementation.  
4. Confidence Threshold: Lowering confidence to 0.15 improved Recall and mAP@0.5 but slightly reduced precision.  

Citations & References
----------------------
If you use this code for your research, please cite the following works:  
- YOLOv8: Jocher, G., et al. "YOLOv8 by Ultralytics." (2023).  
- SAHI: Akyon, F. C., et al. "Slicing aided hyper inference and fine-tuning for small object detection." (2022).  
- WBF: Solovyev, R., et al. "Weighted boxes fusion: improving ensemble of object detection models." (2021).  
- VisDrone: Zhu, P., et al. "Detection and tracking meet drones challenge." (2022).  

License
-------
This project is licensed under the MIT License. See the LICENSE file for details.  

Developed for: **National University of Sciences & Technology (NUST)'s Machine Learning Course Project**  
Contact:  https://github.com/Waheed-Shinwari
