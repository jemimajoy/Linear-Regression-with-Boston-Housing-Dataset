# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository overview

This is a single educational Jupyter notebook (`LR.ipynb`) demonstrating Simple Linear Regression on the Boston Housing dataset using scikit-learn. There is no application code, package structure, build system, or test suite — the notebook is both the documentation and the deliverable.

## Setup and running

Dependencies (no requirements.txt or environment file exists; install manually):
```
pip install numpy pandas matplotlib seaborn scikit-learn jupyter
```

Run the notebook:
```
jupyter notebook LR.ipynb
```

Note: `LR.ipynb` imports `load_boston` from `sklearn.datasets`, which was removed in scikit-learn 1.2+ due to ethical concerns about the dataset (the `B` column). Running this notebook requires `scikit-learn<1.2`, or the loader call must be replaced with an alternative data source (e.g. loading the CSV directly from the original CMU StatLib source, or `fetch_california_housing` as a different dataset) if working with a current scikit-learn version.

## Notebook structure

`LR.ipynb` follows a linear, top-to-bottom workflow — there is no modularization into functions or scripts:

1. **Load data** — `load_boston()` from sklearn, inspect keys and `DESCR`.
2. **Build DataFrame** — combine `data`/`feature_names` into a `boston` DataFrame, append the target as a `Price` column.
3. **Explore** — `.info()`, `.describe()`, correlation heatmap (`sns.heatmap`), price distribution (`sns.distplot`).
4. **Split** — `train_test_split(X, y, test_size=0.3, random_state=50)`, where `X` is `boston.drop('Price', axis=1)` and `y` is `boston['Price']`.
5. **Train** — fit `sklearn.linear_model.LinearRegression` on the training split.
6. **Evaluate** — inspect `intercept_`/`coef_`, scatter-plot actual vs. predicted prices on the test set, compute MAE/MSE/RMSE via `sklearn.metrics`.

When modifying the notebook, preserve this sequence (load → build DataFrame → explore → split → train → evaluate) since later cells depend on variable names defined earlier (`boston`, `X`, `y`, `X_train`/`X_test`/`y_train`/`y_test`, `lr`, `pred`).
