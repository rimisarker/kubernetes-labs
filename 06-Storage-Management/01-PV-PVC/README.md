# Part 06: Storage Management (PV & PVC) 💾

কুবারনেটিসে ডাটা পারসিস্টেন্সি (Data Persistency) নিশ্চিত করার জন্য PV এবং PVC ব্যবহার করা হয়।

## 🔑 মূল কনসেপ্ট
- **PV (Persistent Volume):** ফিজিক্যাল স্টোরেজ (অ্যাডমিন তৈরি করে)।
- **PVC (Persistent Volume Claim):** স্টোরেজের জন্য পডের করা রিকোয়েস্ট।
- **Volume Mount:** পডের ভেতরের কোনো ফোল্ডারকে PV-এর সাথে জোড়া লাগানো।

---

## 🛠️ প্র্যাকটিক্যাল কমান্ডস

১. **PV এবং PVC তৈরি করুন:**
```bash
kubectl apply -f 01-PV-PVC/pv.yaml
kubectl apply -f 01-PV-PVC/pvc.yaml


২. স্ট্যাটাস চেক করুন:

Bash
kubectl get pv
kubectl get pvc

৩. পড রান করুন:

Bash
kubectl apply -f 01-PV-PVC/pod-with-storage.yaml
🔍 ডেব্যাগিং গাইড (Debug)
যদি PVC 'Pending' থাকে, তবে চেক করুন PV-এর সাইজ PVC-এর চেয়ে কম কি না। (PV অবশ্যই সমান বা বড় হতে হবে)।

kubectl describe pvc my-pvc দিয়ে ইরর মেসেজ দেখুন।
