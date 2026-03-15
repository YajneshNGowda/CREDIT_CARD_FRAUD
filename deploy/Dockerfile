# Credit Card Fraud Detection Service
FROM python:3.10-slim

WORKDIR /app

# Install dependencies
COPY requirements_deploy.txt .
RUN pip install --no-cache-dir -r requirements_deploy.txt

# Copy model artifact and API code
COPY fraud_model_artifact.pkl .
COPY app.py .

# Environment
ENV MODEL_PATH=/app/fraud_model_artifact.pkl
ENV PORT=8000

EXPOSE 8000

HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
    CMD curl -f http://localhost:8000/ || exit 1

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000", "--workers", "2"]
