# Paper Artifact Map

| Paper item | Claim / content | Supporting artifact |
|---|---|---|
| Table 3 | Locked train/validation/test split counts | `data/FINAL_split_manifest.csv` |
| Leakage audit | No confirmed cross-partition near duplicates in final split | `leakage_audit/FINAL_phase7_summary.json` |
| Table 6 | Locked three-class benchmark | `benchmarks/locked_final_benchmark/MANUSCRIPT_FINAL_3Class_Percent.csv` |
| Table 7 | Cataract-vs-Normal clinical metrics | `benchmarks/locked_final_benchmark/MANUSCRIPT_FINAL_Clinical_Percent.csv` |
| Confusion matrices | Five-model test confusion matrices | `benchmarks/locked_final_benchmark/confusion_matrices/` |
| Tables 8-9 | McNemar and DeLong pairwise tests | `benchmarks/statistical_tests/MANUSCRIPT_FINAL_Pairwise_Statistical_Tests.csv` |
| Table 10 | Last-block fine-tuning sensitivity | `benchmarks/fine_tuning_sensitivity/Reviewer_10_2_Final_Comparison.csv` |
| Table 11 | Tesla T4 latency | `latency/t4/Table_T4_latency_rebenchmark_100runs.csv` |
| Table 12 | Android physical-device latency | `latency/android/android_latency_summary.csv` and `latency/android/logs/` |
| Table 13 | ODIR zero-shot evaluation | `odir_zeroshot/ODIR_True_ZeroShot_Summary.csv` |
| Deployment model | Selected MobileNetV2 LastBlock TFLite | `deployment/tflite/MobileNetV2_LastBlock_float32.tflite` |
| Grad-CAM | Selected model inspection outputs | `gradcam/` |
| Figures | Manuscript figures | `figures/` |
