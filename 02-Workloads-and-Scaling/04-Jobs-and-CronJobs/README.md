# 04. Jobs and CronJobs Practice
**কেন ব্যবহার করছি?** 
- **Job:** একবার কাজ শেষ করে বন্ধ হয়ে যাবে এমন টাস্কের জন্য।
- **CronJob:** নির্দিষ্ট সময় পরপর (শিডিউল অনুযায়ী) কাজ করার জন্য (যেমন- ব্যাকআপ)।

**প্রয়োজনীয় কম্যান্ড:**
* **Apply:** `kubectl apply -f hello-cronjob.yaml`
* **Check Job:** `kubectl get jobs`
* **Check CronJob:** `kubectl get cj`
* **View Logs:** `kubectl logs <completed-pod-name>`
