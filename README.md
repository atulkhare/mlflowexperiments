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
```

Set a DagsHub access token in the current PowerShell session before running the
app (create one in your DagsHub account settings):

```powershell
$env:DAGSHUB_USER_TOKEN = "<your-dagshub-token>"
```

The app initializes MLflow tracking for the `atulkhare/mlflowexperiments`
DagsHub repository before it starts a run. Keep the token out of source control;
it is used only for authentication.

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

Runs are logged to the DagsHub repository's MLflow UI:
[https://dagshub.com/atulkhare/mlflowexperiments.mlflow](https://dagshub.com/atulkhare/mlflowexperiments.mlflow).

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