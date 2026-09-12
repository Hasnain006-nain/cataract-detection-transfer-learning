# Data Manifests

This folder contains the final split manifest and data-provenance notes for the cataract screening artifact package. Raw medical or third-party images are not redistributed here unless rights are explicitly clear.

## Primary Dataset

| Dataset / Source | Role | Link | Notes |
|---|---|---|---|
| Cataract Eye Dataset - 3-Class Mobile Screening | Curated internal three-class source release | https://www.kaggle.com/datasets/suyog17/cataracteyedata | 13,669 images: 4,514 Cataract, 5,154 Normal, 4,001 Not Eye. Kaggle license field recorded as Unknown. |
| K. B. Ojha Cataract Detection using CNN | Upstream Cataract/Normal image source | https://github.com/krishnabojha/Cataract_Detection-using-CNN | Source for the ocular classes in the curated release. |
| Indian Food Images Dataset | Upstream Not Eye source | https://www.kaggle.com/datasets/iamsouravbanerjee/indian-food-images-dataset | 4,000 of 4,001 Not Eye images were traced to this dataset. |

## Final Manifest Counts

Use `FINAL_split_manifest.csv` to verify final split membership and class counts.

| Partition | Images |
|---|---:|
| Train | 8,845 |
| Validation | 2,178 |
| Test | 2,587 |
| Quarantine | 14 |

## External Dataset

ODIR-5K was used only for true zero-shot external-domain stress testing and is not redistributed here: https://odir2019.grand-challenge.org/dataset/

The external ODIR-5K data was not used for training, calibration, threshold selection, or model selection.
