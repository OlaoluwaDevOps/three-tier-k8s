# Three-Tier Web App with Kubernetes (K3s) on AWS EC2

A production-grade three-tier web application deployed on 
Kubernetes using K3s on AWS EC2 Free Tier.

## Live Architecture
## Tiers
- Tier 1: Frontend — Nginx serving HTML/CSS/JS on port 30080
- Tier 2: Backend — Node.js + Express REST API on port 30500
- Tier 3: Database — MongoDB for data persistence

## Tech Stack
- AWS EC2 t2.micro Ubuntu 24.04 (Free Tier)
- K3s (Lightweight Kubernetes)
- Docker
- Nginx
- Node.js 18 + Express
- MongoDB 6.0
- kubectl

## Challenges Solved
- Fixed Jenkins GPG key error on Ubuntu 24.04
- Resolved Kubernetes disk-pressure taint on t2.micro
- Expanded EBS volume from 8GB to 15GB to support K3s
- Freed disk space by removing snap and kernel headers
- Successfully imported Docker images into K3s containerd

## Kubernetes Resources
- 3 Deployments: frontend, backend, mongodb
- 3 Services: frontend NodePort 30080, backend NodePort 30500,
  mongodb ClusterIP
- 1 Secret: MongoDB credentials

## How to Deploy
```bash
kubectl apply -f k8s/mongodb-secret.yaml
kubectl apply -f k8s/mongodb-deployment.yaml
kubectl apply -f k8s/mongodb-service.yaml
kubectl apply -f k8s/backend-deployment.yaml
kubectl apply -f k8s/backend-service.yaml
kubectl apply -f k8s/frontend-deployment.yaml
kubectl apply -f k8s/frontend-service.yaml
```

## Check Status
```bash
kubectl get pods
kubectl get services
```

## API Endpoints
- GET  /          → Backend status
- GET  /health    → Health check
- GET  /api/items → Get all items
- POST /api/items → Add new item

## Access
- Frontend: http://your-server-ip:30080
- Backend:  http://your-server-ip:30500
