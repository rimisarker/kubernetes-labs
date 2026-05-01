# 05-02: NodePort Service

NodePort is used to expose a service onto each Node's IP at a static port. This makes the service accessible from outside the cluster.

### YAML Breakdown:
- **type: NodePort**: Tells Kubernetes to open a port on all nodes.
- **nodePort (30005)**: The specific port exposed on the node. Range must be between 30000-32767.
- **port**: Internal service port.
- **targetPort**: The port on the container.

### How to Run:
1. **Apply Service:** `kubectl apply -f nodeport.yaml`
2. **Create Pod:** `kubectl run frontend-pod --image=nginx --labels="app=frontend-app"`
3. **Access App:**
   - On a cloud provider: `http://Node-IP:30005`
   - On Local/Kind: Use Port-forwarding
     ```bash
     kubectl port-forward svc/frontend-service 8080:80
     ```

### 🛠 Troubleshooting & Debugging:
1. **`nodePort: 30005: Provided port is not in the valid range`**: 
   - *Reason:* NodePort must be between 30000 and 32767.
2. **Cannot access via Node-IP**: 
   - *Reason:* If using Docker Desktop/Kind on Windows/Mac, the Nodes are inside a VM. Direct IP access might be blocked by a firewall.
   - *Fix:* Use `kubectl port-forward`.
3. **Endpoints are `<none>`**:
   - *Reason:* Service selector `app: frontend-app` doesn't match Pod labels.
