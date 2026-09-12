# Cataract Detection with Transfer Learning

A leakage-controlled deep learning study for cataract screening using five ImageNet-pretrained convolutional neural networks, deployment-oriented latency analysis, TensorFlow Lite export, Android physical-device benchmarking, Grad-CAM inspection, and external ODIR-5K zero-shot stress testing.

This repository contains the final artifact package for the study: metrics, manifests, leakage audits, benchmark outputs, statistical tests, selected figures, deployment files, and reproducibility notes.

> Important: this repository supports retrospective research analysis only. It is not a clinical diagnostic product, not a regulated medical device, and not a substitute for professional medical evaluation.

---

## Study Snapshot

| Area | Summary |
|---|---|
| Task | Three-class image classification: Cataract, Normal, Not Eye |
| Internal test set | 2,587 locked held-out images |
| Clinical subset | 1,831 ocular images after excluding Not Eye |
| Models compared | MobileNetV2, DenseNet201, InceptionResNetV2, ResNet152V2, Xception |
| Selected deployment model | MobileNetV2 LastBlock float32 TensorFlow Lite |
| External stress test | ODIR-5K true zero-shot evaluation |
| Android device benchmark | Xiaomi 23053RN02A, Android 15, XNNPACK CPU, 4 threads |
| Main caution | Strong internal accuracy did not transfer to ODIR-5K fundus images |

---

## Visual Overview

The figure below is the graphical abstract for the study.

![Graphical abstract](figures/Graphical_Abstract.png)

More figures are available in [`figures/`](figures/) and selected Grad-CAM examples are available in [`gradcam/examples/`](gradcam/examples/).

---

## Dataset Sources and Availability

The internal three-class dataset described in the manuscript is based on a public Kaggle release and documented upstream sources. Raw source images are not redistributed in this repository.

| Dataset / Source | Role in this study | Link | Notes |
|---|---|---|---|
| Cataract Eye Dataset - 3-Class Mobile Screening | Curated internal three-class source release | https://www.kaggle.com/datasets/suyog17/cataracteyedata | 13,669 images: 4,514 Cataract, 5,154 Normal, 4,001 Not Eye. The Kaggle release records the license as Unknown. |
| K. B. Ojha Cataract Detection using CNN | Upstream source for Cataract and Normal classes | https://github.com/krishnabojha/Cataract_Detection-using-CNN | Used as the upstream ocular-image source in the curated release. |
| Indian Food Images Dataset | Traced source for most Not Eye images | https://www.kaggle.com/datasets/iamsouravbanerjee/indian-food-images-dataset | 4,000 of 4,001 Not Eye images were traced to this dataset. |
| ODIR-5K | External zero-shot stress test only | https://odir2019.grand-challenge.org/dataset/ | Not used for training, calibration, threshold selection, or model selection. Not redistributed here. |

Internal split counts recorded by the final manifest:

| Partition | Images |
|---|---:|
| Train | 8,845 |
| Validation | 2,178 |
| Test | 2,587 |
| Quarantine | 14 |

Users who need the raw images should download them from the original providers and follow the usage terms, licenses, and access conditions of each source. The files in this repository document the final split, evaluation outputs, audit results, deployment artifacts, and benchmark logs.

---
## Key Results

### Locked Three-Class Benchmark

| Model | Test N | Accuracy | Macro Recall | Macro F1 | Macro AUC |
|---|---:|---:|---:|---:|---:|
| MobileNetV2 | 2,587 | 99.30% | 0.9934 | 0.9934 | 0.9997 |
| DenseNet201 | 2,587 | 99.65% | 0.9968 | 0.9967 | 0.9998 |
| InceptionResNetV2 | 2,587 | 99.38% | 0.9943 | 0.9942 | 0.9996 |
| ResNet152V2 | 2,587 | 99.42% | 0.9945 | 0.9945 | 0.9995 |
| Xception | 2,587 | 99.15% | 0.9920 | 0.9920 | 0.9995 |

Source: [`benchmarks/locked_final_benchmark/MANUSCRIPT_FINAL_3Class_Percent.csv`](benchmarks/locked_final_benchmark/MANUSCRIPT_FINAL_3Class_Percent.csv)

