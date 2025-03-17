# Koku Helm Chart Deployment

[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/koku)](https://artifacthub.io/packages/search?repo=koku)

## About Koku
Koku is a cloud-native application designed to simplify cost management and monitoring in Kubernetes environments. It provides insights into resource utilization, helping organizations optimize their cloud spending efficiently. Koku integrates seamlessly with AWS and Kubernetes, enabling real-time cost tracking and analysis.

## Prerequisites

Ensure you have the following installed before proceeding:
- [Helm](https://helm.sh/docs/intro/install/)
- Kubernetes cluster configured
- AWS credentials


> [!CAUTION]
> If you want to make the database persistant, use a RDS postgres database.

## Installation Steps

### 1. Add Koku Helm Repository

```sh
helm repo add koku https://skyu-io.github.io/koku-helm-chart
```

### 2. Update Helm Repositories

```sh
helm repo update
```

### 3. Install Koku

Replace `<your-aws-access-key-id>` and `<your-aws-secret-access-key>` with your actual AWS credentials.

```sh
helm install koku koku/koku \
  --set credentials.awsAccessKeyId="<your-aws-access-key-id>" \
  --set credentials.awsSecretAccessKey="<your-aws-secret-access-key>" \
  --namespace koku --create-namespace
```

## Verification

After installation, check if the deployment was successful:

```sh
kubectl get pods -n koku
```

You should see running pods associated with Koku.

## Uninstalling Koku

To uninstall Koku and remove all associated resources, run:

```sh
helm uninstall koku -n koku
```


## Port-forwarding the Koku server

```sh
kubectl port-forward svc/koku-server -n koku 8000
```
