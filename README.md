# CT Reconstruction & Beam Hardening Analysis (ASTRA-Toolbox)

This repository contains a Python-based computational imaging project to address a technical challenge on **"beam hardening" (BH) artifacts**.

The Jupyter Notebook implements the standard **Feldkamp-Davis-Kress (FDK)** reconstruction algorithm to reproduce and visualize the baseline artifacts (streaks and cupping) from a 3D Cone-Beam CT (CBCT) dataset.

## ℹ️ Technical Challenge

This implementation uses the **ASTRA-Toolbox** as an alternative to TIGRE toolbox, a powerful library for tomographic reconstruction, which required a custom `condacolab` environment setup to run in Colab.

## 🛠️ Tech Stack & Pipeline

This project is implemented in a Jupyter Notebook designed for Google Colab with a GPU.

1.  **Environment Setup:**
    * Uses **Condacolab** to install the **ASTRA-Toolbox** (`astra-toolbox`), `imageio`, and `gdown` (for data handling) from conda-forge channels.

2.  **Data Pre-processing:**
    * Uses `gdown` to automatically download the 2GB+ `projections.zip` data from Google Drive.
      https://drive.google.com/drive/folders/1ayBozT1QAVTLbs1M8UbZXeXOMtDUToyl?usp=drive_link
    * Loads 512 raw `.png` X-ray projections.
    * Performs air normalization (using 99.9th percentile as $I_0$).
    * Applies the logarithmic conversion (`-np.log(I/I0)`) to get linear attenuation (sinogram) data.

3.  **ASTRA Reconstruction (FDK):**
    * Defines the precise **cone-beam geometry** as specified in the ZEISS task PDF (DSO=100mm, DSD=1500mm, etc.).
    * Creates a 3D volume geometry (512x512x512).
    * Runs the reconstruction using ASTRA's GPU-accelerated FDK algorithm (`astra.astra_dict('FDK_CUDA')`).

4.  **Visualization:**
    * Saves the X, Y, and Z cross-sections from the reconstructed volume.
    * Applies the specific visualization windowing (`[0.15*min, 0.15*max]`) mentioned in the PDF to correctly display the beam hardening artifacts.

## 🚀 Getting Started

To run this simulation:

1.  Open the notebook in Google Colab and ensure you are assigned a **GPU runtime**.
2.  Run the first cell to install `condacolab`, `gdown`, and restart the kernel.
3.  Run the second cell to install `astra-toolbox`.
4.  Run the data loading cell (this will download the data via `gdown`) and the `run_fdk.py` cell to generate the reconstruction.

## 📊 Demonstration: FDK Baseline Results (Artifacted)

*X-axis (YZ plane), Y-axis (XZ plane), and Z-axis (Axial) cross-sections showing severe beam hardening artifacts.*

<img width="512" height="512" alt="FDK x-axis" src="https://github.com/user-attachments/assets/11a3f212-04f9-42c0-a4d2-7b72371bf9aa" />
<img width="512" height="512" alt="FDK y-axis" src="httpsG://github.com/user-attachments/assets/8fc18ba0-fed4-4ecc-8c5d-9854e1c2c067" />
<img width="512" height="512" alt="FDK z-axis" src="https:G//github.com/user-attachments/assets/388b1eb5-f9c4-415d-a37c-e1594bef6875" />

## 👤 Contact

**Didem Doğan Başkaya**
* **LinkedIn:** [`in/didemdoganbaskaya`](https://www.linkedin.com/in/didemdoganbaskaya)
* **GitHub:** [`Didemld`](https://github.com/Didemld)
