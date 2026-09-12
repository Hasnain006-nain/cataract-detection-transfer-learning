# Android Physical-Device Benchmark

This folder contains the final Android benchmark evidence for the selected MobileNetV2 LastBlock TensorFlow Lite model.

The manuscript values are supported by:

- `android_latency_summary.csv`
- `MobileNetV2_REVIEWER_SUMMARY.txt`
- `MobileNetV2_FINAL_RESULT.txt`
- `logs/MobileNetV2_latency_log.txt`
- `logs/MobileNetV2_full_log.txt`

Protocol:

- Device: Xiaomi 23053RN02A
- Android: 15 / SDK 35
- Runtime: TensorFlow Lite Android benchmark
- Delegate: XNNPACK CPU
- Threads: 4
- Warmup runs: 10
- Timed runs: 100
- GPU and NNAPI disabled
- Randomized benchmark tensor input, model invocation only