### Cataract-vs-Normal Clinical Subset

| Model | Clinical N | Accuracy | Sensitivity | Specificity | AUC |
|---|---:|---:|---:|---:|---:|
| MobileNetV2 | 1,831 | 99.07% | 99.06% | 99.08% | 0.9991 |
| DenseNet201 | 1,831 | 99.51% | 99.77% | 99.28% | 0.9996 |
| InceptionResNetV2 | 1,831 | 99.13% | 99.53% | 98.77% | 0.9989 |
| ResNet152V2 | 1,831 | 99.18% | 99.18% | 99.18% | 0.9986 |
| Xception | 1,831 | 98.80% | 98.83% | 98.77% | 0.9985 |

Source: [`benchmarks/locked_final_benchmark/MANUSCRIPT_FINAL_Clinical_Percent.csv`](benchmarks/locked_final_benchmark/MANUSCRIPT_FINAL_Clinical_Percent.csv)

### Last-Block Fine-Tuning Sensitivity

| Model | Condition | Three-Class Accuracy | Clinical Accuracy | Sensitivity | Specificity | Clinical AUC |
|---|---|---:|---:|---:|---:|---:|
| MobileNetV2 | Frozen backbone | 99.30% | 99.07% | 99.06% | 99.08% | 0.9991 |
| MobileNetV2 | Last block unfrozen | 99.69% | 99.56% | 99.41% | 99.69% | 0.9999 |
| DenseNet201 | Frozen backbone | 99.65% | 99.51% | 99.77% | 99.28% | 0.9996 |
| DenseNet201 | Last block unfrozen | 99.77% | 99.67% | 99.77% | 99.59% | 0.9999 |

Source: [`benchmarks/fine_tuning_sensitivity/Reviewer_10_2_Final_Comparison.csv`](benchmarks/fine_tuning_sensitivity/Reviewer_10_2_Final_Comparison.csv)

---

## Deployment Benchmark

The selected deployment candidate is the MobileNetV2 LastBlock float32 TensorFlow Lite model.

| Item | Value |
|---|---|
| Model file | `MobileNetV2_LastBlock_float32.tflite` |
| Size | 10,400,328 bytes |
| SHA-256 | `E98067D7BC8550190B2455894C826E7477D2775D8141C15BF6B7CB81B53C37E6` |
| Android device | Xiaomi 23053RN02A |
| Android version | 15 / SDK 35 |
| Runtime | TensorFlow Lite Android Benchmark |
| Delegate | XNNPACK CPU |
| Threads | 4 |
| Timed runs | 100 |
| Mean latency | 25.9222 ms |
| Median latency | 21.151 ms |
| P95 latency | 65.175 ms |

Android evidence:

- [`latency/android/android_latency_summary.csv`](latency/android/android_latency_summary.csv)
- [`latency/android/MobileNetV2_REVIEWER_SUMMARY.txt`](latency/android/MobileNetV2_REVIEWER_SUMMARY.txt)
- [`latency/android/logs/MobileNetV2_latency_log.txt`](latency/android/logs/MobileNetV2_latency_log.txt)
- [`latency/android/logs/MobileNetV2_full_log.txt`](latency/android/logs/MobileNetV2_full_log.txt)

---

## External ODIR-5K Stress Test

ODIR-5K was used only as a true zero-shot external-domain stress test. It was not used for model training, calibration, threshold tuning, or model selection.

| Metric | Value |
|---|---:|
| External images | 3,265 |
| Distinct patients | 2,029 |
| Cataract images | 307 |
| Normal images | 2,958 |
| Accuracy | 9.40% |
| Sensitivity | 99.35% |
| Specificity | 0.068% |
| AUC | 0.3516 |
| Bootstrap replicates | 5,000 |

Source: [`odir_zeroshot/ODIR_True_ZeroShot_Summary.csv`](odir_zeroshot/ODIR_True_ZeroShot_Summary.csv)

This result is intentionally included because it demonstrates that strong internal performance does not guarantee cross-domain clinical generalization.

---

## Repository Map

