# Commands
## apply

We can define deployment and services YAML configuration files and load them into processes by running

```shell
kubectl apply -f example-deployment.yaml
```

## get

We can check the status of the running instances like **deployments, services, pods, and ReplicaSets** by calling the get command followed by the namespace argument:

```shell
kubectl get pods -n example-namespace
```

In case we want to see all namespaces we use `-A`:

```shell
kubectl get pods -A
```
## describe

This command can be used to show the details of a resource (or a group of resources) for troubleshooting or analysis situations.

```shell
kubectl describe pod example-pod -n example-namespace
```

## logs

This command is used to check a pod logs.

```shell
kubectl logs example-pod -n example-namespace
```

## exec

Executes commands on a pod (like an interactive shell). Everything after the `--` will be executed:

```shell
kubectl exec -it example-pod -n example-namespace -- sh
```

## port-forward

This command allows you to create a secure tunnel between your local machine and a running pod in your cluster.

```shell
kubectl port-forward service/example-service 8090:8080
```

This command establishes a local port (8090) and forwards traffic to a specified service (example-service) within the Kubernetes cluster, mapping it to port 8080 within the service's pods, enabling local access and interaction with the service.

## serviceaccount
(TODO)

```shell
kubectl create sa terminal-user
```

# Recipes
## Getting credentials from secret

```shell
# Get available secrets
kubectl get secrets # finds terminal-creds

# Get variables stored (it saves as json base64 encripted by default)
kubectl describe secret terminal-creds # Finds username and password

# Decodes values
kubectl get secret terminal-creds -o jsonpath='{.data.username}'| base64 --decode
```

## Restricting access to a service account
1. Create a Role or ClusterRole:
	- Decide whether you want to create a Role (scoped to a namespace) or a ClusterRole (applies cluster-wide)
2. Create  a RoleBinding or ClusterRoleBinding:
	- Use the service account you want to restrict and bind it to the Role or ClusterRole
3. Apply the Role and RoleBinding:
	- Use `kubectl apply -f` to apply the role and RoleBinding


```yaml
# restrict-service-account-role-yaml
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  namespace: default
  name: secret-admin
rules:
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get"]
  resourceNames: ["terminal-creds]
```
- **Kind**: Specifies that this YAML defines a Role.
- **apiVersion**: Indicates the API version of the RBAC resource.
- **metadata**:
    - **namespace**: Specifies the namespace where this Role is created (`default` in this case).
    - **name**: Defines the name of the Role (`secret-admin` in this case).
- **rules**: Defines the permissions (rules) associated with this Role:
    - **apiGroups**: Specifies the API group (`""` indicates core Kubernetes API).
    - **resources**: Specifies the Kubernetes resource type (`secrets`).
    - **verbs**: Specifies the allowed actions (`get` allows reading secrets).
    - **resourceNames**: Optionally restricts the Role to specific resource instances (`terminal-creds`).

---

```yaml
# restrict-service-account-binding-yaml
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: secret-admin-binder
  namespace: default
subjects:
- kind: ServiceAccount
  name: terminal-admin
  namespace: default
roleRef:
  kind: Role  # or ClusterRole
  name: secret-admin
  apiGroup: rbac.authorization.k8s.io
```

- **Kind**: Specifies that this YAML defines a RoleBinding.
- **apiVersion**: Indicates the API version of the RBAC resource.
- **metadata**:
    - **name**: Defines the name of the RoleBinding (`secret-admin-binder`).
    - **namespace**: Specifies the namespace where this RoleBinding is created (`default` in this case).
- **subjects**: Specifies the subjects (entities) to which the Role is bound:
    - **kind**: Specifies the kind of subject (`ServiceAccount`).
    - **name**: Specifies the name of the ServiceAccount (`terminal-admin`).
    - **namespace**: Specifies the namespace of the ServiceAccount (`default` in this case).
- **roleRef**: Specifies the Role or ClusterRole to bind:
    - **kind**: Specifies the kind of the referenced role (`Role` in this case).
    - **name**: Specifies the name of the Role (`secret-admin`).
    - **apiGroup**: Specifies the API group of the role (`rbac.authorization.k8s.io`).

---

```bash
kubectl apply -f restrict-service-account-role.yaml
kubectl apply -f restrict-service-account-binding.yaml
```

- **kubectl apply -f restrict-service-account-role.yaml**: This command applies the Role configuration defined in `restrict-service-account-role.yaml` to the Kubernetes cluster. It creates or updates the Role `secret-admin` in the `default` namespace, allowing the `terminal-admin` ServiceAccount to get (read) the `terminal-creds` secret.
- **kubectl apply -f restrict-service-account-binding.yaml**: This command applies the RoleBinding configuration defined in `restrict-service-account-binding.yaml`. It binds the `secret-admin` Role to the `terminal-admin` ServiceAccount in the `default` namespace, effectively granting the permissions specified in `secret-admin` to the ServiceAccount `terminal-admin`.


### Explanation:

- **Role**: Defines a set of permissions (`get` on `secrets`) scoped to a specific namespace (`default`).
- **RoleBinding**: Binds the Role (`secret-admin`) to a specific ServiceAccount (`terminal-admin`) within the same namespace (`default`), allowing the ServiceAccount to perform the actions specified in the Role (`get` operation on `terminal-creds` secret).
- **kubectl apply**: Command used to apply the YAML configurations to the Kubernetes cluster, thereby configuring RBAC rules and bindings.
### Verification:

- To verify that the restrictions are applied correctly, you can:
    - Test accessing pods or other resources using `kubectl` with the restricted service account.
    - Ensure that attempts to perform actions not allowed by the Role result in permission denied errors.

```
kubectl auth can-i get \
secret/terminal-creds --as=system:serviceaccount:default:terminal-user
```
### Notes:

- **ClusterRole**: If you need to apply restrictions across namespaces or at the cluster level, use `ClusterRole` and `ClusterRoleBinding` instead of `Role` and `RoleBinding`.
- **Customization**: Adjust the `apiGroups`, `resources`, and `verbs` according to the specific permissions you want to grant or restrict for the service account.