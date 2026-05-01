# 05-01: ClusterIP Service

ClusterIP is the default Kubernetes service type. It provides a stable internal IP address that other pods within the cluster can use to communicate.

### Why use ClusterIP?
- For internal microservices (e.g., Database, Internal API).
- To provide a single point of entry for a set of pods.
- It is not accessible from outside the cluster.

### YAML Breakdown:
- **Selector (`app: backend-app`)**: This connects the service to any Pod labeled with `app: backend-app`.
- **Port**: The port the service listens on inside the cluster.
- **TargetPort**: The port the container is actually running on.

### Commands:
```bash
# Apply the service
kubectl apply -f clusterip.yaml

# Check service status
kubectl get svc backend-service

# Check endpoints (to see if pods are connected)
kubectl describe svc backend-service

### 🛠 Critical Debugging: "Failed to connect (exit code 7)"
If you get a connection failure, follow these steps:
1. **Check Endpoints**: Run `kubectl get endpoints backend-service`. 
   - If it says `<none>`, your service cannot find any pods with the label `app: backend-app`.
2. **Check Labels**: Run `kubectl get pods --show-labels`. Ensure your target pod has the exact label.
3. **Check TargetPort**: Ensure the `targetPort` in `clusterip.yaml` matches the actual port your application is listening on inside the pod.
