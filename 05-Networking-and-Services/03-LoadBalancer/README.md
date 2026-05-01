# 05-03: LoadBalancer Service

The LoadBalancer service is the standard way to expose a service to the internet in a production environment (AWS, Azure, GCP).

### How it works:
1. It creates a `NodePort` and a `ClusterIP` internally.
2. It requests the Cloud Provider to provision a External Load Balancer.
3. Traffic flows: **User -> External IP -> Service -> Pods**.

### Deployment & Execution:
1. **Create App:** 
   `kubectl create deployment frontend-app --image=nginx --replicas=2`
2. **Apply Service:** 
   `kubectl apply -f loadbalancer.yaml`
3. **Verify:** 
   `kubectl get svc cloud-service`

### 🛠 Debugging:
- **Status `<pending>`**: On local clusters (Kind/Minikube), this is normal. Use `kubectl port-forward` to test.
- **Wrong Endpoints**: Ensure the deployment has the label `app: frontend-app`.
- **Port Mismatch**: `port` is what the service uses, `targetPort` is what the container uses.

### 🧹 Clean up:
```bash
kubectl delete svc cloud-service
kubectl delete deployment frontend-app

### বোনাস টিপস (Troubleshooting):
যদি কখনো দেখেন পড চলছে কিন্তু লোড ব্যালেন্সার দিয়ে ঢুকতে পারছেন না, তখন এই কমান্ডটি দিন:
`kubectl get endpoints cloud-service`
যদি এন্ডপয়েন্ট লিস্ট খালি থাকে, তার মানে আপনার সার্ভিসের **Selector** এবং পডের **Label** এর বানানে ভুল আছে।
