# Concepts
## Pod
![pod diagram](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/98b54b6b8427fae556be0cdd516b9e36.svg)
<center>Pods are the smallest deployable unit of computing you can create and manage in Kubernetes.</center> 

You can think of a pod as a **group of one or more containers**. These containers share storage and network resources. Because of this, containers on the same pod can communicate easily as if they were on the same machine whilst maintaining a degree of isolation.

## Nodes

- **Node:** A worker machine in the cluster.
	- The **control plane** is also know as the "master node"
- **kubelet:** Runs on each node and manages pod lifecycle, container runtime, and node-level resource management.
- **kube-proxy:** Network proxy that implements service abstraction and load balancing.
- **Container runtime:** Executes container images (e.g., Docker, containerd, CRI-O).

![The control plane can communicate with nodes using two paths](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/1bf22d1f65ab408e71d15d5049d11129.svg)

## Cluster
A set of nodes
# How it all works together

**Imagine Kubernetes as a smart apartment building manager.**

- **The Manager's Office (Control Plane):** This is where all the decisions are made.
    - **The Boss (kube-apiserver):** Takes requests from tenants (you) about what they need (like more space, or fixing a broken light).
    - **The Planner (kube-scheduler):** Figures out which apartment (node) is best for a new tenant (pod).
    - **The Fixer (kube-controller-manager):** Makes sure everything is running smoothly, like fixing broken appliances or renewing leases.
    - **The Memory (etcd):** Keeps track of who lives where and what their needs are.
- **The Apartments (Nodes):** These are where the tenants (pods) actually live.
    
    - **The Apartment Manager (kubelet):** Makes sure the apartment is clean, the lights work, and the tenant has everything they need.
    - **The Delivery Guy (kube-proxy):** Helps packages (network traffic) get to the right tenant.

**So, when you want to move in (deploy a pod):**

1. You tell the Boss (kube-apiserver) what kind of apartment you need.
2. The Planner (kube-scheduler) finds a suitable apartment.
3. The Apartment Manager (kubelet) gets your stuff ready and lets you move in.

**The Manager's Office and the Apartments work together to make sure everyone is happy and has what they need.**

![Cluster diagram](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/1eba5a686238be009bc802dd419a09c8.svg)

# Understanding the Kubernetes Landscape

Kubernetes is a powerful platform for managing containerized applications. To effectively navigate this landscape, it's essential to grasp key concepts and their roles.

## Core Kubernetes Components

- **Namespaces:** Virtual divisions within a cluster, isolating resources for different projects or teams.
- **ReplicaSets:** Ensure a specific number of identical pods are running at all times.
- **Deployments:** Manage the desired state of a pod group, automatically scaling and updating.
- **StatefulSets:** Handle applications that require persistent storage and stable network identities (e.g., databases, stateful services).
- **Services:** Provide a stable network endpoint for accessing pods, enabling load balancing and service discovery.
- **Ingress:** Acts as a single entry point for external traffic, routing requests to different services.

## Stateful vs. Stateless Applications

A crucial distinction lies between stateful and stateless applications.

- **Stateless applications:** Treat each request independently, without relying on previous interactions. Deployments are typically used to manage these applications. Examples include web servers, load balancers, and API gateways.
- **Stateful applications:** Maintain data and state across multiple requests, requiring persistent storage. StatefulSets are designed for these applications. Examples include databases, message queues, and stateful microservices.

## DevOps and DevSecOps Roles

- **DevOps:** Focuses on building, deploying, and managing Kubernetes clusters, including creating and configuring resources.
- **DevSecOps:** Incorporates security practices into the DevOps lifecycle, protecting the cluster and applications.

**In summary**, understanding these core components and the distinction between stateful and stateless applications is crucial for both DevOps and DevSecOps engineers. While DevOps is primarily concerned with infrastructure and application deployment, DevSecOps extends these responsibilities to include security considerations.

# In practice
We can interact with the cluster, nodes and pods using the [dashboard](https://github.com/kubernetes/dashboard) or the API using the kubectl command (See [[kubectl Cheat Sheet]]).