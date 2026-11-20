# OSNR Estimation from Eye Diagrams

A multi-task CNN that estimates optical signal-to-noise ratio (OSNR) and classifies the impairment type (noise and/or chromatic dispersion) from 128×128 grayscale eye-diagram images.

> **Note:** all data is simulated. It does not come from laboratory measurements.

## Dataset
- 5,250 eye diagrams: 21 OSNR levels × 5 CD levels × 50 realisations, plus 600 off-grid samples
- Split: train 3,325 / val 712 / test 713 / unseen-combination 500
- Impairment classes: `clean`, `noise_impaired`, `dispersion_impaired`, `noise_and_dispersion` (see `label_mapping.json`)

## Results (CNN, OSNR regression)
| set | MAE (dB) | RMSE (dB) | R² | within 1 dB |
|---|---|---|---|---|
| test (seen combos) | 0.232 | 0.296 | 0.998 | 99.9% |
| unseen combos | 0.218 | 0.277 | 0.997 | 100% |
| off-grid | 0.206 | 0.264 | 0.998 | 100% |

The full report, including the MLP, Random Forest and SVR baselines, is in [performance_report.md](performance_report.md).

## Contents
- `model/`: trained Keras model (`osnr_cnn_best.keras`) and weights (`osnr_cnn.weights.h5`)
- `plots/`: EDA, training curves, confusion matrices, error analysis and model comparison
- `metadata*.csv`: per-sample labels and splits
- `preprocessing_config.json`: image preprocessing parameters
- `training_history.*`, `training_log.csv`: training logs
- `model_comparison.csv`, `bn_ablation.csv`: comparison and ablation results
