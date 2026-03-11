# Deploying a Simple HTML Page to Local Kubernetes using Docker



## 📖 Project Overview
The objective of this project is to demonstrate the complete lifecycle of containerizing a simple web application and deploying it to a local Kubernetes cluster. It is designed to be easily understood by anyone, regardless of their technical background. 

We start by building a Docker image locally from a basic HTML file, push that image to a public Docker Hub repository, and finally instruct a local Kubernetes environment (Minikube) to pull and run the application.

---

## 🛠️ Prerequisites
To understand or reproduce this project, the following tools were used:
* **Docker:** To build and package the local HTML code into an image.
* **Docker Hub Account:** A cloud registry to store our built image.
* **Minikube:** To run a single-node Kubernetes cluster on a local machine.
* **kubectl:** The command-line tool used to send instructions to Kubernetes.

---

## 🚀 Step-by-Step Implementation Guide

### Step 1: Writing the Code and Dockerfile
We started by creating a simple `index.html` file to serve as our web page. Then, we created a `Dockerfile` in the same directory. This file acts as a recipe, telling Docker to use an Nginx web server and copy our HTML file into it.

> **[Insert SS here: Screenshot showing the project folder structure, `index.html` code, and `Dockerfile` code]**

### Step 2: Building the Docker Image Locally
Using the terminal, we built the Docker image directly on our local machine using the `docker build` command. 

> **[Insert SS here: Screenshot of the terminal showing the successful Docker build process]**

### Step 3: Pushing the Image to Docker Hub
Once the image was built locally, we tagged it with our Docker Hub username and uploaded (pushed) it to the cloud using `docker push`. This makes the image available for Kubernetes to download later.

> **[Insert SS here: Screenshot of the terminal showing the successful push command, or the image listed in the Docker Hub web dashboard]**

### Step 4: Starting the Local Kubernetes Cluster
We prepared our local server environment by starting Minikube using the `minikube start` command.

> **[Insert SS here: Screenshot of the terminal showing Minikube successfully starting]**

### Step 5: Creating the Kubernetes Deployment
We created a configuration file named `deployment.yaml`. This file instructs Kubernetes to pull our previously uploaded image from Docker Hub and run it inside a "Pod" (a small, isolated container environment).

> **[Insert SS here: Screenshot of the `deployment.yaml` code and the terminal showing `kubectl get pods` with the status 'Running']**

### Step 6: Exposing the Application via a Service
To make the running application accessible from a web browser, we created a `service.yaml` file. We used a `NodePort` service, which acts as a bridge between the internal Kubernetes network and the outside world.

> **[Insert SS here: Screenshot of the `service.yaml` code and the terminal showing `kubectl get svc` with the assigned port numbers]**

### Step 7: Viewing the Live Project
Finally, using port forwarding (or Minikube's local IP), we accessed the deployed application live in our web browser.

> **[Insert SS here: Screenshot of your web browser displaying the "Hello from Docker!" page, ensuring the address bar with the IP/Port is visible]**

---

## 📌 Project Architecture Flow
1. **Code:** Write HTML locally.
2. **Build:** Create Docker image on the local machine.
3. **Push:** Upload the local image to Docker Hub.
4. **Deploy:** Apply Kubernetes Deployment & Service configurations.
5. **Run:** Kubernetes pulls the image from the Hub and serves the website locally.
