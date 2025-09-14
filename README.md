# 🚀 Deploy NGINX Web App on Kubernetes with Minikube

[![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Minikube](https://img.shields.io/badge/Minikube-7B7B7B?style=for-the-badge)](https://minikube.sigs.k8s.io/docs/)

A step-by-step guide to deploy an **NGINX-based Docker application** to a local Kubernetes cluster using **Minikube** and **kubectl**.

---

## 📑 Table of Contents

1. [Step 1: Install Docker](#-step-1-install-docker)  
2. [Step 2: Install Minikube](#-step-2-install-minikube)  
3. [Step 3: Install kubectl](#-step-3-install-kubectl-kubernetes-cli)  
4. [Step 4: Start Minikube](#-step-4-start-minikube-with-docker-driver)  
5. [Step 5: Create Deployment & Service](#-step-5-create-kubernetes-deployment--service-nginx)  
6. [Step 6: Deploy to Kubernetes](#-step-6-deploy-to-kubernetes)  
7. [Step 7: Access Your Nginx App](#-step-7-access-your-nginx-app)  
8. [Step 8: Troubleshooting](#-step-8-troubleshooting-commands)  
9. [Step 9: Cleanup](#-step-9-cleanup-optional)  
10. [Architecture Diagram](#-nginx-deployment-architecture)  

---

## 🐳 Step 1: Install Docker

If Docker is not installed yet:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
## ⚙️ Step 2: Install Minikube

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

2. **Step 3: Install kubectl**
```markdown
## 🔧 Step 3: Install kubectl (Kubernetes CLI)

```bash
curl -LO "https://dl.k8s.io/release/$(curl -Ls https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

3. **Step 4: Start Minikube**
```markdown
## 🚀 Step 4: Start Minikube with Docker Driver

Start the Minikube cluster:

```bash
minikube start --driver=docker

4. **Step 5: Create Deployment & Service (NGINX)**
```markdown
## 🛠️ Step 5: Create Kubernetes Deployment & Service (NGINX)

Create a new YAML file:

```bash
nano my-app.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80

---

apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  type: NodePort
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080

5. **Step 6: Deploy to Kubernetes**
```markdown
## 📦 Step 6: Deploy to Kubernetes

Apply the deployment:

```bash
kubectl apply -f my-app.yaml

6. **Step 7: Access Your Nginx App**
```markdown
## 🌐 Step 7: Access Your Nginx App

Get the Minikube IP:

```bash
minikube ip

7. **Step 8: Troubleshooting**
```markdown
## 🧪 Step 8: Troubleshooting Commands

Check pod logs:

```bash
kubectl logs <POD_NAME>

8. **Step 9: Cleanup**
```markdown
## 🧹 Step 9: Cleanup (Optional)

Delete all Kubernetes resources:

```bash
kubectl delete -f my-app.yaml

9. **Step 10: Architecture Diagram**
```markdown
## 🖼️ NGINX Deployment Architecture

```mermaid
flowchart TD
    subgraph Minikube Node
        direction TB
        Pod1[Pod: my-app (NGINX)] -->|Port 80| Service[Service: my-app-service]
        Pod2[Pod: my-app (NGINX)] -->|Port 80| Service
        Service -->|NodePort 30080| MinikubeIP[Minikube IP]
    end

    Browser[Browser/User] -->|HTTP Request| MinikubeIP
Browser/User
     |
     v
Minikube IP (NodePort 30080)
     |
     v
Service: my-app-service
     |
     +--> Pod: my-app (NGINX)
     +--> Pod: my-app (NGINX)

---

### ✅ Final Step
Once you’ve pasted **all sections**, click **Commit changes** on GitHub.  
Your README will now display:

- Step-by-step instructions  
- Code blocks  
- Badges  
- Mermaid diagram (or ASCII fallback)  

---
