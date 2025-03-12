```sh
helm repo add koku https://skyu-io.github.io/koku-helm-chart
```

```sh
helm repo update
```

```sh
helm install koku koku/koku \
  --set credentials.awsAccessKeyId="<your-aws-access-key-id>" \
  --set credentials.awsSecretAccessKey="<your-aws-secret-access-key>" \
  --namespace koku --create-namespace
```