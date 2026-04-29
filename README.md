# Kubernetes Learning Journey
## Troubleshooting: ImagePullBackOff Error

প্রজেক্ট করার সময় আমি `frontend-rs` এ `ImagePullBackOff` error পেয়েছিলাম।

### error dekhar commad:
`kubectl describe pod <pod-name>`

### কেন error হয়েছিলো?
ইমেজ ট্যাগ `v3` খুঁজে পাওয়া যাচ্ছিলো না। ইভেন্টে নিচের মেসেজটি ছিল:
> Failed to pull image "gcr.io/google_samples/gb-frontend:v3": rpc error: code = NotFound

### solution:
আমি YAML ফাইলে ইমেজ পরিবর্তন করে `nginx:latest` দিয়েছি এবং পডগুলো রিস্টার্ট করেছি।

### ekhn status:
এখন সব pod `Running` অবস্থায় আছে।
```bash
kubectl get pods
NAME                READY   STATUS    RESTARTS   AGE
annotation-pod      1/1     Running   0          46m
frontend-rs-8chfh   1/1     Running   0          10m
frontend-rs-8gskg   1/1     Running   0          10m
frontend-rs-rmj26   1/1     Running   0          10m
label-demo-pod      1/1     Running   0          48m
nginx-pod           1/1     Running   0          54m
