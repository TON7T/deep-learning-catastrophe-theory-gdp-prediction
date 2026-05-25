# Deep Learning and Catastrophe Theory for GDP Prediction

This repository contains the code and data used in the research project **Deep Learning and Catastrophe Theory for GDP Prediction**. The study evaluates the predictive performance of Long Short-Term Memory (LSTM) networks for modeling the trajectory of GDP at constant 2015 prices in U.S. dollars. In addition to models trained exclusively on real macroeconomic data, the project explores a synthetic pretraining strategy based on time series generated from a potential function inspired by the cusp catastrophe model.

The repository is intended to support the consultation, use, and understanding of the computational procedures implemented in the study, as well as to provide a basis for future research extensions.

## Repository Structure

```text
.
├── 01_dataset_construction.ipynb
├── 02_real_data_training_and_model_selection.ipynb
├── 03_synthetic_data_generation.ipynb
├── 04_lstm_synthetic_pretraining.ipynb
├── 05_lstm_fine_tuning.ipynb
├── README.md
├── base_datos.csv
└── data_reshaped.npy
```

## Files Description

| File | Description |
|---|---|
| `01_dataset_construction.ipynb` | Constructs the main dataset used in the study from World Bank data. |
| `02_real_data_training_and_model_selection.ipynb` | Implements the first experimental stage using real data. It evaluates combinations of input variables and hyperparameters to select the configuration with the lowest validation RMSE. |
| `03_synthetic_data_generation.ipynb` | Generates synthetic time series from the proposed potential function inspired by the cusp catastrophe model. This notebook specifies the time-dependent functions used for the system coefficients. |
| `04_lstm_synthetic_pretraining.ipynb` | Performs the pretraining of the LSTM network using the generated synthetic time series. |
| `05_lstm_fine_tuning.ipynb` | Fine-tunes the pretrained model using real data. |
| `base_datos.csv` | Real macroeconomic dataset used in the empirical analysis. |
| `data_reshaped.npy` | Synthetic dataset used for the LSTM pretraining stage. |

## Methodological Overview

The workflow follows five main stages:

1. **Dataset construction**  
   A real macroeconomic dataset is constructed from World Bank data. The target variable is GDP at constant 2015 prices in U.S. dollars. The dataset also includes macroeconomic control variables used to evaluate whether additional information improves predictive performance.

2. **Training with real data and model selection**  
   LSTM models are trained using real data. Different combinations of input variables are evaluated, followed by hyperparameter tuning. The main evaluation metric is the Root Mean Squared Error (RMSE).

3. **Synthetic data generation**  
   Synthetic time series are generated from a parametrization of a potential function inspired by the cusp catastrophe model. The aim is to create trajectories that incorporate nonlinear dynamics, including patterns of decline and recovery.

4. **Synthetic pretraining**  
   An LSTM architecture is pretrained using the synthetic dataset. This stage allows the model to learn general temporal patterns before being adapted to the real GDP series.

5. **Fine-tuning with real data**  
   The pretrained model is fine-tuned using real data. This step adapts the representations learned during synthetic pretraining to the observed dynamics of the target variable.

## Data

This repository includes two data files:

- `base_datos.csv`: real dataset used for training, validation, and testing with macroeconomic data.
- `data_reshaped.npy`: synthetic dataset generated from the proposed potential-function framework and used during the pretraining stage.

The real dataset is chronologically divided into training, validation, and test subsets. Normalization is performed using only the training set parameters in order to avoid data leakage.

## Main Results

The empirical results indicate that synthetic pretraining followed by fine-tuning achieved the best out-of-sample performance among the evaluated LSTM specifications. In the test set, the model with synthetic pretraining obtained an RMSE of **0.275**, compared with **0.409** for the target-only model and **0.369** for the best-performing configuration trained only with real data.

Although the pretrained model achieved the lowest test RMSE, the error still represents a non-negligible proportion of the observed variability in the test set. Therefore, the results should be interpreted as evidence that synthetic pretraining is a promising strategy, rather than as a definitive early-warning system.

## Requirements

The notebooks were developed in Python using Jupyter Notebook. The main libraries required include:

```text
numpy
pandas
matplotlib
scikit-learn
tensorflow
keras
```

Depending on the local environment, additional standard scientific-computing libraries may be required.

## Disclaimer

The implemented models should not be interpreted as a definitive early-warning system or as a basis for economic policy decisions.

Due to the stochastic nature of neural network training some numerical results may vary across executions or computational environments. Therefore, results may differ from one run to another.

## Author

Antonio Trávez
