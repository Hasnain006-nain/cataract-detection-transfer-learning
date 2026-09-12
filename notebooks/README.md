# Notebooks

This folder contains the code notebooks used to generate or verify the final cataract-screening study artifacts.

The notebooks are provided as research code. They are not a clinical application and do not include raw third-party images. Rerunning the full workflow requires access to the original datasets and a compatible Python/TensorFlow environment.

## Folder Map

| Folder | Purpose |
|---|---|
| `final_pipeline/` | Leakage-control, final verification, locked evaluation, statistics, Grad-CAM, ODIR zero-shot, TensorFlow Lite export, and latency audit notebooks. |
| `training_models/` | Model-specific clean-split training notebooks for MobileNetV2, DenseNet201, InceptionResNetV2, ResNet152V2, and Xception. |

## Recommended Reading Order

| Step | Notebook | Purpose |
|---:|---|---|
| 1 | `final_pipeline/01_build_leakage_controlled_split.ipynb` | Build leakage-controlled split. |
| 2 | `final_pipeline/02_reaudit_clean_split.ipynb` | Re-audit split for duplicates/near-duplicates. |
| 3 | `final_pipeline/03_rebuild_split_with_confirmed_pairs.ipynb` | Rebuild using confirmed pair information. |
| 4 | `final_pipeline/04_reaudit_clean_split_v2.ipynb` | Second-pass split audit. |
| 5 | `final_pipeline/05_final_global_family_clustering.ipynb` | Final global family clustering. |
| 6 | `final_pipeline/06_final_independent_verification.ipynb` | Independent verification of final split. |
| 7 | `training_models/MobileNetV2_clean_split_training.ipynb` | MobileNetV2 frozen clean-split training. |
| 8 | `training_models/DenseNet201_clean_split_training.ipynb` | DenseNet201 frozen clean-split training. |
| 9 | `training_models/InceptionResNetV2_clean_split_training.ipynb` | InceptionResNetV2 frozen clean-split training. |
| 10 | `training_models/ResNet152V2_clean_split_training.ipynb` | ResNet152V2 frozen clean-split training. |
| 11 | `training_models/Xception_clean_split_training.ipynb` | Xception frozen clean-split training. |
| 12 | `final_pipeline/07_mobilenetv2_densenet201_last_block_finetuning.ipynb` | Last-block fine-tuning sensitivity analysis. |
| 13 | `final_pipeline/08_inceptionresnetv2_corrected_13_layer_frozen.ipynb` | Corrected InceptionResNetV2 frozen run. |
| 14 | `final_pipeline/09_locked_five_model_benchmark.ipynb` | Locked five-model benchmark. |
| 15 | `final_pipeline/10_statistical_tests_mcnemar_delong_holm.ipynb` | McNemar, DeLong, and Holm-adjusted paired tests. |
| 16 | `final_pipeline/11_mobilenetv2_gradcam_analysis.ipynb` | MobileNetV2 Grad-CAM inspection. |
| 17 | `final_pipeline/12_odir_true_zeroshot_external_validation.ipynb` | ODIR-5K true zero-shot external validation. |
| 18 | `final_pipeline/13_odir_protocol_sanity_audit_no_training.ipynb` | ODIR protocol sanity audit. |
| 19 | `final_pipeline/14_tflite_export_and_deployment_latency_audit.ipynb` | TensorFlow Lite export and deployment latency audit. |

## Notes

- Output artifacts from these notebooks are organized in the top-level repository folders such as `benchmarks/`, `data/`, `deployment/`, `latency/`, `leakage_audit/`, `gradcam/`, and `odir_zeroshot/`.
- Raw image datasets are not included in this repository.
- Some paths inside notebooks may point to the original execution environment and may need adjustment before rerunning.
