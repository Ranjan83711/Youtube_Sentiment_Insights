# Docker Deployment Guide

## Quick Start

### Using Docker Compose (Recommended)

```bash
# Build and start the container
docker-compose up -d

# View logs
docker-compose logs -f

# Stop the container
docker-compose down
```

### Using Docker CLI

```bash
# Build the image
docker build -t youtube-sentiment-app .

# Run the container
docker run -d \
  --name youtube-sentiment-app \
  -p 5000:5000 \
  -e MLFLOW_TRACKING_URI=http://54.90.172.25:5000 \
  youtube-sentiment-app

# View logs
docker logs -f youtube-sentiment-app

# Stop the container
docker stop youtube-sentiment-app

# Remove the container
docker rm youtube-sentiment-app
```

## Important Notes

### Model Files
Make sure the following files exist before building:
- `lgbm_model.pkl` (in root or flask_app directory)
- `tfidf_vectorizer.pkl` (in root or flask_app directory)

### MLflow Connection
The app connects to MLflow at `http://54.90.172.25:5000`. Make sure:
1. The MLflow server is accessible
2. The model "my_model" version "1" exists in the registry
3. Network connectivity is available

### Port Configuration
The app runs on port 5000 by default. To use a different port:

```bash
# Using Docker
docker run -d -p 8080:5000 youtube-sentiment-app

# Using Docker Compose (edit docker-compose.yml)
ports:
  - "8080:5000"
```

## Testing the Deployment

```bash
# Health check
curl http://localhost:5000/

# Test prediction endpoint
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"comments": ["This is great!", "I hate this"]}'
```

## Troubleshooting

### Container won't start
```bash
# Check logs
docker logs youtube-sentiment-app

# Check if port is already in use
netstat -ano | findstr :5000
```

### Model loading issues
- Verify model files exist in the correct location
- Check MLflow server connectivity
- Ensure model name and version are correct

### Memory issues
```bash
# Run with memory limit
docker run -d --memory="2g" -p 5000:5000 youtube-sentiment-app
```

## Production Deployment

For production, consider:
1. Using a reverse proxy (nginx)
2. Setting up SSL/TLS
3. Using environment variables for sensitive data
4. Implementing proper logging and monitoring
5. Using a production WSGI server (gunicorn)

### Example with Gunicorn

Update Dockerfile CMD:
```dockerfile
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "--workers", "4", "flask_app.app:app"]
```

Add to requirements.txt:
```
gunicorn
```
