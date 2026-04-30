# 01. Deployments Practice
**কেন ব্use  করছি?**Production Application চালানোর সবচেয়ে জনপ্রিয় উপায়। এটি রোলিং আপডেট (Rolling Update) এবং রোলব্যাক সাপোর্ট করে।

**প্রয়োজনীয় Command:**
* **Apply:** `kubectl apply -f nginx-deployment.yaml`
* **Check Status:** `kubectl rollout status deployment/nginx-deployment`
* **Check Revision:** `kubectl rollout history deployment/nginx-deployment`
* **Scale Manually:** `kubectl scale deployment nginx-deployment --replicas=5`
