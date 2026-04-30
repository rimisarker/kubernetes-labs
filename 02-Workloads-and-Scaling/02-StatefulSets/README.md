# 02. StatefulSets Practice
**কেন use করছি?** databese or statefulset অ্app ar জন্য use হয়। এর প্রতিটি pod er একটি নির্দিষ্ট নাম (যেমন: web-sts-0) থাকে যা রিস্টার্ট দিলেও পরিবর্তন হয় না।

**প্রয়োজনীয় কম্যান্ড:**
* **Apply:** `kubectl apply -f web-sts.yaml`
* **Check:** `kubectl get sts`
* **Watch Naming:** `kubectl get pods -w` (দেখুন কীভাবে একটির পর একটি পড তৈরি হয়)
