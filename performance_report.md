# OSNR estimation from eye diagrams - performance report

*Generated automatically on 2026-11-20 14:45 from a notebook run. SIMULATED DATA - not laboratory measurements.*

* Dataset: 5250 eye diagrams (21 OSNR levels x 5 CD levels x 50 realisations), off-grid set: 600
* Split: train 3325, val 712, test 713, unseen-combination 500
* Held-out combinations: osnr12_cd0, osnr12_cd200, osnr12_cd400, osnr18_cd100, osnr19_cd100, osnr21_cd400, osnr24_cd200, osnr24_cd800, osnr25_cd0, osnr25_cd800
* Training: 44 epochs, 2.2 min, QUICK_RUN = False
* Back-to-back OSNR for Q = 6 in this simulated system: 16.5 dB

## CNN - OSNR regression
| set | N | MAE_dB | MSE_dB2 | RMSE_dB | R2 | bias_dB | within_0.5dB_% | within_1dB_% |
|---|---|---|---|---|---|---|---|---|
| test (seen combos) | 713 | 0.232 | 0.087 | 0.296 | 0.998 | -0.095 | 90.323 | 99.860 |
| unseen combos | 500 | 0.218 | 0.077 | 0.277 | 0.997 | -0.061 | 91.400 | 100.000 |
| off-grid | 600 | 0.206 | 0.070 | 0.264 | 0.998 | -0.072 | 93.833 | 100.000 |

## CNN - impairment classification
| set | accuracy | macro_precision | macro_recall | macro_F1 |
|---|---|---|---|---|
| test (seen combos) | 0.994 | 0.994 | 0.994 | 0.994 |
| unseen combos | 0.998 | 0.750 | 0.749 | 0.749 |
| off-grid | 0.807 | 0.857 | 0.650 | 0.675 |

## Comparison with baselines (OSNR regression)
| model /  | MAE_dB / off-grid | MAE_dB / test (seen combos) | MAE_dB / unseen combos | R2 / off-grid | R2 / test (seen combos) | R2 / unseen combos | RMSE_dB / off-grid | RMSE_dB / test (seen combos) | RMSE_dB / unseen combos |
|---|---|---|---|---|---|---|---|---|---|
| CNN (multi-task) | 0.206 | 0.232 | 0.218 | 0.998 | 0.998 | 0.997 | 0.264 | 0.296 | 0.277 |
| MLP (32×32 pixels) | 0.420 | 0.323 | 0.335 | 0.989 | 0.995 | 0.993 | 0.593 | 0.443 | 0.451 |
| Random Forest (eye features) | 0.388 | 0.108 | 0.298 | 0.990 | 0.999 | 0.993 | 0.566 | 0.209 | 0.453 |
| SVR-RBF (eye features) | 0.202 | 0.171 | 0.158 | 0.997 | 0.997 | 0.998 | 0.304 | 0.311 | 0.212 |

## Classification comparison
| model | set | accuracy | macro_precision | macro_recall | macro_F1 |
|---|---|---|---|---|---|
| CNN (multi-task) | test (seen combos) | 0.994 | 0.994 | 0.994 | 0.994 |
| CNN (multi-task) | unseen combos | 0.998 | 0.750 | 0.749 | 0.749 |
| CNN (multi-task) | off-grid | 0.807 | 0.857 | 0.650 | 0.675 |
| Random Forest (eye features) | test (seen combos) | 0.997 | 0.996 | 0.998 | 0.997 |
| Random Forest (eye features) | unseen combos | 1.000 | 0.750 | 0.750 | 0.750 |
| Random Forest (eye features) | off-grid | 0.825 | 0.803 | 0.683 | 0.703 |
