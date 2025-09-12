# K8s

//-------------------------------------------------------------------------------------------------------------------------//
 
 

# 🚀 Deploy NGINX Web App on Kubernetes with Minikube

A step-by-step guide to help you deploy an NGINX-based Docker application to a local Kubernetes cluster using **Minikube** and **kubectl**.

---

## 🐳 Step 1: Install Docker

If Docker is not installed yet:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```
Add your user to the docker group:

```bash
sudo usermod -aG docker $USER
newgrp docker
```
Verify Docker works:

bash
Copy code
docker run hello-world
⚙️ Step 2: Install Minikube
bash
Copy code
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
🔧 Step 3: Install kubectl (Kubernetes CLI)
bash
Copy code
curl -LO "https://dl.k8s.io/release/$(curl -Ls https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
🚀 Step 4: Start Minikube with Docker Driver
Start the Minikube cluster:

bash
Copy code
minikube start --driver=docker
Verify it’s working:

bash
Copy code
kubectl get nodes
You should see minikube with status Ready.

🛠️ Step 5: Create Kubernetes Deployment & Service (Nginx)
Create a new file:

bash
Copy code
nano my-app.yaml
Paste the following YAML configuration:

yaml
Copy code
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
Save and exit (Ctrl+O, Enter, Ctrl+X).

📦 Step 6: Deploy to Kubernetes
Apply the deployment:

bash
Copy code
kubectl apply -f my-app.yaml
Check if the pods are running:

bash
Copy code
kubectl get pods
Check if the service is created:

bash
Copy code
kubectl get svc
🌐 Step 7: Access Your Nginx App
Get the Minikube IP:

bash
Copy code
minikube ip
If the IP is 192.168.49.2, then your app is accessible at:

cpp
Copy code
http://192.168.49.2:30080
OR Use this shortcut to open directly in browser:

bash
Copy code
minikube service my-app-service
🧪 Step 8: Troubleshooting Commands
Check pod logs:

bash
Copy code
kubectl logs <POD_NAME>
Describe pod for errors:

bash
Copy code
kubectl describe pod <POD_NAME>
Verify labels match service selector:

bash
Copy code
kubectl get pods --show-labels
Look for app=my-app label on each pod.

🧹 Step 9: Cleanup (Optional)
To delete all Kubernetes resources:

bash
Copy code
kubectl delete -f my-app.yaml
To stop Minikube:

bash
Copy code
minikube stop
To delete the Minikube cluster completely:

bash
Copy code
minikube delete
✅ You’re Done!
Your NGINX app is live on Kubernetes using Docker and Minikube! 🎉
"""

Save to markdown file
Path("k8s-nginx-deployment.md").write_text(markdown_content)

yaml
Copy code

---

This will create a file called `k8s-nginx-deployment.md` in your current directory. You can then upload
