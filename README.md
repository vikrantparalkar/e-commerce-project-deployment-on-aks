# E-Commerce Application on AKS

This project deploys the "Robot Shop" 3-tier e-commerce application to Azure Kubernetes Service (AKS).

## 
Project Overview

* **Application:** This is a 3-tier application composed of **8 microservices** (e.g., `cart`, `catalogue`, `mysql`, `mongodb`, `shipping`, etc.).
* **Docker:** Each microservice has its own `Dockerfile`. The pre-built container images are hosted on Docker Hub.
* **Helm Chart:** All Kubernetes manifests are packaged as a Helm chart, located in the **`AKS/helm`** directory.
* **Architecture:** The pre-built images are for the **`linux/amd64`** (x86-64) architecture. Your AKS cluster's node pool **must** use `amd64` VMs to run this project.

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

4.  **Deploy the App:**
    * Navigate to the `AKS/helm` directory.
    * Create the `robot-shop` namespace (`kubectl create namespace robot-shop`).
    * Run `helm install robot-shop . --namespace robot-shop` to deploy all 8 services.

5.  **Enable Ingress Controller:**
    * In the Azure Portal, go to your AKS cluster.
    * Under **Networking**, check the box to **"Enable Ingress controller"**. This will automatically deploy an Application Gateway Ingress Controller (AGIC).

6.  **Apply Ingress Rule:**
    * Wait for the Ingress controller to be ready.
    * From the `AKS/helm` directory, apply the `ingress.yaml` file to expose your application through the Ingress.
        ```bash
        kubectl apply -f ingress.yaml -n robot-shop
        ```

### 
Verify

Once deployed, use `kubectl get ingress -n robot-shop` to find the `ADDRESS` (the public IP) assigned to your application. Paste this IP into your browser to view the Robot Shop.
