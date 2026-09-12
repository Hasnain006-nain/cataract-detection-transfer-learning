# Data Card

The internal dataset uses Cataract, Normal, and Not Eye classes with a locked leakage-controlled split.

## Dataset Sources

| Dataset / Source | Role | Link | Notes |
|---|---|---|---|
| Cataract Eye Dataset - 3-Class Mobile Screening | Curated internal three-class release | https://www.kaggle.com/datasets/suyog17/cataracteyedata | 13,669 images: 4,514 Cataract, 5,154 Normal, 4,001 Not Eye. Kaggle license field recorded as Unknown. |
| K. B. Ojha Cataract Detection using CNN | Upstream Cataract/Normal source | https://github.com/krishnabojha/Cataract_Detection-using-CNN | Ocular source data for the curated release. |
| Indian Food Images Dataset | Upstream Not Eye source | https://www.kaggle.com/datasets/iamsouravbanerjee/indian-food-images-dataset | 4,000 of 4,001 Not Eye images were traced to this dataset. |
| ODIR-5K | External zero-shot stress test only | https://odir2019.grand-challenge.org/dataset/ | Not used for training, calibration, threshold selection, or model selection. Not redistributed here. |

## Final Manifest Counts

| Partition | Images |
|---|---:|
| Train | 8,845 |
| Validation | 2,178 |
| Test | 2,587 |
| Quarantine | 14 |

## Important Limitations

- Raw source images are not redistributed in this repository.
- The curated Kaggle release records the license as Unknown, and this repository does not relicense underlying third-party images.
- Patient identifiers are unavailable for the upstream ocular collection.
- Exact and near-duplicate leakage controls were performed, but this is not equivalent to patient-level splitting.
- One Not Eye image source/license was not fully established in the manuscript evidence.
- ODIR-5K is used only as an external zero-shot stress test and is not redistributed here.
