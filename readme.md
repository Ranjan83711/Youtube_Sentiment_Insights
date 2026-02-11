# 🎬 YouTube Sentiment Insights

> An end-to-end MLOps project for analyzing YouTube comment sentiments using Machine Learning, MLflow, DVC, Docker, and AWS.

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-2.0+-green.svg)](https://flask.palletsprojects.com/)
[![MLflow](https://img.shields.io/badge/MLflow-Tracking-orange.svg)](https://mlflow.org/)
[![Docker](https://img.shields.io/badge/Docker-Ready-blue.svg)](https://www.docker.com/)
[![DVC](https://img.shields.io/badge/DVC-Pipeline-purple.svg)](https://dvc.org/)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Project Architecture](#-project-architecture)
- [Project Structure](#-project-structure)
- [Technology Stack](#-technology-stack)
- [Installation](#-installation)
- [Usage](#-usage)
- [ML Pipeline](#-ml-pipeline)
- [API Endpoints](#-api-endpoints)
- [Chrome Extension](#-chrome-extension)
- [Deployment](#-deployment)
- [MLOps Practices](#-mlops-practices)
- [Results](#-results)
- [Future Enhancements](#-future-enhancements)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Overview

**YouTube Sentiment Insights** is a production-ready machine learning system that analyzes YouTube comments to determine sentiment (Positive, Neutral, or Negative). The project demonstrates industry-standard MLOps practices including experiment tracking, model versioning, containerization, and cloud deployment.

### Key Highlights:
- 🤖 **LightGBM** classifier with **TF-IDF** feature engineering
- 📊 **MLflow** for experiment tracking and model registry
- 🔄 **DVC** for data versioning and pipeline orchestration
- 🐳 **Docker** for containerized deployment
- ☁️ **AWS EC2 + S3** for cloud infrastructure
- 🌐 **Flask REST API** for real-time predictions
- 🧩 **Chrome Extension** for YouTube integration

---

## ✨ Features

### Core Functionality
- ✅ Real-time sentiment analysis of YouTube comments
- ✅ Batch prediction with timestamps
- ✅ Sentiment distribution visualization (pie charts)
- ✅ Word cloud generation
- ✅ Sentiment trend analysis over time
- ✅ Chrome extension for seamless YouTube integration

### MLOps Features
- ✅ Automated ML pipeline with DVC
- ✅ Experiment tracking with MLflow
- ✅ Model versioning and registry
- ✅ Artifact storage in Amazon S3
- ✅ Containerized deployment with Docker
- ✅ RESTful API architecture
- ✅ Comprehensive logging and error handling

---

## 🏗️ Project Architecture

```
┌─────────────────┐
│  YouTube User   │
└────────┬────────┘
         │
         ▼
┌─────────────────────────┐
│  Chrome Extension       │
│  (Frontend Interface)   │
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────┐
│   Flask REST API        │
│   (Docker Container)    │
│   - /predict            │
│   - /generate_chart     │
│   - /generate_wordcloud │
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────┐
│   MLflow Server (EC2)   │
│   - Model Registry      │
│   - Experiment Tracking │
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────┐
│   Amazon S3             │
│   - Model Artifacts     │
│   - Vectorizer Files    │
└─────────────────────────┘
```

---

## 📁 Project Structure

```
Youtube_Sentiment_Insights/
│
├── 📂 src/                          # Source code
│   ├── 📂 data/
│   │   ├── data_ingestion.py        # Data loading and splitting
│   │   └── data_preprocessing.py    # Text preprocessing pipeline
│   │
│   ├── 📂 model/
│   │   ├── model_building.py        # Model training with LightGBM
│   │   ├── model_evaluation.py      # Model evaluation and metrics
│   │   └── register_model.py        # MLflow model registration
│   │
│   └── __init__.py
│
├── 📂 flask_app/                    # Flask API application
│   ├── app.py                       # Main Flask application
│   ├── test.py                      # API testing scripts
│   ├── lgbm_model.pkl               # Trained model (optional)
│   └── tfidf_vectorizer.pkl         # TF-IDF vectorizer (optional)
│
├── 📂 yt-chrome-plugin-frontend/    # Chrome Extension
│   ├── manifest.json                # Extension configuration
│   ├── popup.html                   # Extension UI
│   └── popup.js                     # Extension logic
│
├── 📂 data/                         # Data directory (DVC tracked)
│   ├── 📂 raw/                      # Raw train/test splits
│   └── 📂 interim/                  # Preprocessed data
│
├── 📂 notebook/                     # Jupyter notebooks for EDA
│
├── 📄 dvc.yaml                      # DVC pipeline definition
├── 📄 dvc.lock                      # DVC pipeline lock file
├── 📄 params.yaml                   # Hyperparameters and configs
├── 📄 requirements.txt              # Python dependencies
│
├── 📄 Dockerfile                    # Docker image definition
├── 📄 docker-compose.yml            # Docker Compose configuration
├── 📄 .dockerignore                 # Docker ignore patterns
│
├── 📄 lgbm_model.pkl                # Trained LightGBM model
├── 📄 tfidf_vectorizer.pkl          # TF-IDF vectorizer
├── 📄 experiment_info.json          # MLflow experiment metadata
│
├── 📄 DEPLOYMENT.md                 # Deployment documentation
├── 📄 DOCKER_README.md              # Docker usage guide
└── 📄 readme.md                     # This file
```

---

## 🛠️ Technology Stack

### Machine Learning
- **Algorithm**: LightGBM (Gradient Boosting)
- **Feature Engineering**: TF-IDF (n-grams: 1-3)
- **Text Processing**: NLTK (stopwords, lemmatization)
- **Data Handling**: Pandas, NumPy

### MLOps Tools
- **Experiment Tracking**: MLflow
- **Data Versioning**: DVC
- **Model Registry**: MLflow Model Registry
- **Pipeline Orchestration**: DVC Pipelines

### Backend & API
- **Framework**: Flask
- **CORS**: Flask-CORS
- **Visualization**: Matplotlib, Seaborn, WordCloud

### Deployment
- **Containerization**: Docker, Docker Compose
- **Cloud Platform**: AWS EC2
- **Storage**: Amazon S3
- **Model Serving**: MLflow Model Registry

### Frontend
- **Chrome Extension**: Vanilla JavaScript
- **YouTube API**: Google API Client

---

## 🚀 Installation

### Prerequisites
- Python 3.11+
- Docker & Docker Compose (for containerized deployment)
- AWS Account (for cloud deployment)
- Git

### Local Setup

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/Youtube_Sentiment_Insights.git
cd Youtube_Sentiment_Insights
```

2. **Create virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Download NLTK data**
```python
python -c "import nltk; nltk.download('stopwords'); nltk.download('wordnet'); nltk.download('omw-1.4')"
```

5. **Set up DVC** (optional)
```bash
dvc init
dvc remote add -d myremote s3://your-bucket-name
```

6. **Configure MLflow**
```bash
# Set MLflow tracking URI
export MLFLOW_TRACKING_URI=http://your-mlflow-server:5000
```

---

## 💻 Usage

### Running the ML Pipeline

The entire ML pipeline is orchestrated using DVC:

```bash
# Run the complete pipeline
dvc repro

# Run specific stages
dvc repro data_ingestion
dvc repro data_preprocessing
dvc repro model_building
dvc repro model_evaluation
dvc repro model_registration
```

### Running the Flask API Locally

```bash
# Navigate to flask_app directory
cd flask_app

# Run the Flask application
python app.py
```

The API will be available at `http://localhost:5000`

### Running with Docker

```bash
# Build and start the container
docker-compose up -d

# View logs
docker-compose logs -f

# Stop the container
docker-compose down
```

### Testing the API

```bash
# Health check
curl http://localhost:5000/

# Predict sentiment
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"comments": ["This video is amazing!", "I hate this content"]}'
```

---

## 🔄 ML Pipeline

The project uses **DVC** to orchestrate a reproducible ML pipeline with 5 stages:

### 1️⃣ Data Ingestion
- **Script**: `src/data/data_ingestion.py`
- **Purpose**: Load raw YouTube comments data and split into train/test sets
- **Output**: `data/raw/train.csv`, `data/raw/test.csv`
- **Parameters**: `test_size: 0.20`

### 2️⃣ Data Preprocessing
- **Script**: `src/data/data_preprocessing.py`
- **Purpose**: Clean and preprocess text data
- **Steps**:
  - Lowercase conversion
  - Remove special characters and URLs
  - Remove stopwords (retain sentiment-critical words: not, but, however, no, yet)
  - Lemmatization
- **Output**: `data/interim/train_processed.csv`, `data/interim/test_processed.csv`

### 3️⃣ Model Building
- **Script**: `src/model/model_building.py`
- **Algorithm**: LightGBM Classifier
- **Feature Engineering**: TF-IDF Vectorizer
- **Hyperparameters** (from `params.yaml`):
  ```yaml
  ngram_range: [1, 3]
  max_features: 1000
  learning_rate: 0.09
  max_depth: 20
  n_estimators: 367
  ```
- **Output**: `lgbm_model.pkl`, `tfidf_vectorizer.pkl`

### 4️⃣ Model Evaluation
- **Script**: `src/model/model_evaluation.py`
- **Metrics**:
  - Accuracy
  - Precision, Recall, F1-Score
  - Confusion Matrix
  - Classification Report
- **Logging**: Metrics logged to MLflow
- **Output**: `experiment_info.json`

### 5️⃣ Model Registration
- **Script**: `src/model/register_model.py`
- **Purpose**: Register model in MLflow Model Registry
- **Model Name**: `my_model`
- **Version**: Auto-incremented
- **Artifact Storage**: Amazon S3

---

## 🌐 API Endpoints

### 1. `GET /`
**Health Check**
```bash
curl http://localhost:5000/
```
Response: `"Welcome to our flask api"`

---

### 2. `POST /predict`
**Predict sentiment for comments**

**Request:**
```json
{
  "comments": [
    "This is an amazing video!",
    "I don't like this content"
  ]
}
```

**Response:**
```json
[
  {
    "comment": "This is an amazing video!",
    "sentiment": 1
  },
  {
    "comment": "I don't like this content",
    "sentiment": -1
  }
]
```

**Sentiment Labels:**
- `1` = Positive
- `0` = Neutral
- `-1` = Negative

---

### 3. `POST /predict_with_timestamps`
**Predict sentiment with timestamps**

**Request:**
```json
{
  "comments": [
    {
      "text": "Great video!",
      "timestamp": "2024-01-15T10:30:00Z"
    }
  ]
}
```

**Response:**
```json
[
  {
    "comment": "Great video!",
    "sentiment": "1",
    "timestamp": "2024-01-15T10:30:00Z"
  }
]
```

---

### 4. `POST /generate_chart`
**Generate sentiment distribution pie chart**

**Request:**
```json
{
  "sentiment_counts": {
    "1": 150,
    "0": 50,
    "-1": 30
  }
}
```

**Response:** PNG image (pie chart)

---

### 5. `POST /generate_wordcloud`
**Generate word cloud from comments**

**Request:**
```json
{
  "comments": [
    "amazing video great content",
    "love this tutorial"
  ]
}
```

**Response:** PNG image (word cloud)

---

### 6. `POST /generate_trend_graph`
**Generate sentiment trend over time**

**Request:**
```json
{
  "sentiment_data": [
    {
      "sentiment": 1,
      "timestamp": "2024-01-01T00:00:00Z"
    },
    {
      "sentiment": -1,
      "timestamp": "2024-01-02T00:00:00Z"
    }
  ]
}
```

**Response:** PNG image (line graph showing sentiment trends)

---

## 🧩 Chrome Extension

The project includes a Chrome extension for seamless YouTube integration.

### Installation

1. Open Chrome and navigate to `chrome://extensions/`
2. Enable "Developer mode"
3. Click "Load unpacked"
4. Select the `yt-chrome-plugin-frontend` folder

### Features

- 📊 Analyze sentiment of current video's comments
- 📈 View sentiment distribution
- ☁️ Generate word clouds
- 📉 Track sentiment trends over time

### Configuration

Update the API endpoint in `popup.js`:
```javascript
const API_URL = 'http://localhost:5000/';  // Change to your deployed URL
const API_KEY = 'YOUR_YOUTUBE_API_KEY';
```

---

## ☁️ Deployment

### MLflow Server Setup (AWS EC2)

```bash
- sudo apt update

- sudo apt install python3-pip

- sudo apt install pipenv

- sudo apt install virtualenv

- mkdir mlflow

- cd mlflow

- pipenv install mlflow

- pipenv install awscli

- pipenv install boto3

- pipenv shell


## Then set aws credentials
aws configure


#Finally Start MLflow server
mlflow server \
  --host 0.0.0.0 \
  --port 5000 \
  --backend-store-uri sqlite:///mlflow.db \
  --default-artifact-root s3://your-bucket-name \
  --allowed-hosts "*"
#open Public IPv4 DNS to the port 5000

#set uri in your local terminal and in your code 
export MLFLOW_TRACKING_URI=http://ec2-54-147-36-34.compute-1.amazonaws.com:5000/

```

### Docker Deployment

```bash
# Build Docker image
docker build -t youtube-sentiment-app .

# Run container
docker run -d \
  --name youtube-sentiment-app \
  -p 5000:5000 \
  -e MLFLOW_TRACKING_URI=http://your-mlflow-server:5000 \
  youtube-sentiment-app
```

### Using Docker Compose

```bash
docker-compose up -d
```

For detailed deployment instructions, see [DEPLOYMENT.md](DEPLOYMENT.md)

---

## 🔧 MLOps Practices

This project implements industry-standard MLOps practices:

### 1. **Experiment Tracking**
- All experiments logged to MLflow
- Hyperparameters, metrics, and artifacts tracked
- Model comparison and selection

### 2. **Model Versioning**
- Models registered in MLflow Model Registry
- Version control for models
- Easy rollback to previous versions

### 3. **Data Versioning**
- DVC for data version control
- Reproducible data pipelines
- Remote storage integration (S3)

### 4. **Pipeline Orchestration**
- Automated ML pipeline with DVC
- Dependency management between stages
- Reproducible workflows

### 5. **Containerization**
- Docker for consistent environments
- Docker Compose for multi-container setup
- Production-ready deployment

### 6. **Cloud Integration**
- AWS EC2 for compute
- Amazon S3 for artifact storage
- IAM-based secure access

### 7. **API Design**
- RESTful API architecture
- JSON request/response format
- Error handling and logging

---

## 📊 Results

### Model Performance

| Metric    | Train Set | Test Set |
|-----------|-----------|----------|
| Accuracy  | ~95%      | ~92%     |
| Precision | ~94%      | ~91%     |
| Recall    | ~95%      | ~92%     |
| F1-Score  | ~94%      | ~91%     |

### Key Insights

- ✅ LightGBM with TF-IDF achieves high accuracy
- ✅ N-gram features (1-3) capture context effectively
- ✅ Retaining sentiment-critical stopwords improves performance
- ✅ Model generalizes well to unseen data

---

## 🔮 Future Enhancements

### Technical Improvements
- [ ] Implement CI/CD pipeline (GitHub Actions)
- [ ] Add Kubernetes deployment
- [ ] Integrate Prometheus for monitoring
- [ ] Add Grafana dashboards
- [ ] Implement A/B testing framework
- [ ] Add model drift detection

### Feature Enhancements
- [ ] Multi-language support
- [ ] Real-time streaming predictions
- [ ] Aspect-based sentiment analysis
- [ ] Emotion detection (beyond sentiment)
- [ ] Sarcasm detection
- [ ] User authentication and rate limiting

### Model Improvements
- [ ] Experiment with transformer models (BERT, RoBERTa)
- [ ] Ensemble methods
- [ ] Active learning pipeline
- [ ] Automated hyperparameter tuning (Optuna)

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Your Name**
- GitHub: [@ranjan83711](https://github.com/ranjan83711)
- LinkedIn: [Your LinkedIn](https://www.linkedin.com/in/ranjan-kumar-yadav-05b62a231/)
- Email: [EMAIL_ADDRESS](ranjan83711yadav@gmail.com)

---

## 🙏 Acknowledgments

- YouTube Data API for comment data
- MLflow community for excellent documentation
- DVC team for data versioning tools
- LightGBM developers
- Flask and Python communities

---

## 📞 Contact

For questions or feedback, please open an issue or reach out via email.

---

<div align="center">

**⭐ Star this repository if you found it helpful!**

Made with ❤️ and Python

</div>
