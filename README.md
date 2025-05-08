# 📘 ML Platform Architecture – README

This repository contains the high-level design and implementation outline for a scalable, secure, and modular machine learning platform tailored for retail banking needs.

## 🚀 Project Overview

A hybrid ML platform designed to:

* Keep raw customer data on-prem (e.g., Oracle DWH)
* Leverage cloud compute (AWS SageMaker) for training
* Serve models via internal FastAPI or AWS Lambda
* Enable observability, reproducibility, and compliance

## 📂 Repository Structure

```
.
├── dags/                  # Airflow DAGs for ingestion, training, retraining
├── dbt/                  # DBT models for SQL feature transformation
├── features/             # pandas + sklearn feature pipelines
├── model_training/       # Dockerized model training code (XGBoost, LightGBM)
├── monitoring/           # EvidentlyAI & Prometheus integrations
├── deployment/           # FastAPI app + Lambda functions
├── terraform/            # Infrastructure as Code (IAM, VPC, S3)
└── README.md             # This file
```

## ⚙️ Tech Stack

| Component           | Technology                       |
| ------------------- | -------------------------------- |
| Ingestion           | Oracle SQL + Airflow             |
| Feature Engineering | DBT, pandas, sklearn             |
| Versioning          | DVC or LakeFS                    |
| Model Training      | SageMaker + MLflow               |
| Serving             | FastAPI / AWS Lambda             |
| Monitoring          | Prometheus, Grafana, EvidentlyAI |
| IaC                 | Terraform                        |

## 📌 Usage Instructions

### 1. Run Feature Pipeline

```bash
python features/build_features.py --input data/raw.csv --output data/features.parquet
```

### 2. Train Model

```bash
cd model_training/
python train.py --config configs/xgb_config.yaml
```

### 3. Serve Model Locally (FastAPI)

```bash
cd deployment/
uvicorn app:app --reload
```

### 4. Run Monitoring Dashboard

```bash
docker-compose up monitoring
```

## 🧠 Model Lifecycle Flow

1. Ingest raw data via Airflow
2. Transform features using DBT + pandas
3. Store & version features (DVC)
4. Train model on SageMaker
5. Track model & metrics (MLflow)
6. Deploy as API (FastAPI / Lambda)
7. Monitor model health (drift, latency, alerts)

## 🔐 Security Notes

* TLS encryption for all cloud traffic
* IAM roles scoped to least privilege
* Audit logs via CloudTrail / application logs

## 📈 Future Enhancements

* Feature store centralization
* Automated model promotion policies
* Feedback loop from BI systems

---

**Maintainer**: Oleksandr Shevchenko
**Contact**: [oleksandr.shevchenko.ua@gmail.com](mailto:oleksandr.shevchenko.ua@gmail.com)
