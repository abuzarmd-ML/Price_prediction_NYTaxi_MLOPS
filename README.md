# New York Taxi Price Prediction

This repository implements a complete end-to-end pipeline for predicting New York taxi fares. The project covers data collection, model training, evaluation, deployment, and monitoring, utilizing tools like Prefect for orchestration, DVC for data versioning, and FastAPI for model serving.

## Features

- **Data Collection & Processing**: Automated data extraction and preprocessing.
- **Model Training & Evaluation**: A custom pipeline using `XGBoost` and evaluation processes.
- **Model Deployment**: Prediction API served through FastAPI.
- **Monitoring**: Data drift, prediction drift, and quality checks via Evidently, tracked with Grafana.
- **Versioning**: DVC is used for versioning data and models.
- **Deployment**: Hosted using Fly.io with AWS Tigris as storage.

---

## Project Structure

```bash
.
├── backend/                    # FastAPI backend for model serving
├── dvclive/                    # DVC live tracking for model and data versions
├── model_pipeline/             # Data processing, model training, and evaluation pipeline
├── monitoring/                 # Monitoring logs, metrics, and Evidently reports
├── scripts/                    # Utility and support scripts
├── tests/                      # Test cases for model, API, and data validation
├── Dockerfile                  # Docker setup for the application
├── dvc.lock                    # DVC lock file for version control
├── dvc.yaml                    # DVC configuration for the pipeline
├── fly.toml                    # Fly.io deployment configuration
├── requirements-app.txt        # Requirements specific to the FastAPI application
├── requirements.txt            # Main Python dependencies
```

## Setup Instructions

- **Clone the Repository**
  
`` git clone https://github.com/abuzarmd-ML/Price_prediction_NYTaxi_MLOPS.git ``

`` cd ny-taxi-price-prediction ``

`` pip install -r requirements.txt ``

`` pip install -r requirements-app.txt ``

`` dvc init ``

`` dvc pull ``

`` EVIDENTLY_TOKEN=your_evidently_token``

`` EVIDENTLY_PROJECT_ID=your_project_id ``

`` python model_pipeline.py``

`` uvicorn backend.main:app --reload``

`` curl -X POST "http://localhost:8000/predict" -d @sample_request.json ``

## Monitoring and Metrics Reporting

To track data and prediction drifts, run the monitoring scripts that generate reports and upload them to Evidently Cloud:``
```python monitoring_report.py```

**Using Evidently for Monitoring**
Evidently helps in  visualizing and monitoring the performance of the machine learning models. It provides features to track data drift, prediction drift, and data quality.

Example of generating reports:
```
data_report = create_data_report(df_current=df_current, df_ref=df_train_val)

prediction_report = create_prediction_drift_report(df_current=df_current, df_ref=df_test)

upload_reports(data_report=data_report, prediction_report=prediction_report)
```

## Fly.io Deployment

**Install the Fly.io CLI**

- **Log in to Fly.io:**
  
  ``flyctl auth login``

  ``fly deploy``

## Testing
Unit tests for the model, API, and data pipeline are available in the tests/ folder. To run the tests:
``pytest tests/``
