# StorageClass (Dynamic Provisioning)

ম্যানুয়ালি PV বানানোর ঝামেলা দূর করার জন্য StorageClass ব্যবহার করা হয়।

### কাজ করার প্রক্রিয়া:
1. **StorageClass:** এটি ডিফাইন করে স্টোরেজ কোথা থেকে আসবে (AWS, Azure, Local)।
2. **PVC:** এই ফাইলে শুধু `storageClassName` বলে দিতে হয়।
3. **Automatic PV:** পড তৈরি হওয়ার সাথে সাথে StorageClass নিজে থেকেই একটি PV বানিয়ে ফেলে।

### ইন্টারভিউ প্রশ্ন:
**Q: Static vs Dynamic Provisioning কি?**
**Ans:** Static মানে অ্যাডমিন আগে থেকে PV বানিয়ে রাখে। Dynamic মানে StorageClass ব্যবহার করে পডের দরকার অনুযায়ী অটোমেটিক PV তৈরি হয়।

**Q: volumeBindingMode: WaitForFirstConsumer কেন ব্যবহার করা হয়?**
**Ans:** যাতে স্টোরেজটি সেই নোডেই তৈরি হয় যেখানে পডটি শিডিউল হয়েছে।


ক্লিনআপ (Cleanup):
সব চেক করা হয়ে গেলে ডিলিট করতে পারেন:

Bash
kubectl delete -f 06-Storage-Management/02-StorageClass/

