# CKA Complete Study Guide

## Introduction
This study guide is designed to provide comprehensive coverage of all exam domains for the Certified Kubernetes Administrator (CKA) certification. It includes essential information, kubectl commands, and YAML examples.

## 1. Cluster Architecture
### Understanding Cluster Components
- **Kubernetes Master**: Controls the cluster. Components include API Server, Scheduler, Controller Manager, etc.
- **Worker Nodes**: Run the application workloads (Pods).

### Key Components of a Kubernetes Cluster:
- **etcd**: Consistent and highly available key-value store.
- **Kubelet**: An agent that runs on each node in the cluster.
- **Kube-proxy**: Manages network proxying and load balancing.

### Essential Commands:
```bash
# View cluster info
kubectl cluster-info

# Get nodes status
kubectl get nodes
```

## 2. Services & Networking
### Understanding Services
- **ClusterIP**: Exposes the service on an internal IP in the cluster.
- **NodePort**: Exposes the service on each Node's IP at a static port.
- **LoadBalancer**: Exposes the service externally using a cloud provider’s load balancer.

### Essential Commands:
```bash
# Get services
kubectl get services

# Describe a service
kubectl describe service [service-name]
```

### YAML Example for a Service:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30000
  selector:
    app: MyApp
```

## 3. Troubleshooting
### Common Troubleshooting Commands:
```bash
# Get pod logs
kubectl logs [pod-name]

# Get events for a namespace
kubectl get events --namespace=[namespace]

# Describe pod to get detailed information
kubectl describe pod [pod-name]
```

## 4. Workloads & Scheduling
### Workload Types
- **Pods**: The smallest deployable units in Kubernetes.
- **Deployments**: Manage the deployment of ReplicaSets.
- **StatefulSets**: Manage stateful applications.

### Essential Commands:
```bash
# List deployments
kubectl get deployments

# Scale a deployment
kubectl scale deployment [deployment-name] --replicas=[number]
```

### YAML Example for a Deployment:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: MyApp
  template:
    metadata:
      labels:
        app: MyApp
    spec:
      containers:
        - name: my-container
          image: my-image:latest
```

## 5. Storage
### Understanding Persistent Storage
- **Persistent Volumes (PV)** and **Persistent Volume Claims (PVC)** are used to manage storage resources.

### Essential Commands:
```bash
# Get persistent volumes
kubectl get pv

# Get persistent volume claims
kubectl get pvc
```

### YAML Example for a PVC:
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

## Conclusion
This study guide provides a foundation for preparing for the CKA certification exam. Make sure to practice these commands and understand the underlying concepts thoroughly.