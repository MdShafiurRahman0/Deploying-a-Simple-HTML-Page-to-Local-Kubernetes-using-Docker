# Deploying a Simple HTML Page to Local Kubernetes using Docker

> A beginner-friendly project demonstrating how to build a Docker image from a local HTML file, push it to Docker Hub, and deploy it on a local Kubernetes (Minikube) cluster.

---

# 🌍 English Version

## 📖 Project Overview

The objective of this project is to demonstrate the complete lifecycle of containerizing a simple web application and deploying it to a local Kubernetes cluster.

In this project we:

1. Create a simple **HTML webpage**
2. Build a **Docker image** from that webpage
3. Push the image to **Docker Hub**
4. Deploy the container using **Kubernetes (Minikube)**
5. Access the application through a **NodePort service**

---

# 📂 Project Structure

```
docker-kubernetes-1-project/
├── index/
│   ├── Dockerfile
│   └── index.html
├── deployment.yaml
└── service.yaml
```

---

# 1️⃣ Application Code (index/index.html)

```
<!DOCTYPE html>
<html>
<body>
    <h1>Hello from Docker!</h1>
    <p>This is my first Docker project.</p>
</body>
</html>
```

---

# 2️⃣ Docker Configuration (index/Dockerfile)

```
FROM nginx: alpine
COPY index.html /usr/share/nginx/html/
```

This Dockerfile uses a lightweight **Nginx Alpine image** and copies the local HTML file into the Nginx web directory.

---

# 🚀 Step-by-Step Implementation

---

# Step 1: Build Docker Image from Local HTML

Navigate to the project directory:

```
cd docker-kubernetes-1-project/index
```

Build the Docker image:

```
docker build -t shafiur22/my-first-app:latest .
```

Verify the image:

```
docker images
```

---

# Step 2: Docker Hub Authentication

Before pushing the image, login to Docker Hub:

```
docker login
```

Terminal Output:

```
Authenticating with existing credentials... [Username: shafiur22]
Login Succeeded
```

---

# Step 3: Push Image to Docker Hub

Push the Docker image to Docker Hub:

```
docker push shafiur22/my-first-app:latest
```

Now anyone can pull the image using:

```
docker pull shafiur22/my-first-app:latest
```

---

# 3️⃣ Kubernetes Deployment (deployment.yaml)

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-first-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-first-app
  template:
    metadata:
      labels:
        app: my-first-app
    spec:
      containers:
      - name: my-first-app
        image: shafiur22/my-first-app:latest
        ports:
        - containerPort: 80
```

This deployment instructs Kubernetes to run **1 replica of the container** using the Docker Hub image.

---

# 4️⃣ Kubernetes Service (service.yaml)

```
apiVersion: v1
kind: Service
metadata:
  name: my-first-app-service
spec:
  type: NodePort
  selector:
    app: my-first-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30007
```

This service exposes the application using **NodePort** so it can be accessed externally.

---

# Step 4: Deploy Application to Kubernetes

Apply the deployment:

```
kubectl apply -f deployment.yaml
```

Apply the service:

```
kubectl apply -f service.yaml
```

Check running pods:

```
kubectl get pods
```

Example Output:

```
NAME                           READY   STATUS
my-first-app-7776c7865-kjnmf   1/1     Running
```

---

# Step 5: Access the Service

Generate the service URL using:

```
minikube service my-first-app-service
```

Example output:

```
http://192.168.49.2:30007
```

---

# Step 6: Port Forwarding (Access Outside VM)

Since Minikube runs inside a Virtual Machine, we use port-forward:

```
kubectl port-forward --address 0.0.0.0 service/my-first-app-service 30007:80
```

Terminal Output:

```
Forwarding from 0.0.0.0:30007 -> 80
```

---

# 🎉 Final Result

The containerized webpage is successfully deployed and accessible at:

```
http://100.119.65.50:30007
```

The webpage displays:

```
Hello from Docker!
This is my first Docker project.
```

---

# 🇧🇩 বাংলা সংস্করণ (Bangla Version)

## 📖 প্রজেক্টের সারসংক্ষেপ

এই প্রজেক্টটির উদ্দেশ্য হলো একটি সাধারণ HTML ওয়েবপেজকে Docker container এ রূপান্তর করা এবং সেই container টি Kubernetes (Minikube) ব্যবহার করে লোকাল সার্ভারে রান করা।

এই প্রজেক্টে আমরা:

1. একটি সাধারণ **HTML ওয়েবপেজ তৈরি করেছি**
2. সেটি থেকে একটি **Docker image তৈরি করেছি**
3. Docker Hub এ image আপলোড করেছি
4. Kubernetes ব্যবহার করে container deploy করেছি
5. NodePort service দিয়ে ব্রাউজারে অ্যাপটি দেখেছি

---

# 📂 প্রজেক্ট ফোল্ডার স্ট্রাকচার

```
docker-kubernetes-1-project/
├── index/
│   ├── Dockerfile
│   └── index.html
├── deployment.yaml
└── service.yaml
```

---

# 🚀 কাজের ধাপসমূহ

---

# ধাপ ১: HTML ফাইল থেকে Docker Image তৈরি

প্রজেক্ট ফোল্ডারে যান:

```
cd docker-kubernetes-1-project/index
```

Docker image build করুন:

```
docker build -t shafiur22/my-first-app:latest .
```

Image তৈরি হয়েছে কিনা দেখুন:

```
docker images
```

---

# ধাপ ২: Docker Hub লগইন

Docker Hub এ লগইন করুন:

```
docker login
```

টার্মিনাল আউটপুট:

```
Login Succeeded
```

---

# ধাপ ৩: Docker Hub এ Image আপলোড

Docker image push করুন:

```
docker push shafiur22/my-first-app:latest
```

যে কেউ চাইলে নিচের কমান্ড দিয়ে image pull করতে পারবে:

```
docker pull shafiur22/my-first-app:latest
```

---

# ধাপ ৪: Kubernetes Deployment চালু করা

Deployment apply করুন:

```
kubectl apply -f deployment.yaml
```

Service apply করুন:

```
kubectl apply -f service.yaml
```

Pods চেক করুন:

```
kubectl get pods
```

---

# ধাপ ৫: Service Access করা

Service URL বের করতে:

```
minikube service my-first-app-service
```

---

# ধাপ ৬: Port Forwarding

VM এর বাইরে থেকে অ্যাপটি দেখতে:

```
kubectl port-forward --address 0.0.0.0 service/my-first-app-service 30007:80
```

---

# 🎉 চূড়ান্ত ফলাফল

পোর্ট ফরওয়ার্ড করার পরে অ্যাপটি ব্রাউজারে লাইভ দেখা যাবে:

```
http://100.119.65.50:30007
```

এখানে ওয়েবপেজে দেখাবে:

```
Hello from Docker!
This is my first Docker project.
```

---
