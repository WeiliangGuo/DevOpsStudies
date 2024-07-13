# Layers of Abstraction of a K8S Cluster on Azure
```
Azure Infrastructure
|
+-- Hardware Resources
|   |
|   +-- CPUs
|   |
|   +-- GPUs
|   |
|   +-- Memory
|   |
|   +-- Storage
|
+-- Virtual Networks
|   |
|   +-- Subnets
|
+-- Virtual Machines
|   |
|   +-- Network Interfaces
|   |   |
|   |   +-- Public IPs
|   |   |
|   |   +-- Network Security Groups
|   |
|   +-- Disks
|
Azure Kubernetes Service (AKS) (Built on Azure Infrastructure)
|
+-- AKS Cluster (Managed Kubernetes cluster)
|   |
|   +-- Kubernetes Components (Core components to manage and run the cluster)
|   |   |
|   |   +-- Control Plane (Manages the cluster)
|   |   |   |
|   |   |   +-- API Server (Handles API requests)
|   |   |   |
|   |   |   +-- etcd (Key-value store)
|   |   |   |
|   |   |   +-- Scheduler (Assigns pods to nodes)
|   |   |   |
|   |   |   +-- Controller Manager (Manages controllers)
|   |   |
|   |   +-- Node Components (Run on each node)
|   |       |
|   |       +-- Kubelet (Manages containers)
|   |       |
|   |       +-- Kube Proxy (Networking for services)
|   |       |
|   |       +-- Container Runtime (Runs containers)
|   |
|   +-- Node Pools (Groups of VMs)
|       |
|       +-- Virtual Machines (Nodes in the cluster)
|           |
|           +-- node1
|           |   |
|           |   +-- Kubernetes Resources (Objects to manage applications)
|           |       |
|           |       +-- Namespaces (Virtual clusters)
|           |       |
|           |       +-- Deployments (Manage replica sets)
|           |       |   |
|           |       |   +-- ReplicaSets (Maintain a stable set of pods)
|           |       |       |
|           |       |       +-- Pods (Smallest deployable units)
|           |       |           |
|           |       |           +-- Containers (Run applications)
|           |       |
|           |       +-- Services (Expose applications)
|           |       |
|           |       +-- ConfigMaps (Configuration data)
|           |       |
|           |       +-- Secrets (Sensitive data)
|           |
|           +-- node2
|           |
|           +-- node3
|           |
|           +-- ...
|           |
|           +-- nodeN
|
Monitoring and Logging (Tools for monitoring and logging)
|
+-- Azure Monitor (Monitor resources)
|
+-- Log Analytics (Analyze logs)
|
+-- Application Insights (Application performance)
```
