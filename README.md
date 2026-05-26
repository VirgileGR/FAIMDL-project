# Open-World Anomaly Segmentation for Autonomous Driving

This repository contains the course project material for anomaly segmentation in autonomous driving. The project studies how segmentation models behave when evaluated outside a closed-world setting, with a focus on cross-domain segmentation and anomaly detection.

## Repository Structure

```text
.
├── README.md
├── assignment/
│   └── Project 1 - Anomaly_Segmentation.pdf
├── figures/
├── notebooks/
│   ├── Project_Image_Segmentation.ipynb
│   └── Task7_Pixel_Baselines.ipynb
└── paper/
    └── paper.tex
```

## How to Navigate the Repository

- `paper/` contains the LaTeX report.
- `notebooks/` contains the experimental notebooks used for the completed tasks.
- `figures/` is reserved for generated figures used by the report.
- `assignment/` contains the original project specification.

## Current Experimental Material

`notebooks/Project_Image_Segmentation.ipynb` contains the cross-domain segmentation work:

- loading EoMT Cityscapes and EoMT COCO checkpoints;
- qualitative comparison on Cityscapes validation images;
- deterministic COCO-to-Cityscapes label mapping;
- Cityscapes validation mIoU evaluation;
- preliminary EoMT-COCO fine-tuning code.

`notebooks/Task7_Pixel_Baselines.ipynb` contains the ERFNet pixel-based anomaly baseline:

- MSP anomaly score;
- MaxLogit anomaly score;
- maximum entropy anomaly score;
- AuPRC and FPR95 evaluation on the anomaly validation datasets.

## Datasets and Checkpoints

Large datasets, model checkpoints, and external baseline code are not included in this lightweight repository. The notebooks currently preserve the original Colab paths used during development; before rerunning the experiments, adapt those paths to your local environment.

The intended local layout for data and checkpoints is:

```text
.
├── checkpoints/
│   ├── eomt_cityscapes.bin
│   ├── eomt_coco.bin
│   ├── eomt_finetuned.bin
│   └── erfnet_pretrained.pth
└── data/
    ├── Cityscapes/
    └── Validation_Dataset/
        ├── RoadAnomaly21/
        ├── RoadObsticle21/
        ├── FS_LostFound_full/
        ├── fs_static/
        └── RoadAnomaly/
```

`data/Cityscapes/` should contain the Cityscapes structure expected by `torchvision.datasets.Cityscapes`, including `leftImg8bit/` and `gtFine/`.

`data/Validation_Dataset/` should contain the anomaly validation datasets used by the ERFNet baseline notebook. Each dataset folder is expected to contain:

```text
<dataset_name>/
├── images/
└── labels_masks/
```

The baseline repository used for EoMT, ERFNet, and evaluation utilities should be downloaded separately from the course-provided GitHub repository when experiments need to be rerun from scratch.
