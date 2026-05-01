### **৩. ০৪-Configuration-and-Env/03-Secrets/README.md**

```markdown
# Kubernetes Secrets

পাসওয়ার্ড, এপিআই কি এবং সার্টিফিকেটের মতো গোপন তথ্য রাখার জন্য Secret ব্যবহার করা হয়।



### গুরুত্বপূর্ণ তথ্য:
- সিক্রেট ডাটা অবশ্যই **Base64** এনকোড করা হতে হবে।
- এটি পডের মেমোরিতে (RAM) থাকে, ডিস্কে নয়।

### কিভাবে Base64 এনকোড করবেন?
```bash
echo -n 'my-password' | base64


# Secret এবং পড তৈরি করুন
kubectl apply -f secret.yaml
kubectl apply -f pod-secret.yaml

# যাচাই করুন
kubectl exec secret-pod -- printenv | grep DATABASE_PASSWORD
প্রশ্ন: Base64 কি সিকিউর?
উত্তর: না, এটি শুধু এনকোডিং। প্রোডাকশনে আমরা এর সাথে Encryption at Rest বা HashiCorp Vault ব্যবহার করি।
