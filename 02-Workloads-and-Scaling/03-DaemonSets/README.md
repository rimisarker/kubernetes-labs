# 03. DaemonSets Practice
**কেন ব্যবহার করছি?** ক্লাস্টারের প্রতিটি নোড-এ একটি নির্দিষ্ট পড চালানোর জন্য (যেমন: Log collector বা Monitoring agent)।

**প্রয়োজনীয় কম্যান্ড:**
* **Apply:** `kubectl apply -f fluentd-ds.yaml`
* **Check:** `kubectl get ds`
* **Check Pods:** `kubectl get pods -o wide` (দেখবেন আপনার নোডের সংখ্যা অনুযায়ী পড তৈরি হয়েছে)
