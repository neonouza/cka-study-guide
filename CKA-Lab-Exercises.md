# CKA Lab Exercises

## Cluster Setup
1. Install Kubernetes using your preferred method (e.g., kubeadm, minikube).
2. Verify the installation:
   ```bash
   kubectl get nodes
   ```

## RBAC Configuration
1. Create a new namespace for testing RBAC:
   ```bash
   kubectl create namespace rbac-test
   ```
2. Create a role that allows access to pod resources:
   ```yaml
   apiVersion: rbac.authorization.k8s.io/v1
   kind: Role
   metadata:
     namespace: rbac-test
     name: pod-access
   rules:
   - apiGroups: ["*"]
     resources: ["pods"]
     verbs: ["get", "list"]
   ```
3. Bind the role to a user:
   ```yaml
   apiVersion: rbac.authorization.k8s.io/v1
   kind: RoleBinding
   metadata:
     name: pod-access-binding
     namespace: rbac-test
   subjects:
   - kind: User
     name: myuser
     apiGroup: rbac.authorization.k8s.io
   roleRef:
     kind: Role
     name: pod-access
     apiGroup: rbac.authorization.k8s.io
   ```

## Networking Setup
1. Install a CNI plugin (e.g., Calico, Flannel).
2. Verify network connectivity between pods:
   ```bash
   kubectl exec -it <pod-name> -- ping <another-pod-ip>
   ```

## Storage Configuration
1. Set up a persistent volume (PV) and a persistent volume claim (PVC):
   ```yaml
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: my-pv
   spec:
     capacity:
       storage: 5Gi
     accessModes:
       - ReadWriteOnce
     hostPath:
       path: /mnt/data
   ```
2. Create a PVC:
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
         storage: 5Gi
   ```

## Troubleshooting Labs
1. Use `kubectl describe` to inspect a pod.
   ```bash
   kubectl describe pod <pod-name>
   ```
2. Check pod logs:
   ```bash
   kubectl logs <pod-name>
   ```

## Security Labs
1. Implement network policies to restrict traffic.
2. Use Pod Security Policies (PSP) to enforce security standards.