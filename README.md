# Kubernetes-5-Tier-Microservices-Architecture

## 📌 Overview
This project demonstrates the deployment of a scalable, multi-tier microservices architecture using Kubernetes. It orchestrates a 5-tier distributed application, showcasing the seamless integration of stateless web frontends, a message broker, a background worker, and a stateful database within a unified cluster. 

This repository highlights practical container orchestration, service networking (`ClusterIP` and `NodePort`), and deployment management.

## ✅ Prerequisites
Ensure you have the following installed and running on your local machine:
* [Docker](https://docs.docker.com/get-docker/)
* [Minikube](https://minikube.sigs.k8s.io/docs/start/)
* [kubectl](https://kubernetes.io/docs/tasks/tools/)

Before deploying, ensure you have pulled the required application image:
```bash
docker pull kodekloud/examplevotingapp_result:latest

```

## 🏗️ Architecture

The application consists of five distinct microservices communicating within the cluster:

* **Voting App (Python):** The frontend interface for users to cast their votes.
* **Redis:** An in-memory queue that temporarily holds the incoming votes.
* **Worker (.NET):** A background service that processes votes from the Redis queue and safely writes them to the database.
* **Database (PostgreSQL):** The persistent, stateful storage for the final vote tally.
* **Result App (React.js):** A real-time frontend dashboard displaying the current voting results.


*(Note: Ensure this image is uploaded to the root of your repository).*

## 🛠️ Technologies Used

* **Container Orchestration:** Kubernetes
* **Local Cluster:** Minikube
* **Application Stack:** Python, React.js, .NET, Redis, PostgreSQL
* **Containerization:** Docker
* **Configuration:** YAML (Deployments, Pods, Services)

## 🚀 Deployment Guide

### Steps to Deploy

**Note**: The pods/ directory is included for reference purposes only. You do not need to deploy these files, as the pods are managed by the configurations in the deployment/ folder.

1. **Clone the repository:**
```bash
git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
cd your-repo-name

```


2. **Start the Minikube cluster:**
```bash
minikube start

```


3. **Deploy the application components:**
Apply the YAML configurations to create the deployments and services.
```bash
kubectl apply -f deployment/
kubectl apply -f service/

```

4. **Verify the cluster status:**
Check that all pods are `Running` and services have been correctly assigned their IPs and Ports.
```bash
kubectl get all -o wide

```



### 🌐 Accessing the Application

The internal services (Redis, PostgreSQL) are secured behind `ClusterIP` services, while the frontends are exposed via `NodePort`. Use the following commands to get the access URLs:

**To open the Voting interface:**

```bash
minikube service vote --url

```

**To open the Results dashboard:**

```bash
minikube service result --url

```
