# Machine Learning for Robotic Inverse Kinematics

Machine learning approaches to the inverse kinematics of the **ABB IRB 2400** industrial manipulator, using regression models to predict joint configurations from end-effector poses.

## Overview

The project explores and compares different regression algorithms for learning the mapping between Cartesian end-effector poses and robot joint configurations.

The workflow includes:
- Dataset exploration and preprocessing.
- Detection and removal of data leakage from input joint variables.
- Feature scaling and train/test splitting.
- Hyperparameter optimization using `GridSearchCV`.
- Multi-output regression and per-joint performance evaluation.

## Models Evaluated

- Ridge Regression
- Kernel Ridge Regression (RBF)
- Support Vector Regression (RBF)
- Decision Tree
- Random Forest
- Gradient Boosting

## Results

Models are evaluated on a held-out test set using MAE, MSE and R², both globally and for individual joints.

| Model | Test R² | Test MAE |
|---|---:|---:|
| Gradient Boosting | 0.334 | 1.334 |
| Random Forest | 0.321 | 1.328 |
| Kernel Ridge (RBF) | 0.298 | 1.357 |
| SVR (RBF) | 0.288 | 1.308 |
| Decision Tree | 0.248 | 1.372 |
| Ridge Regression | 0.108 | 1.458 |

Gradient Boosting achieved the highest overall R², although performance varied significantly across joints.

## Key Finding

An initial analysis revealed that `q_in` variables introduced data leakage: a Ridge model using only these variables achieved an R² of 0.9974. They were therefore excluded from the final input features to ensure a more meaningful evaluation of pose-to-joint regression.

## Technologies

Python · NumPy · Pandas · Scikit-learn · Matplotlib

## Dataset

[ABB IRB 2400 Arm Robot Kinematics Dataset – Kaggle](https://www.kaggle.com/datasets/luisatencio/abb-irb-2400-arm-robot-kinematics-dataset)

## Running the Notebook

Install the required dependencies:

```bash
pip install numpy pandas matplotlib scikit-learn kagglehub
```

Open and run the Jupyter notebook. The dataset is downloaded automatically using `kagglehub`.
