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

## 🔒 Security

### SAST (Static Application Security Testing)
The project uses **Bandit** to scan the codebase for security vulnerabilities:
- Runs automatically in the CI/CD pipeline
- Scans the `app/` directory for common security issues
- Executes on every push and pull request

### DAST (Dynamic Application Security Testing)
The project uses **OWASP ZAP** to scan the running API for security vulnerabilities:
- Runs automatically after Docker image is built
- Performs baseline security scan against the deployed API
- Generates detailed HTML security reports
- Reports available as GitHub Actions artifacts

**To access DAST reports:**
1. Go to the [Actions tab](https://github.com/asmamest/Devops/actions) on GitHub
2. Click on the latest workflow run
3. Download the `zap-scan-report` artifact
4. Open `zap-report.html` to view security findings

**To run DAST locally:**
```bash
# Start the application
docker run -d -p 8000:8000 --name todo-api simple-todo-app

# Run OWASP ZAP scan
docker run -v ${PWD}:/zap/wrk/:rw -t zaproxy/zap-stable \
  zap-baseline.py -t http://host.docker.internal:8000 \
  -r zap-report.html -I

# Stop the application
docker stop todo-api && docker rm todo-api

# View the report
start zap-report.html
```

## 🧪 Testing

Run the test suite using pytest:

```bash
pytest
```
