# k8s-monitoring-local
=======
# 🧭 Kubernetes Monitoring Demo

This project demonstrates how to deploy a **Python Flask web application** into a **local Kubernetes cluster** (like Minikube) with integrated **monitoring using Prometheus and Grafana**. It includes both:

- **Kubernetes YAML files**
- **Helm chart** for simplified deployment

---

## 📦 What's Included

### ✔️ Web App
- A simple Flask app that responds with a test message
- Dockerized for container deployment

### ✔️ Kubernetes Resources
- Deployment, Service for the Flask app
- Prometheus:
  - ConfigMap with scrape config
  - Deployment and Service
- (Grafana setup can be added next)

### ✔️ Helm Chart
- Templated deployment and service for the Flask app
- Values customizable for image, ports, and replicas

---

## 🚀 How to Run (Local Setup with Minikube)

### Prerequisites
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Helm](https://helm.sh/)
- [Docker](https://www.docker.com/)

### Step 1: Start Minikube
```bash
minikube start
```

### Step 2: Build Docker Image (inside Minikube Docker env)
```bash
eval $(minikube docker-env)
docker build -t flask-monitoring-demo .
```

### Step 3: Deploy App with Kubernetes YAMLs
```bash
kubectl apply -f k8s/local/
kubectl get all
```

### Step 4: Access the App
Get the NodePort for `flask-service`:
```bash
minikube service flask-service --url
```

---

## 📊 How to Access Prometheus

To access Prometheus in the browser:
```bash
minikube service prometheus --url
```

Then go to the URL shown and navigate to **Targets** to see scrape results.

---

## 🧪 How to Test the App

After deploying:
1. Run:
   ```bash
   curl $(minikube service flask-service --url)
   ```
2. Expected output:
   ```
   Hello from Kubernetes with Monitoring!
   ```

You can also check the logs:
```bash
kubectl logs deployment/flask-app
```
