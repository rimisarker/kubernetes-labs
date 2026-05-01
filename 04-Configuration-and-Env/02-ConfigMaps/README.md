### **২. ০৪-Configuration-and-Env/02-ConfigMaps/README.md**

```markdown
# ConfigMaps

ConfigMap হলো একটি সেন্ট্রাল স্টোরেজ যেখানে নন-সেনসিটিভ ডাটা রাখা হয়।



### কেন ব্যবহার করবেন?
- যখন একই কনফিগারেশন অনেকগুলো পড ব্যবহার করে।
- ডাটাবেস হোস্টনেম বা অ্যাপ সেটিংস আলাদা রাখার জন্য।

### ব্যবহারের উপায়:
১. **Env Variable হিসেবে:** পডের ভেতরে ভেরিয়েবল হিসেবে ডাটা ঢোকানো যায়।
২. **Volume হিসেবে:** পডের ভেতরে একটি ফাইল (যেমন `config.json`) হিসেবে মাউন্ট করা যায়।

### প্র্যাকটিক্যাল কমান্ড:
```bash
# ConfigMap এবং পড তৈরি করুন
kubectl apply -f configmap.yaml
kubectl apply -f pod-configmap.yaml

# যাচাই করুন
kubectl exec config-pod -- printenv | grep DB_HOST
