# Comprehensive Road Scene Understanding for Autonomous Driving

**Politecnico di Torino**  
*Fundamentals of Artificial Intelligence and Machine/Deep Learning (FAIMDL) — Academic Year 2025/2026*

**Authors:**
- **Virgile Gazeres** (s362611@studenti.polito.it)
- **Basile Fauconnier** (s361358@studenti.polito.it)
- **German Federico Ryjluk** (s364139@studenti.polito.it)

---

This repository contains the course project material for comprehensive road scene understanding for autonomous driving. The project studies how segmentation models behave when evaluated outside a closed-world setting, progressing from pixel-based (ERFNet) to mask-based (EoMT) architectures, with a strong focus on cross-domain segmentation and open-world anomaly detection.

## ⚠️ Evaluation Note for TAs

To simplify the evaluation process, **all Jupyter notebooks in the `notebooks/` directory have been pre-executed**. 
Cell outputs, mIoU computations, AuPRC metrics, and qualitative segmentation plots are fully preserved within the `.ipynb` files.

You **do not** need to download the gigabytes of datasets or model weights, nor do you need to rerun the execution loops to verify our results. You can inspect the methodology and the outputs directly by opening the notebooks.

## Repository Structure

```text
├── README.md
├── .gitignore
├── assignment/
│   └── Project 1 - Anomaly_Segmentation.pdf
├── figures/
├── notebooks/
│   ├── Task4-6.ipynb
│   ├── Task7.ipynb
│   └── Task8.ipynb
└── paper/
    └── 69_IS_s362611_s364139_sZZZZZZ_Gazeres_Ryjluk.pdf
```

## How to Navigate the Repository

- `paper/` contains the final PDF report summarizing the findings.
- `notebooks/` contains the cleaned experimental notebooks used for all tasks (cross-domain evaluation, fine-tuning, and anomaly baseline scoring).
- `figures/` is reserved for generated figures used by the report.

*(Note: We maintained the exact naming convention provided for datasets, including the `RoadObsticle21` folder name, to ensure compatibility with evaluation scripts).*

## Reproducibility Guide

We have engineered this repository to be "Plug & Play". All experimental notebooks use **relative paths**, meaning you do not have to modify any code cells to run them, provided the data is placed in the correct directories.

### 1. Download Artifacts

To successfully reproduce the results, you need to download specific artifacts for each task. The required scripts are available in the [Course Project GitHub Repository](https://github.com/AlessandroMarinai/MaskArchitectureAnomaly_CourseProject), while **all datasets and model weights** are hosted in this [Official Google Drive Folder](https://drive.google.com/drive/folders/1q2vHUzora2nP52fP50zmoQAykWuwoGav).

**For Task 4 & 5 (EoMT Evaluation & Fine-Tuning):**
- **Pretrained Weights:** Download the EoMT model weights (`eomt_cityscapes.bin` and `eomt_coco.bin`) from the Official Google Drive folder.
- **Datasets:** Download the original Cityscapes dataset (leftImg8bit and gtFine) from the Official Google Drive folder.

**For Task 7 (ERFNet Anomaly Baselines):**
- **Evaluation Scripts:** Download the entire `eval/` folder (containing `erfnet.py`, `transform.py`, etc.) from the Course GitHub repository.
- **Pretrained Weights:** Download `erfnet_pretrained.pth` from the `trained_models/` folder in the Course GitHub repository (or from the Official Google Drive if present).
- **Datasets:** Download `Anomaly_Validation_Datasets.zip` from the Official Google Drive folder.

**For Task 8 (EoMT Anomaly Evaluation & Temperature Scaling):**
- **Model Architecture:** Download the entire `eomt/` folder from the Course GitHub repository (it contains the `models/` Python package required to instantiate EoMT).
- **Datasets & Weights:** This task reuses the same anomaly datasets and EoMT weights downloaded for the previous tasks.

### 2. Google Colab Execution (Recommended)
Since deep learning inference requires significant compute power, most users will opt to run these notebooks on Google Colab. 

To avoid altering the clean relative paths in the code, you can use **symbolic links** to seamlessly map the expected repository folders directly to your Google Drive.

1. Upload the downloaded artifacts to a folder in your Google Drive, structuring them logically:
   ```text
   MyDrive/FAIMDL_Evaluation/
   ├── checkpoints/      <-- (Place .bin and .pth weights here)
   ├── data/             <-- (Place dataset zips/folders here)
   ├── eval/             <-- (Place erfnet.py, transform.py here)
   └── eomt/             <-- (Place the eomt/ source code folder here)
   ```
   *(Note: You can place the `.ipynb` notebooks anywhere you want, or just upload the entire repository folder. Google Colab always executes notebooks in its ephemeral `/content/` directory regardless of where the file is stored).*

2. Open any of the notebooks in Google Colab and create a new code cell at the very top.
3. Paste and run the following setup script, adjusting the `MY_DRIVE_BASE_PATH` variable to match your Drive folder:

```python
from google.colab import drive
import os

# 1. Mount your Google Drive
drive.mount('/content/drive')

# 2. Define the base path on YOUR Drive where you uploaded the folders
MY_DRIVE_BASE_PATH = "/content/drive/MyDrive/FAIMDL_Evaluation"

# 3. Create symbolic links to trick the notebook into seeing local relative directories
os.system(f"mkdir -p /content/data /content/checkpoints /content/eval /content/eomt")
os.system(f"ln -sf '{MY_DRIVE_BASE_PATH}/data/'* /content/data/")
os.system(f"ln -sf '{MY_DRIVE_BASE_PATH}/checkpoints/'* /content/checkpoints/")
os.system(f"ln -sf '{MY_DRIVE_BASE_PATH}/eval/'* /content/eval/")
os.system(f"ln -sf '{MY_DRIVE_BASE_PATH}/eomt/'* /content/eomt/")

print("Symlinks created! You can now 'Run All' without modifying the code.")
```
After executing this single cell, the rest of the notebook will run flawlessly using the unaltered relative paths!

### 3. Local Execution
If you prefer to run the code locally, simply place the downloaded files into their respective placeholders within this repository:

```text
.
├── checkpoints/
│   ├── eomt_cityscapes.bin
│   ├── eomt_coco.bin
│   └── erfnet_pretrained.pth
├── data/
│   ├── Anomaly_Validation_Datasets.zip
│   └── Cityscapes/
├── eomt/
│   ├── models/
│   └── ...
├── eval/
│   ├── erfnet.py
│   └── transform.py
```
Once the files are in place locally, open any notebook in the `notebooks/` folder and click **Run All**.
