# Simple Todo API

A robust, containerized Todo application built with Python and FastAPI, designed to demonstrate modern DevOps practices including structured logging, observability with Prometheus, and Kubernetes deployment.

## 🚀 Features

- **RESTful API**: Complete CRUD operations for Todo management.
- **FastAPI**: High performance, easy to learn, fast to code, ready for production.
- **Observability**:
  - **Prometheus Metrics**: Built-in `/metrics` endpoint for monitoring.
  - **Structured Logging**: JSON-formatted logs for easy parsing and analysis.
  - **Tracing**: Request ID tracking and processing time headers (`X-Request-ID`, `X-Process-Time`).
- **Containerization**: Optimized `Dockerfile` for efficient building and running.
- **Kubernetes Ready**: Pre-configured manifests for easy deployment.

## 🛠️ Tech Stack

- **Language**: Python 3.9+
- **Framework**: FastAPI
- **Server**: Uvicorn
- **Container**: Docker
- **Orchestration**: Kubernetes

## 🏁 Getting Started

### Prerequisites

- Python 3.9 or higher
- Docker (optional)
- Kubernetes (optional, e.g., Minikube, Docker Desktop)

### 🐍 Local Development

1. **Clone the repository:**

   ```bash
   git clone https://github.com/asmamest/Devops.git
   cd "final project devops"
   ```

2. **Create a virtual environment:**

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application:**

   ```bash
   uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
   ```

   The API will be available at `http://localhost:8000`.

### 🐳 Docker Support

1. **Build the Docker image:**

   ```bash
   docker build -t simple-todo-app .
   ```

2. **Run the container:**
   ```bash
   docker run -p 8000:8000 simple-todo-app
   ```

### ☸️ Kubernetes Deployment

Deploy the application to your Kubernetes cluster using the provided manifests.

```bash
kubectl apply -f k8s/
```

Verify the deployment:

```bash
kubectl get pods
kubectl get services
```

## 📚 API Documentation

Once the application is running, you can access the interactive API documentation:

- **Swagger UI**: `http://localhost:8000/docs`
- **ReDoc**: `http://localhost:8000/redoc`

## 📊 Monitoring

Prometheus metrics are exposed at the `/metrics` endpoint.

```bash
curl http://localhost:8000/metrics
```

## 🧪 Testing

Run the test suite using pytest:

```bash
pytest
```
