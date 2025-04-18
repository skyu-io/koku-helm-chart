# Koku Helm Chart Deployment

[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/koku)](https://artifacthub.io/packages/search?repo=koku)

## About Koku
Koku is a cloud-native application designed to simplify cost management and monitoring in Kubernetes environments. It provides insights into resource utilization, helping organizations optimize their cloud spending efficiently. Koku integrates seamlessly with AWS and Kubernetes, enabling real-time cost tracking and analysis.

## Prerequisites

Ensure you have the following installed before proceeding:
- [Helm](https://helm.sh/docs/intro/install/)
- Kubernetes cluster configured
- AWS credentials
- Database Setup 

> [!NOTE]
> Create two new users, named `postgres` and `hive`, and assign secure passwords to each. Configure the necessary permissions, as below. Then, create two databases: `koku` for the `postgres` user and `hive` for the `hive` user.

![Screenshot from 2025-03-27 17-58-04](https://github.com/user-attachments/assets/a2a03ca6-5ce1-4fd2-bbf0-a568773a4382)
![Screenshot from 2025-03-27 17-58-11](https://github.com/user-attachments/assets/6ec17191-e428-45a4-9361-f4308584dce3)

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

Replace the following values with your actual values.

```sh
helm install koku koku/koku \
  --set credentials.awsAccessKeyId="<your-aws-access-key-id>" \
  --set credentials.awsSecretAccessKey="<your-aws-secret-access-key>" \
  --set database.postgresSQLServiceHost="<your-postgres-host>" \
  --set database.databaseName="<your-database-name>" \
  --set database.databaseUser="<your-database-user-name>" \
  --set database.databaseAdmin="<your-database-admin-user-name>" \
  --set database.databasePassword="<your-database-password>" \
  --set database.hiveDatabaseName="<your-hive-database-name>" \
  --set database.hiveDatabaseUser="<your-hive-database-user-name>" \
  --set database.hiveDatabasePassword="<your-hive-database-password>" \
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
