# 🧩 Kubernetes Starter Guide

A concise reference for getting started with **Kubernetes**, **Minikube**, and **kubectl** — ideal for local testing and basic deployments.

---

## 📘 Terms

### **Namespaces**
Namespaces are used to separate and organize resources (like services, deployments, and pods) within a Kubernetes cluster.  
They allow for logical isolation between environments (e.g., `dev`, `staging`, `prod`).

---

## 🚀 Minikube Commands

Minikube runs a single-node Kubernetes cluster locally for testing and development.

```bash
# Check Minikube status
$ minikube status

# Start Minikube cluster
$ minikube start
```

---

## ⚙️ Kubectl Basics

`kubectl` is the command-line tool to interact with the Kubernetes API.

```bash
# List all running pods
$ kubectl get pod

# List cluster nodes
$ kubectl get nodes

# List running services
$ kubectl get services

# List ReplicaSets (includes old pods)
$ kubectl get replicaset
```

---

## 🧱 Deployments

A **Deployment** is an abstraction over pods that manages their creation, scaling, and rolling updates.

### CLI-Based Deployment

```bash
# List all deployments
$ kubectl get deployment

# Create a deployment using an image (e.g., nginx)
$ kubectl create deployment my-nginx --image=nginx

# Edit a specific deployment
$ kubectl edit deployment my-nginx

# View logs of a deployment
$ kubectl logs my-nginx

# Describe details of a specific pod
$ kubectl describe pod <pod-name>

# Delete a deployment
$ kubectl delete deployment my-nginx
```

---

## 🧾 YAML-Based Deployment

You can define deployments declaratively using YAML files.

```bash
# Apply a YAML configuration
$ kubectl apply -f deployment.yaml

# Apply a config in a specific namespace
$ kubectl apply -f mysql-configmap.yaml --namespace=my-namespace
```

### Example: NGINX Deployment + Service

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
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
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
  type: NodePort
```

---

## 🌐 Ingress

Ingress is used to expose HTTP and HTTPS routes from outside the cluster to services within it.  
It provides load balancing, SSL termination, and name-based virtual hosting.

*(Add ingress commands and examples as you learn more.)*

---

## 🧭 Tips

- Always use **namespaces** for organized environments.  
- Use `kubectl describe` for debugging and understanding resource behavior.  
- Use `kubectl delete -f <file>` to remove resources defined in a YAML.  
- Combine Minikube dashboard for a visual overview:  
  ```bash
  $ minikube dashboard
  ```

---

### 🧑‍💻 Author
Created by **Asadullah Al Galib**  
A practical quick-reference for Kubernetes beginners and local dev setups.
