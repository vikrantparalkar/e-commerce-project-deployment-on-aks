# E-Commerce App Deployment on Kubernetes (AKS) 

This project deploys the "Robot Shop" e-commerce application to Azure Kubernetes Service (AKS) using Helm. All the necessary chart files are located in the `AKS/helm` folder.

## Deployment Process

1.  **Azure Setup:** You need an Azure account. Log in using the Azure CLI.
2.  **Create Cluster:** Create an AKS cluster in a new resource group.
3.  **Connect to Cluster:** Use the Azure CLI to get the credentials so `kubectl` (the Kubernetes tool) can talk to your new cluster.
4.  **Deploy App:** Navigate to the `AKS/helm` directory, create a new namespace, and then use a single `helm install` command to deploy the entire application.

## Key Fixes Included

The files in this repository are already modified to solve major problems:

* **CPU Architecture Error (`exec format error`):** The project is set up to use standard `amd64` (x86) nodes, which matches the existing `robotshop` images and prevents this crash.
* **Database Crashes (`CrashLoopBackOff`):** The database manifests (MongoDB and MySQL) are fixed to include the necessary passwords and storage configurations so they can start up correctly for testing.
