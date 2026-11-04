# MLflow Wine Quality Example

This project trains an ElasticNet regression model to predict red wine quality
from physicochemical measurements. It uses MLflow to track training parameters,
evaluation metrics, and the resulting model.

## Requirements

- Python
- Internet access to download the dataset

The project dependencies are listed in [`requirements.txt`](requirements.txt).

## Setup

Create and activate a virtual environment, then install the dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m pip install scikit-learn
```

`scikit-learn` is installed explicitly because the application imports it
directly.

## Run

Run with the default ElasticNet parameters (`alpha=0.5` and `l1_ratio=0.5`):

```powershell
python app.py
```

Or provide `alpha` and `l1_ratio` as positional arguments:

```powershell
python app.py 0.1 0.3
```

The script downloads the dataset, makes a reproducible 75/25 train/test split,
trains the model, and prints RMSE, MAE, and R-squared metrics. Each run logs
`alpha`, `l1_ratio`, and those metrics to MLflow, along with a model and its
inferred input/output signature.

## View tracked runs

Start the MLflow tracking UI in a separate terminal:

```powershell
mlflow ui
```

Then open [http://localhost:5000](http://localhost:5000). The UI uses MLflow's
configured tracking store; for the default local setup, run it from this
project directory.

When the tracking URI uses a file store, the model is logged without registry
registration. For other tracking URI schemes, the script attempts to register
the model as `ElasticnetWineModel`; the configured backend must support the
MLflow Model Registry.

## Dataset

The application downloads the red wine quality CSV from the MLflow GitHub
repository. The dataset is from the UCI Wine Quality dataset, described in:

P. Cortez, A. Cerdeira, F. Almeida, T. Matos, and J. Reis, “Modeling wine
preferences by data mining from physicochemical properties,” *Decision Support
Systems*, 47(4), 547–553, 2009.
