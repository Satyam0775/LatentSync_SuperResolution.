# 🎬 LatentSync – Super-Resolution Enhancement (GFPGAN + CodeFormer)

> **Enhanced Lip-Sync Output Using GFPGAN and CodeFormer for High-Quality Super-Resolution**

This repository is a **modified version of the LatentSync** project, enhanced to apply **face super-resolution** on generated lip-synced videos.  
The aim was to improve the **output facial region quality** using **GFPGAN** and **CodeFormer**, ensuring the upscaled part matches the original frame’s resolution.

---

## 📁 Google Drive (Models + Outputs)
👉 [**Google Drive Folder Link**](https://drive.google.com/drive/folders/1cPYHe6GNPAXR75eVMDJiEx8Hw1eIAP0T?usp=sharing)  
This folder contains:
- ✅ Pretrained model weights (GFPGAN & CodeFormer)  
- 🎥 Final enhanced output videos  
- 🧾 Supporting result files for evaluation  

---

## 🚀 Project Overview

LatentSync originally generates lipsynced video frames, but the generated **mouth region** often appears lower in quality compared to the original full frame.  
This enhancement pipeline fixes that issue by:

1. Detecting the **mouth ROI (Region of Interest)** in each frame  
2. Comparing its resolution ratio with the input frame  
3. Automatically applying **GFPGAN** or **CodeFormer** super-resolution only when needed  
4. Merging the enhanced ROI back into the full frame to produce **high-quality output videos**

---

## ⚙️ Key Improvements

| Feature | Description |
|----------|-------------|
| 🎯 **Selective Super-Resolution** | Applies SR only when the generated patch is lower quality |
| ⚡ **Dual Model Support** | Option to use either GFPGAN or CodeFormer via `--superres` argument |
| 🧠 **Automatic Ratio Check** | Dynamically computes frame-to-ROI resolution ratio |
| 🖼️ **Region-Specific Processing** | Enhances only the generated part, not the full image |
| 🧩 **Command Line Config** | Integrates smoothly with existing inference script (`inference.py`) |
| 🔁 **Fast Mode Support** | Optimized for reduced processing time with GPU acceleration |

---

## 🧩 Enhancement Flow

<img width="207" height="302" alt="image" src="https://github.com/user-attachments/assets/7197d32d-db5d-48df-9955-e46a31b4adf1" />



🧠 Model Overview
🟩 GFPGAN (Face Restoration)

Used for face super-resolution and detail recovery.

Model: GFPGANv1.4.pth

Path: GFPGAN/experiments/pretrained_models/

🟦 CodeFormer (Fidelity Restoration)

Used for balanced detail and fidelity reconstruction.

Model: codeformer.pth

Path: CodeFormer/weights/

🧰 Directory Structure
LatentSync_Fresh/
├── inference.py                   # Main enhanced inference script
├── GFPGAN/                        # GFPGAN submodule
│   └── experiments/pretrained_models/GFPGANv1.4.pth
├── CodeFormer/                    # CodeFormer submodule
│   ├── basicsr/
│   └── weights/codeformer.pth
├── output_GFPGAN_fast.mp4         # GFPGAN-enhanced video
├── output_CodeFormer_final.mp4    # CodeFormer-enhanced video
└── README.md                      # This file

🧩 Command Line Usage
🟢 Run with GFPGAN
python inference.py --input path/to/input.mp4 --output output_GFPGAN_fast.mp4 --superres GFPGAN

🔵 Run with CodeFormer
python inference.py --input path/to/input.mp4 --output output_CodeFormer_final.mp4 --superres CodeFormer


✅ Automatically detects low-quality mouth region
✅ Applies the selected super-resolution model only when necessary
✅ Produces a clean, high-resolution final output video

📦 Installation
git clone https://github.com/<your-username>/LatentSync_SuperRes.git
cd LatentSync_SuperRes

# Install dependencies
pip install -r requirements.txt


Ensure both GFPGAN and CodeFormer are cloned or placed inside your project folder.

🔗 Model Weights

Download pretrained weights manually or let the script auto-download them on first run.

Model	Download Link
GFPGANv1.4.pth	Download GFPGAN v1.4

CodeFormer.pth	Download CodeFormer
📁 Output Example

The enhanced videos generated using both models can be found here:
🎥 Google Drive Link for Models and Outputs

Model	Output Video	Description
GFPGAN	output_GFPGAN_fast.mp4	Fast facial super-resolution
CodeFormer	output_CodeFormer_final.mp4	Balanced detail + fidelity enhancement
🧩 Flow of Execution

Read Input Video

Extract ROI (Region around mouth area)

Compute Resolution Ratio

If ROI < Original Frame → Apply Super-Resolution

Merge ROI into Frame

Save Enhanced Video

⚡ Example Logs
🎬 Processing 1788 frames using GFPGAN (Fast Mode)...
🔹 Loading GFPGAN model (fast mode)...
✅ Fast enhanced video saved: output_GFPGAN_fast.mp4

🎬 Processing 1788 frames using CodeFormer (Fast Mode)...
🔹 Loading CodeFormer model (fast mode)...
✅ Enhanced video saved: output_CodeFormer_final.mp4

🧪 Verification Commands
# Verify CUDA and device
!nvidia-smi
!python -c "import torch; print('CUDA available:', torch.cuda.is_available())"

# Run final test
python inference.py --input sample.mp4 --output enhanced.mp4 --superres GFPGAN

🧭 Troubleshooting
Issue	Cause	Fix
ModuleNotFoundError: No module named 'basicsr.archs.arcface_arch'	Missing or broken import	Add safe import block in basicsr/__init__.py
ModuleNotFoundError: No module named 'basicsr.version'	Missing version file	Create version.py with __version__ = "1.0.0"
No module named 'ffmpeg'	Python package missing	pip install ffmpeg-python
Frame skipped due to resize.cpp error	Empty ROI frame	Add region validity checks before resizing
🧩 Summary of Achievements

✅ Integrated GFPGAN and CodeFormer into LatentSync
✅ Added --superres flag for dynamic model selection
✅ Implemented ROI-based enhancement logic
✅ Fixed missing imports and version errors in CodeFormer
✅ Produced enhanced outputs verified via GPU (Tesla T4)

🏁 Conclusion

This enhancement improves the visual fidelity of the lipsynced face while maintaining original frame consistency.
By selectively applying GFPGAN or CodeFormer, the pipeline ensures a balance between speed and detail restoration —
a modular design ready for future upgrades.

Author: Satyam Kumar
Project: LatentSync Super-Resolution Enhancement
