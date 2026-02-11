
---

# 📄 deployment.md

````markdown
# 🚀 Deployment Guide – YouTube Sentiment Analysis System

This document explains how the Sentiment Analysis system was deployed using AWS EC2, Docker, MLflow, and Amazon S3.

---

# 🏗️ System Architecture

The deployed architecture follows MLOps best practices:

User → Flask API (Docker on EC2) → MLflow Server (EC2) → S3 (Model Artifacts)

### Components:

- **Flask API** – Serves prediction requests
- **MLflow Server** – Model tracking & registry
- **Amazon S3** – Stores trained model artifacts
- **Docker** – Containerizes the API
- **AWS EC2** – Hosts MLflow and Docker container

---

# 🧠 Model Training & Registry

## 1️⃣ Model Training

- Algorithm: LightGBM Classifier
- Feature Engineering: TF-IDF (n-grams)
- Data Versioning: DVC
- Model Saving: MLflow

The model was trained locally and logged using MLflow.

---

## 2️⃣ MLflow Setup on EC2

MLflow server was deployed on an AWS EC2 instance.

### MLflow Server Command:

```bash
mlflow server \
--host 0.0.0.0 \
--port 5000 \
--backend-store-uri sqlite:///mlflow.db \
--default-artifact-root s3://<your-s3-bucket-name> \
--allowed-hosts "*"
````

### Configuration:

* Backend Store: SQLite
* Artifact Store: Amazon S3
* Model Registry enabled

All trained models are stored in S3 and registered in MLflow.

---

# 🐳 Docker Deployment (Flask API)

The Flask application was containerized using Docker to ensure portability and consistent runtime environments.

---

## 1️⃣ Dockerfile

```dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY . /app

RUN pip install --upgrade pip
RUN pip install -r requirements.txt

RUN python -c "import nltk; nltk.download('stopwords'); nltk.download('wordnet')"

EXPOSE 8000

CMD ["gunicorn", "--bind", "0.0.0.0:8000", "app:app"]
```

---

## 2️⃣ Build Docker Image

```bash
docker build -t youtube-sentiment-api .
```

---

## 3️⃣ Run Docker Container on EC2

```bash
docker run -d \
--name sentiment-api \
--restart always \
--network host \
youtube-sentiment-api
```

The API runs on port:

```
http://<EC2_PUBLIC_IP>:8000
```

---

# 🔐 S3 Integration

Amazon S3 is used as the MLflow artifact store.

## Why S3?

* Highly durable object storage
* Scalable
* Industry standard for ML artifacts
* Easy integration with MLflow

## Access Control

An IAM Role was attached to the EC2 instance with permissions:

* s3:GetObject
* s3:PutObject
* s3:ListBucket

No AWS keys were stored in code.

---

# 🔄 API Flow

1. User sends request to `/predict`
2. Flask API receives comment text
3. Text is preprocessed
4. TF-IDF transformation applied
5. Model is loaded from MLflow registry
6. Prediction generated
7. Numeric labels mapped to sentiment labels
8. JSON response returned

---

# 📊 Endpoints

### 1️⃣ `/predict`

Request:

```json
{
  "comments": ["Great movie!"]
}
```

Response:

```json
[
  {
    "comment": "Great movie!",
    "sentiment": "Positive"
  }
]
```

---

### 2️⃣ `/predict_with_timestamps`

Returns sentiment along with timestamps.

---

### 3️⃣ `/generate_chart`

Generates sentiment distribution pie chart.

---

### 4️⃣ `/generate_wordcloud`

Generates word cloud image.

---

### 5️⃣ `/generate_trend_graph`

Generates sentiment trend over time.

---

# 🧩 Challenges Faced

* MLflow schema enforcement errors
* Feature name mismatch between TF-IDF and prediction input
* Git & DVC tracking conflicts
* Label mapping (numeric → readable sentiment)
* Port conflicts between MLflow and Flask

All issues were debugged and resolved.

---

# 🎯 Why This Deployment Is Production-Ready

✔ Model versioning with MLflow
✔ Artifact storage in S3
✔ Containerized API with Docker
✔ Cloud-hosted infrastructure (EC2)
✔ IAM-based secure access
✔ Clean REST API architecture

---

# 🔮 Future Improvements

* Add Nginx reverse proxy
* Enable HTTPS with SSL
* Deploy using Docker Compose
* CI/CD integration
* Push Docker image to AWS ECR
* Move to ECS or Kubernetes

---

# 📌 Conclusion

This deployment demonstrates an end-to-end MLOps pipeline including:

* Data versioning
* Experiment tracking
* Model registry
* Cloud storage
* Containerized deployment
* REST API serving

The system follows industry-standard deployment practices and is scalable for real-world usage.

```

---


```
