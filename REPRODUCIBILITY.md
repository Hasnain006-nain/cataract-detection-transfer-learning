# Reproducibility Notes

This repository is a curated artifact package for the cataract detection transfer learning study. It is designed to make the final reported results traceable to concrete files.

---

## What Can Be Checked Directly

The following items can be verified from files in this repository:

| Item | Location |
|---|---|
| Final split membership and class counts | `data/FINAL_split_manifest.csv` |
| Leakage audit status | `leakage_audit/FINAL_phase7_summary.json` |
| Three-class benchmark metrics | `benchmarks/locked_final_benchmark/MANUSCRIPT_FINAL_3Class_Percent.csv` |
| Clinical Cataract-vs-Normal metrics | `benchmarks/locked_final_benchmark/MANUSCRIPT_FINAL_Clinical_Percent.csv` |
| Confusion matrices | `benchmarks/locked_final_benchmark/confusion_matrices/` |
| McNemar and DeLong pairwise tests | `benchmarks/statistical_tests/` |
| Last-block fine-tuning sensitivity | `benchmarks/fine_tuning_sensitivity/Reviewer_10_2_Final_Comparison.csv` |
| Tesla T4 latency | `latency/t4/Table_T4_latency_rebenchmark_100runs.csv` |
| Android physical-device latency | `latency/android/` |
| TensorFlow Lite export and parity | `deployment/deployment_tables/` |
| ODIR-5K zero-shot evaluation | `odir_zeroshot/ODIR_True_ZeroShot_Summary.csv` |
| Grad-CAM inspection outputs | `gradcam/` |

---

## What Requires Original Data or Compute

The following cannot be fully rerun from this repository alone:

- complete model training from raw images,
- raw image preprocessing from the original upstream collections,
- duplicate-family reconstruction from original image files,
- full external ODIR file matching from source image folders,
- prospective clinical validation.

This repository intentionally stores final manifests, metrics, audit outputs, deployment artifacts, and benchmark logs rather than redistributing all source images.

---

## Environment

The final experiments used the environment summarized in:

```text
environment/environment.json
requirements.txt
```

Core package versions:

| Package | Version |
|---|---|
| Python | 3.12.x |
| TensorFlow | 2.20.0 |
| Keras | 3.13.2 |
| NumPy | 2.0.2 |
| pandas | 2.2.2 |
| scikit-learn | 1.6.1 |
| SciPy | 1.16.3 |
| Matplotlib | 3.10.0 |

---

## Android Benchmark Reproducibility

The Android benchmark evidence is stored in:

```text
latency/android/
```

Important files:

| File | Purpose |
|---|---|
| `android_latency_summary.csv` | Clean one-row summary of the physical-device benchmark |
| `MobileNetV2_FINAL_RESULT.txt` | Extracted final benchmark output |
| `MobileNetV2_REVIEWER_SUMMARY.txt` | Human-readable benchmark summary |
| `logs/MobileNetV2_latency_log.txt` | Focused logcat output |
| `logs/MobileNetV2_full_log.txt` | Full logcat output |
| `model_sha256.txt` | Model identity hash |
| `benchmark_apk_sha256.txt` | Benchmark APK identity hash |
| `device_info.txt` | Device and battery/thermal information |

Protocol summary:

| Setting | Value |
|---|---|
| Device | Xiaomi 23053RN02A |
| Android | 15 / SDK 35 |
| Runtime | TensorFlow Lite Android Benchmark |
| Delegate | XNNPACK CPU |
| Threads | 4 |
| Warmup runs | 10 |
| Timed runs | 100 |
| Input | Randomized benchmark tensor input |
| Scope | Model invocation only |

---

## Source Archive Hashes

The source archives used to assemble this repository are recorded in:

```text
source_hashes.json
```

This allows the artifact package to be traced back to the exact ZIP files used during assembly.

---

## Limitations

- Patient identifiers are unavailable for the upstream ocular collection.
- Exact and near-duplicate leakage controls reduce image-level leakage risk but do not prove patient-level independence.
- ODIR-5K is deliberately cross-domain and shows severe generalization failure.
- Android timing measures model invocation only, not camera capture, preprocessing, UI flow, or end-to-end user latency.
- This repository does not establish clinical deployment readiness.
