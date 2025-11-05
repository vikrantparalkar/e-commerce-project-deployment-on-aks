# E-Commerce Application on AKS

This project deploys the "Robot Shop" e-commerce application to Azure Kubernetes Service (AKS).

## 
Project Overview

* **Application:** This is a 3-tier application composed of 8 microservices (e.g., `cart`, `catalogue`, `mysql`, `mongodb`, etc.).
* **Helm Chart:** All Kubernetes manifests are packaged as a Helm chart, located in the **`AKS/helm`** directory.
* **Docker Images:** The project uses pre-built Docker images hosted on Docker Hub.

### 
Architecture Note

The container images are built for the **`linux/amd64`** (x86-64) architecture. Your AKS cluster's node pool **must** use `amd64` VMs to run this project.

---

## 
Prerequisites

You will need the following tools installed:
* Azure CLI
* `kubectl`
* Helm

---

## 
Basic Deployment Steps

1.  **Log in to Azure:** Use the `az login` command.
2.  **Create AKS Cluster:** Create a new AKS cluster. (Ensure you select an `amd64` VM size for the node pool, like `Standard_D2s_v3`).
3.  **Connect to Cluster:** Use `az aks get-credentials` to connect `kubectl` to your new cluster.
4.  **Deploy:**
    * Navigate to the `AKS/helm` directory.
    * Create the `robot-shop` namespace (`kubectl create namespace robot-shop`).
    * Run `helm install robot-shop . --namespace robot-shop` to deploy the application.

### 
Verify

Once deployed, use `kubectl get svc -n robot-shop` to find the `EXTERNAL-IP` of the `web` service. Paste this IP into your browser to view the application.
