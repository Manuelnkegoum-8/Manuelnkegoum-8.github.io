# X-AnyLabeling: Multispectral Edition

<p align="center">
  <img src="https://raw.githubusercontent.com/CVHub520/X-AnyLabeling/main/anylabeling/resources/images/logo.png" width="150">
  <br>
  <i>Empowering AI labeling for Thermal, Multispectral Imagery.</i>
</p>


## 📖 Introduction

**X-AnyLabeling** is an open-source, AI-assisted data labeling tool designed for the modern computer vision workflow. Its core mission is to replace tedious manual clicking with "interactive intelligence." By integrating state-of-the-art models like the **Segment Anything Model (SAM)** and **YOLO**, it allows users to generate complex masks and bounding boxes with a single click, drastically reducing the time required to build massive datasets. This repository is a **specialized fork of X-AnyLabeling**, custom-engineered to bridge the gap between standard visual spectrum annotation and multi-modal sensing. Specifically, this version is optimized to handle **RGB+IR (Infrared) image pairs** for  data labeling.

### 🎯 Our Task: RGB+IR Dataset Annotation
Annotating datasets with both visible (RGB) and infrared (IR) data presents a unique challenge: features invisible in the RGB spectrum (such as heat signatures or objects in low-light environments) are often vivid in the IR spectrum.

**The goal of this project is to:**
* **Synchronize Multi-Modal Annotation:** Ensure that a bounding box or polygon drawn on the RGB layer perfectly aligns with the corresponding IR features.
* **Enable Cross-Spectrum Visualization:** Allow annotators to toggle between or overlay IR data to identify objects that the human eye might miss in standard light.
* **Build Fusion-Ready Data:** Generate unified ground-truth labels necessary for training **Multi-Spectral Fusion Models**, enabling robust performance in all-weather and 24/7 surveillance conditions.

## 🛠️ Installation

### 1. Environment Setup

You can use Python's built-in `venv` module to create virtual environments. Here are the commands for creating and activating environments under different configurations:

```bash
# CPU [Windows/Linux/macOS]
python3.10 -m venv venv-cpu
source venv-cpu/bin/activate  # Linux/macOS
# venv-cpu\Scripts\activate    # Windows

# CUDA 12.x [Windows/Linux]
python3.12 -m venv venv-cu12
source venv-cu12/bin/activate  # Linux
# venv-cu12\Scripts\activate    # Windows

# CUDA 11.x [Windows/Linux]
python3.11 -m venv venv-cu11
source venv-cu11/bin/activate  # Linux
# venv-cu11\Scripts\activate    # Windows
```

### 2. Installation 
**Step a.** Clone the repository.

```bash
git clone https://github.com/CVHub520/X-AnyLabeling.git
cd X-AnyLabeling
```

After cloning the repository, you can choose to install the dependencies in developer mode.

```bash
# CPU [Windows/Linux/macOS]
pip install -e .[cpu]

# CUDA 12.x is the default GPU option [Windows/Linux]
pip install -e .[gpu]

# CUDA 11.x [Windows/Linux]
pip install -e .[gpu-cu11]
```

Launch the App with the following command:.
```bash
xanylabeling
```


## 🚀 How to Use

This fork is powered by a custom-trained **YOLO-World X v2** model from Ultralytics, optimized for dual-input RGB+IR inference.


### 1. Selecting Your Model
We provide two specialized ONNX model variants depending on your hardware and precision requirements:

| Model Variant | Input Resolution | Best For |
| :--- | :--- | :--- |
| **MS YOLO-World (Standard)** | `640 x 640` | Real-time labeling and standard hardware. |
| **MS YOLO-World (High-Res)** | `1920 x 1088` | High-altitude drone imagery and small object detection. |

<p align="center">
  <video src="./loadmodel.mp4" width="100%" controls title="Batch Labeling Demo"></video>
</p>

### 2. Understanding Fusion Modes
When loading your model in the interface, you can toggle between two architectural fusion strategies:

* **Mid-Level Fusion (Feature Fusion):** * *How it works:* The model extracts features from RGB and IR separately and sum them to make the final detection.
* **Late-Level Fusion (Decision Fusion):**
    * *How it works:* The model processes the RGB and IR streams almost entirely independently, merging the results only at the final detection head.

---



### Labeling Process

Once the application is running and your custom **MS YOLO-World** model is loaded, follow these steps to begin the annotation process.

#### 1. Data Structure Requirements
To ensure the RGB and IR streams synchronize correctly, your dataset must follow this specific directory structure. The application matches pairs based on **identical filenames**.

```text
data/
├── rgb/
│   ├── image_001.png
│   ├── image_002.png
├── ir/
│   ├── image_001.png
│   ├── image_002.png

---



## 🛠️ Creating Your Own Customized Model

Want to train your own RGB+IR model? We follow the Ultralytics training pipeline with a modified 4-channel or dual-stream backbone. 

1.  **Prepare Dataset:** Ensure your images are paired and aligned.
2.  **Export to ONNX:** Use our export script to ensure the fusion layers are correctly serialized.
3.  **Integration:** Drop your `.onnx` and `.yaml` configuration into the `models/` folder.

> [!TIP]
> For advanced model architecture details, refer to the [Official Ultralytics YOLO-World Repository](https://github.com/ultralytics/ultralytics).

---
