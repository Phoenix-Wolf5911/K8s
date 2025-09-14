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
