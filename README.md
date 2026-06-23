# EE-584-Term-Project
================================================================================
TERM PROJECT: TENNIS BALL TRACKING & LOCALIZATION BENCHMARK (TRACKNET vs CV)
================================================================================

This document is prepared for the instructor/assistant evaluating the project 
to smoothly run the Jupyter Notebook files (TrackNet_Dataset1.ipynb 
and TrackNet_Dataset2.ipynb) in the Google Colab environment and 
verify the outputs.

--------------------------------------------------------------------------------
1. DATASET ACCESS AND GOOGLE DRIVE SETTINGS (CRITICAL STEP)
--------------------------------------------------------------------------------
The datasets used in the project are located inside the "EE584" folder, 
which is accessed via the provided Google Drive link:
https://drive.google.com/drive/folders/1_rBS6AxzZZnz2OKDOFVq8IrSNNor883e?usp=sharing

To ensure the notebook code cells automatically find the dataset paths 
(e.g., /content/drive/MyDrive/EE584/...), you MUST follow these exact steps 
before running the code:

METHOD A: Add the "EE584" Folder Shortcut to Your Drive (Recommended & Easiest)
1. Open the shared Google Drive link provided above.
2. Inside the shared directory, locate the folder named **"EE584"**.
3. Right-click on the "EE584" folder (or click the three vertical dots next to it).
4. Select "Organize" -> "Add shortcut" (or "Add shortcut to Drive").
5. Select "All locations" -> "My Drive" as the destination and click "Add".
   (IMPORTANT: The shortcut must be placed directly in the root of "My Drive" 
   and the shortcut's name must remain exactly "EE584").
6. When the notebook runs, approve the `drive.mount('/content/drive')` cell 
   permission. The code will seamlessly locate the datasets without any code 
   modifications.

METHOD B: Direct Upload (Alternative)
If Drive mapping is not preferred, you will need to download the datasets 
to your local machine and manually upload them into the Colab session's 
local storage ensuring the folder structure matches what the code expects, 
or modify the root paths within the notebook cells.

--------------------------------------------------------------------------------
2. COLAB PLATFORM VERSION DIFFERENCES AND SOLUTIONS
--------------------------------------------------------------------------------
This project was developed using the Colab Pro++ tier (High RAM, Advanced GPU 
architectures - A100/L4/V100). If the evaluator uses the standard/free Colab 
tier, potential limitations and their solutions are listed below:

* CUDA Out of Memory (VRAM Limitation):
  The standard tier provides a Tesla T4 GPU. If a VRAM insufficiency error is 
  encountered during the inference or testing phase of the TrackNet model, the 
  `batch_size` parameter in the code block should be reduced to a lower value 
  like 2 or 4.
  
* System RAM Limit (Crash/Runtime Disconnect):
  Loading all frames or feature matrices from the dataset into memory might 
  exceed the ~12.7 GB RAM limit provided by standard Colab. In this case, 
  instead of keeping all images in memory, dynamic data loaders reading from 
  the disk should remain active, or resolution scaling factors should be checked.

* Hardware Accelerator Selection:
  Before running the notebook, follow these steps from the top menu:
  "Runtime" -> "Change runtime type" -> Hardware accelerator: "T4 GPU"

--------------------------------------------------------------------------------
3. STEP-BY-STEP EXECUTION INSTRUCTIONS
--------------------------------------------------------------------------------
1. Open the .ipynb notebook files in the Google Colab environment.
2. From the "Runtime" menu, select "Run all".
3. Grant the access permission popup for the Google Drive integration 
   (`drive.mount`) located in the initial cells.
4. The code flow will automatically process the dataset; calculate the 
   localization metrics (Mean PE, Success@thr) for TrackNet (Deep Learning), 
   MOG2 + Kalman Filter, HSV Segmentation, CAMShift, and Lucas-Kanade Optical 
   Flow methods; and present summary tables as terminal outputs.

Youtube Link: https://www.youtube.com/watch?v=5mnEtxN5TVk
Paper Link: https://arxiv.org/abs/1907.03698

