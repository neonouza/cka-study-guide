# CKA Lab Exercises

This document contains hands-on lab exercises for practicing Kubernetes skills. Each exercise includes step-by-step instructions for deploying applications, configuring RBAC, setting up networking, storage management, and troubleshooting.

## 1. Deploying Applications
### Exercise 1.1: Deploy a NGINX Application
1. Create a deployment:
   ```bash
   kubectl create deployment nginx --image=nginx
   ```
2. Expose the deployment:
   ```bash
   kubectl expose deployment nginx --port=80 --type=LoadBalancer
   ```
3. Verify the deployment:
   ```bash
   kubectl get deployments
   ```

## 2. Configuring RBAC
### Exercise 2.1: Create a Role and RoleBinding
1. Create a role:
   ```yaml
   apiVersion: rbac.authorization.k8s.io/v1
   kind: Role
   metadata:
     namespace: default
     name: pod-reader
   rules:
   - apiGroups: [""]  # core API group
     resources: ["pods"]
     verbs: ["get", "list"]
   ```
2. Apply the role:
   ```bash
   kubectl apply -f role.yaml
   ```
3. Create a RoleBinding:
   ```yaml
   apiVersion: rbac.authorization.k8s.io/v1
   kind: RoleBinding
   metadata:
     name: read-pods-binding
     namespace: default
   subjects:
   - kind: User
     name: example-user # Replace with actual user
     apiGroup: rbac.authorization.k8s.io
   roleRef:
     kind: Role
     name: pod-reader
     apiGroup: rbac.authorization.k8s.io
   ```
4. Apply the RoleBinding:
   ```bash
   kubectl apply -f rolebinding.yaml
   ```

## 3. Setting Up Networking
### Exercise 3.1: Configure a NetworkPolicy
1. Create a NetworkPolicy:
   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: NetworkPolicy
   metadata:
     name: deny-all
     namespace: default
   spec:
     podSelector: {}
     policyTypes:
     - Ingress
   ```
2. Apply the NetworkPolicy:
   ```bash
   kubectl apply -f networkpolicy.yaml
   ```

## 4. Storage Management
### Exercise 4.1: Create a Persistent Volume
1. Create a Persistent Volume (PV):
   ```yaml
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: my-pv
   spec:
     capacity:
       storage: 10Gi
     accessModes:
       - ReadWriteOnce
     hostPath:
       path: /mnt/data
   ```
2. Apply the PV:
   ```bash
   kubectl apply -f pv.yaml
   ```

## 5. Troubleshooting
### Exercise 5.1: Troubleshoot a Pod
1. Describe the pod:
   ```bash
   kubectl describe pod <pod-name>
   ```
2. Check the logs:
   ```bash
   kubectl logs <pod-name>
   ```
3. Check the events:
   ```bash
   kubectl get events
   ```

---

This document is intended to be a comprehensive guide for CKA exam preparation. Feel free to add more exercises and expand on these topics.  
