![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestration-326CE5?logo=kubernetes&logoColor=white)
![Minikube](https://img.shields.io/badge/Minikube-Local%20Cluster-orange?logo=minikube&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?logo=docker&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-InMemory-DC382D?logo=redis&logoColor=white)
![Postgres](https://img.shields.io/badge/Postgres-Database-4169E1?logo=postgresql&logoColor=white)

# 🗳️ Kubernetes Voting App

A complete microservices-based voting application running on **Kubernetes (Minikube)**.

---

## ✅ Architecture Diagram (ASCII)

    ┌────────────────────┐
    │   Voting App (UI)  │
    │   NodePort: 30004  │
    └───────────┬────────┘
                │ POST vote
                ▼
        ┌────────────┐
        │    Redis    │
        │  ClusterIP  │
        └──────┬──────┘
               │ Worker reads
               ▼
    ┌──────────────────────┐
    │      Worker App      │
    │  (Background Logic)  │
    └──────────┬───────────┘
               │ INSERT
               ▼
        ┌────────────┐
        │  Postgres   │
        │  ClusterIP  │
        └──────┬──────┘
               │ SELECT
               ▼
    ┌────────────────────┐
    │   Result App (UI)  │
    │   NodePort: 30005  │
    └────────────────────┘

---

## ✅ Deployment Steps

1. Start Minikube  
       minikube start  

2. Apply YAML files  
       kubectl apply -f .  

3. Check resources  
       kubectl get pods  
       kubectl get svc  
       kubectl get endpoints  

---

## ✅ Accessing the Apps

Voting App  
       minikube service voting-service --url  

Result App  
       minikube service result-service --url  

⚠️ Do not close terminal windows (Minikube tunnel closes)

---

## ✅ Troubleshooting

Endpoints missing  
       kubectl get endpoints voting-service  

Worker stuck on “Waiting for db”  
       POSTGRES_HOST=db  

Votes not updating  
       kubectl logs worker-app-pod  

---

## 📸 Screenshots

### Voting App
![Voting App Screenshot](voting-app.png)

### Results App
![Results App Screenshot](results-app.png)