| Folder | Contents |
|---|---|
| [`benchmarks/`](benchmarks/) | Locked benchmark metrics, fine-tuning sensitivity, statistical tests, clinical-only tables |
| [`data/`](data/) | Final split manifest and data notes |
| [`deployment/`](deployment/) | TensorFlow Lite models and deployment audit tables |
| [`environment/`](environment/) | Environment metadata |
| [`figures/`](figures/) | Manuscript figure PDFs |
| [`gradcam/`](gradcam/) | Grad-CAM outputs and selected examples |
| [`latency/`](latency/) | Tesla T4 and Android latency evidence |
| [`leakage_audit/`](leakage_audit/) | Duplicate and near-duplicate leakage audit outputs |
| [`model_cards/`](model_cards/) | Model and data cards |
| [`odir_zeroshot/`](odir_zeroshot/) | External ODIR-5K zero-shot evaluation outputs |

---

## Trace Manuscript Claims to Artifacts

Use [`PAPER_ARTIFACT_MAP.md`](PAPER_ARTIFACT_MAP.md) to map each major paper table or claim to its supporting file.

| Manuscript item | Supporting artifact |
|---|---|
| Locked split counts | `data/FINAL_split_manifest.csv` |
| Three-class benchmark | `benchmarks/locked_final_benchmark/MANUSCRIPT_FINAL_3Class_Percent.csv` |
| Clinical metrics | `benchmarks/locked_final_benchmark/MANUSCRIPT_FINAL_Clinical_Percent.csv` |
| Confusion matrices | `benchmarks/locked_final_benchmark/confusion_matrices/` |
| Pairwise tests | `benchmarks/statistical_tests/MANUSCRIPT_FINAL_Pairwise_Statistical_Tests.csv` |
| T4 latency | `latency/t4/Table_T4_latency_rebenchmark_100runs.csv` |
| Android latency | `latency/android/android_latency_summary.csv` |
| ODIR zero-shot | `odir_zeroshot/ODIR_True_ZeroShot_Summary.csv` |
| Deployment model | `deployment/tflite/MobileNetV2_LastBlock_float32.tflite` |

---

## Code Notebooks

The final research code notebooks are included in [`notebooks/`](notebooks/).

| Notebook group | Contents |
|---|---|
| [`notebooks/training_models/`](notebooks/training_models/) | Model-specific clean-split training notebooks for MobileNetV2, DenseNet201, InceptionResNetV2, ResNet152V2, and Xception. |
| [`notebooks/final_pipeline/`](notebooks/final_pipeline/) | Leakage control, independent verification, last-block fine-tuning, locked benchmark, statistical tests, Grad-CAM, ODIR zero-shot validation, TensorFlow Lite export, and deployment latency audit. |

These notebooks are provided as research code. Full reruns require access to the original datasets and may require path adjustments for the user's local or cloud environment.

---
## Reproducibility

The repository provides final artifacts and verification records. It does not rerun full training from raw image data.

See [`REPRODUCIBILITY.md`](REPRODUCIBILITY.md) for details on:

- what can be checked directly,
- what requires original image access,
- which files support each benchmark,
- known limitations of the dataset and external validation.

---

## Data and Rights Notice

Raw medical or third-party images are not redistributed here unless rights are explicitly clear. The repository provides split manifests, metrics, audit outputs, model artifacts, figures, and benchmark logs.

The repository license applies to code and documentation. It does not automatically grant rights to external datasets, medical images, pretrained model weights, or third-party benchmark datasets.

---

## Clinical Use Notice

This work is a research prototype artifact package. It does not establish:

- clinical deployment readiness,
- regulatory approval,
- prospective screening performance,
- patient-level independence,
- generalization across all devices, sites, or demographics,
- end-to-end mobile app latency including camera capture and preprocessing.

Prospective patient-level validation with device-diverse and site-diverse data is required before any clinical or regulated use.

---

## Authors

**Hasnain Haider**  
Email: hhnain1006@gmail.com

**Suyog Khanal**  
Email: countylover7@gmail.com

---

## License

Repository code and documentation are released under the MIT License unless otherwise stated.

See [`LICENSE`](LICENSE) for details.



