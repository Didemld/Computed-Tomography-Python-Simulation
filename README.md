# CT Reconstruction & Beam Hardening Analysis (ASTRA-Toolbox)

This repository contains a Google Colab–oriented workflow to reproduce **beam hardening (BH)** artifacts and run baseline **3D CBCT** reconstructions with **ASTRA-Toolbox** on GPU. The notebook implements **FDK (FDK_CUDA)** and **iterative SIRT (SIRT3D_CUDA)**.

## ℹ️ Technical Challenge

The goal is to visualize BH artifacts (streaks, cupping) on a 512-view cone-beam dataset and to provide baseline reconstructions for further analysis. ASTRA-Toolbox is used as a TIGRE alternative and is set up inside Colab via **condacolab** (conda channels: `astra-toolbox`, `conda-forge`).

## 🛠️ Pipeline

1. **Environment (Colab, GPU):**  
   The Colab kernel is prepared with **condacolab**; packages installed: `astra-toolbox`, `imageio`, and `matplotlib`.

2. **Data Preparation:**  
   - Input: **512 PNG projections** named `Object_BH_Proj000.png` … `Object_BH_Proj511.png`.  
   - Place them under `/content/projections/projections_folder/` (for example, by uploading a `projections.zip` and unzipping to that path).  
   - Convert projections to line integrals via air normalization (`I0 = 99.9th percentile`) and `-log(I/I0)`.  
   - Save sinogram and angles as NumPy arrays (`/content/sino3d.npy`, `/content/angles.npy`).

   Data folder (example):
   https://drive.google.com/drive/folders/14ZjXgc9iCxmQyFoFudpBK0pK5CH--fkx?usp=drive_link

4. **Reconstruction:**  
   - **Geometry:** cone-beam with `DSO = 100 mm`, `DSD = 1500 mm`, detector pixel size `0.8 mm`.  
   - **Volume:** `512 × 512 × 512` voxels, physical extent `[-20, 20] mm` in all axes.  
   - **FDK_CUDA** (analytical) and **SIRT3D_CUDA** (iterative, 200 iters).

5. **Visualization:**  
   Axial / XZ / YZ cross-sections are saved as PNG. Display window: `[0.15 × min, 0.15 × max]`. Axis flips are applied to match the reference PDF orientation.

## 🚀 Running on Google Colab

- Open the notebook in **Google Colab** and select **GPU** (Runtime → Change runtime type → GPU).  
- Run cells sequentially: environment setup → data setup (place projections) → reconstruction (FDK, SIRT).  
- No local installation is required.

## 📊 Demonstration: FDK Baseline Results (Artifacted)

*X-axis (YZ plane), Y-axis (XZ plane), and Z-axis (Axial) cross-sections showing beam hardening artifacts.*

<img width="512" height="512" alt="FDK x-axis" src="https://github.com/user-attachments/assets/11a3f212-04f9-42c0-a4d2-7b72371bf9aa" />  
<img width="512" height="512" alt="FDK y-axis" src="https://github.com/user-attachments/assets/8fc18ba0-fed4-4ecc-8c5d-9854e1c2c067" />  
<img width="512" height="512" alt="FDK z-axis" src="https://github.com/user-attachments/assets/388b1eb5-f9c4-415d-a37c-e1594bef6875" />

## 👤 Contact

**Didem Doğan Başkaya**  
- LinkedIn: [`in/didemdoganbaskaya`](https://www.linkedin.com/in/didemdoganbaskaya)  
- GitHub: [`Didemld`](https://github.com/Didemld)
