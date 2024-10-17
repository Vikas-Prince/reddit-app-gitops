# Reddit App on AWS EKS - Kubernetes Manifests

Welcome to the **Kubernetes Manifest Files** repository for the Reddit application on AWS Elastic Kubernetes Service (EKS). This repository contains the Kubernetes manifest files required for deploying the Reddit app. By using these manifests with ArgoCD, you can achieve automated deployments without needing to configure Jenkins.

## Overview

This repository focuses on providing the necessary Kubernetes manifests to deploy the Reddit application on AWS EKS. By leveraging ArgoCD, any changes made to these manifests will automatically trigger deployments, allowing for quick and efficient updates.

## Features

- **Automated Deployments**: Integrated with ArgoCD for seamless automatic deployments upon manifest changes.
- **Kubernetes Manifests**: Clearly structured YAML files for easy deployment and management of the Reddit application.

## Prerequisites

Before you begin, ensure you have the following:

- An AWS account with permissions to create and manage EKS clusters.
- `kubectl` installed and configured to access your EKS cluster.
- [ArgoCD](https://argo-cd.readthedocs.io/en/stable/getting_started/) installed and running in your Kubernetes cluster.
- Basic understanding of Kubernetes and ArgoCD.

## Installation

### 1. Configure AWS EKS

Follow AWS documentation to create and configure your EKS cluster if you haven’t done so already.

### 2. Steps to install ArgoCD

1. **Create a Namespace for ArgoCD:**

```bash
kubectl create namespace argocd
```

2. **Apply the ArgoCD Manifest File:**

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.4.7/manifests/install.yaml
```

3. **Get the ArgoCD Server Service:**

```bash
kubectl get svc -n argocd
```

4. **Edit the ArgoCD Server Service to Change it to LoadBalancer:**

```bash
kubectl edit svc argocd-server -n argocd
```

- In the editor, change the type from ClusterIP to LoadBalancer and save the changes.

5. **Check the Secret File for the Default Admin Password:**

```bash
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 --decode
```

- After these steps, you should have ArgoCD running and accessible via the LoadBalancer IP.

## Usage

1. Once ArgoCD is set up, navigate to the ArgoCD UI.
2. Create a project and sync it with your GitHub repository.
3. Sync your application to deploy the Reddit app.
4. Monitor the application status through the ArgoCD dashboard using the default cluster.

## Updating Manifest Files

To update the Reddit application:

1. Modify the desired manifest files in this repository.
2. Commit and push the changes to the repository.
3. ArgoCD will automatically detect the changes and redeploy the application.

## Source Code Repository

For the source code of the Reddit application, please refer to the main repository: [Reddit App on AWS EKS](https://github.com/Vikas-Prince/Reddit-App-on-AWS-EKS.git).

## Contributing

Contributions are welcome! If you have suggestions for improvements or want to add features, feel free to open an issue or submit a pull request.
