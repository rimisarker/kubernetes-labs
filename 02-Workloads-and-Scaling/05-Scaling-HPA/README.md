# 05. Scaling (HPA) Practice
**কেন ব্যবহার করছি?** সিপিইউ (CPU) লোড বাড়লে অটোমেটিক পড সংখ্যা বাড়ানোর জন্য এটি ব্যবহৃত হয়।

**প্রয়োজনীয় কম্যান্ড:**
* **Apply:** `kubectl apply -f hpa-demo.yaml`
* **Check HPA:** `kubectl get hpa`
* **Note:** এটি কাজ করার জন্য ক্লাস্টারে 'Metrics Server' ইনস্টল থাকা প্রয়োজন।
