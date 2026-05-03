YOLOv8‑Nano + SAHI for Small Object Detection on VisDrone

This repository contains the implementation and reproducibility artifacts for our group research project on small object detection in UAV imagery. The study evaluates zero‑shot COCO→VisDrone transfer using YOLOv8‑Nano, highlighting the limitations of baseline detection for pedestrians and bicycles. We integrate Slicing Aided Hyper Inference (SAHI) with tile‑level NMS to recover fine‑grained instances, achieving a +185.71% relative mAP improvement at the cost of ~12× reduced throughput (54.1 FPS → 4.2 FPS).

The repo includes:

Experimental data & configuration files

* Training curves, confusion matrices, and qualitative detection grids

* Ablation studies on tile size, overlap ratio, and postprocessing (WBF vs NMS)

* Reproducibility pipeline with scripts for replication and hardware‑specific tuning


** Key Contribution: A reproducible benchmark of YOLOv8‑Nano + SAHI for VisDrone, emphasizing the trade‑off between accuracy gains and real‑time deployment constraints.
