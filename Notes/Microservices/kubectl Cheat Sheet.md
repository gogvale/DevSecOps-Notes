# apply

We can define deployment and services YAML configuration files and load them into processes by running

```shell
kubectl apply -f example-deployment.yaml
```

# get

We can check the status of the running instances like **deployments, services, pods, and ReplicaSets** by calling the get command followed by the namespace argument:

```shell
kubectl get pods -n example-namespace
```

# describe

This command can be used to show the details of a resource (or a group of resources) for troubleshooting or analysis situations.

```shell
kubectl describe pod example-pod -n example-namespace
```

# logs

This command is used to check a pod logs.

```shell
kubectl logs example-pod -n example-namespace
```

# exec

Executes commands on a pod (like an interactive shell). Everything after the `--` will be executed:

```shell
kubectl exec -it example-pod -n example-namespace -- sh
```

# port-forward

This command allows you to create a secure tunnel between your local machine and a running pod in your cluster.

```shell
kubectl port-forward service/example-service 8090:8080
```

This command establishes a local port (8090) and forwards traffic to a specified service (example-service) within the Kubernetes cluster, mapping it to port 8080 within the service's pods, enabling local access and interaction with the service.

