# 🔬 Cataract Detection Using Transfer Learning

![Python](https://img.shields.io/badge/Python-3.12-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.20-orange)
![License](https://img.shields.io/badge/License-MIT-green)
![Platform](https://img.shields.io/badge/Platform-Google%20Colab-yellow)
![Hardware](https://img.shields.io/badge/Hardware-T4%20GPU-red)

> A comparative study of five deep learning architectures for automated cataract detection using transfer learning, with rigorous single-image inference latency benchmarking.

---

## 📌 Project Overview

This project evaluates five state-of-the-art convolutional neural network architectures for classifying eye images into three categories:

- **Cataract** — eye affected by cataract
- **Normal** — healthy eye
- **Not Eye** — non-eye image

All models were fine-tuned using transfer learning on ImageNet pretrained weights and evaluated on accuracy, recall, F2-score, and single-image inference latency.

---

## 🧠 Models Evaluated

| Architecture | Parameters | Input Size | Model Size |
|---|---|---|---|
| MobileNetV2 | ~3.4M | 224×224 | 19.07 MB |
| Xception | ~22.9M | 224×224 | 86.99 MB |
| ResNet152V2 | ~60.4M | 224×224 | 231.14 MB |
| InceptionResNetV2 | ~55.8M | 224×224 | 214.79 MB |
| DenseNet201 | ~20M | 224×224 | 74.31 MB |

---

## 📊 Results

### Accuracy & Loss

| Architecture | Train Acc | Test Acc | Train Loss | Test Loss |
|---|---|---|---|---|
| MobileNetV2 | 0.9974 | 0.9969 | 0.0067 | 0.0101 |
| Xception | 0.9975 | 0.9933 | 0.0087 | 0.0183 |
| ResNet152V2 | 0.9983 | 0.9941 | 0.0739 | 0.0153 |
| InceptionResNetV2 | 0.9917 | 0.9808 | 0.0217 | 0.0570 |
| DenseNet201 | 0.9985 | 0.8774 | 0.0032 | 0.3022 |

### Latency Benchmark (Single-Image, 100 Runs, T4 GPU)

| Architecture | Mean (ms) | Std (ms) | P95 (ms) | CV% |
|---|---|---|---|---|
| **MobileNetV2** | **77.8** | **6.6** | **88.3** | **8.5** |
| Xception | 104.3 | 20.8 | 140.3 | 19.9 |
| ResNet152V2 | 106.8 | 21.0 | 145.8 | 19.7 |
| InceptionResNetV2 | 103.3 | 20.7 | 130.1 | 20.0 |
| DenseNet201 | 103.9 | 12.2 | 113.6 | 11.7 |

---

## 📈 Latency Distribution Plots

### Individual Distribution (Histogram + KDE)
![Individual Latency](results/plot1_individual.png)

### Mean ± Std Dev with P95 Markers
![Bar Chart](results/plot3_barchart.png)

---

## 🔬 Methodology

### Dataset
- **Train:** 8,896 images (3 classes)
- **Validation:** 2,221 images
- **Test:** 2,552 images

### Training Strategy
- Base models loaded with ImageNet weights
- Custom CNN head added on top
- Lower layers frozen, top layers fine-tuned
- 20 epochs with ModelCheckpoint (best val_accuracy saved)
- Adam optimizer (lr=0.0001), categorical crossentropy loss

### Latency Benchmarking
- Single image extracted from test set (batch_size=1)
- 10 warm-up runs to stabilize GPU memory
- 100 repeated inference runs using `time.perf_counter()`
- No I/O overhead — image pre-loaded into memory
- Metrics: Mean ± Std, Median (P50), P95, Min, Max, CV

---

## 🗂️ Repository Structure
├── notebooks/
│   ├── MobileNetV2_FineTune.ipynb
│   ├── DenseNet201.ipynb
│   ├── ResNet152V2.ipynb
│   ├── Xception_FineTune.ipynb
│   └── InceptionResNetV2.ipynb
├── results/
│   ├── plot1_individual.png
│   └── plot3_barchart.png
├── latency_data/
│   ├── latency_MobileNetV2.npy
│   ├── latency_DenseNet201.npy
│   ├── latency_ResNet152V2.npy
│   ├── latency_Xception.npy
│   └── latency_InceptionResNetV2.npy
├── LICENSE
└── README.md

---

## ⚙️ How to Run

**Step 1** — Open any `.ipynb` notebook in Google Colab

**Step 2** — Mount Google Drive and set correct paths

**Step 3** — Run cells 0–5 (mount, imports, paths, datagen, iterators)

**Step 4** — Skip training cells (models already saved as `.h5`)

**Step 5** — Run load_model, compile, evaluate, and latency cells

---

## 🏆 Key Finding

**MobileNetV2 is the best overall architecture** for cataract detection in terms of deployment efficiency:
- Fastest average latency: **77.8 ms**
- Lowest P95 latency: **88.3 ms** — most consistent
- Smallest model size: **19.07 MB**
- Highest test accuracy: **99.69%**

---

## 🛠️ Tech Stack

- Python 3.12
- TensorFlow 2.20
- Keras
- NumPy, Matplotlib, SciPy, Scikit-learn
- Google Colab T4 GPU

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Hasnain** — hhnain1006@gmail.com
