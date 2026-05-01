🌐 Ingress: A to Z Mastery Guide
১. ইনগ্রেস কী এবং কেন লাগবে? (The Logic)সাধারণ NodePort এ আমাদের আইপির পর পোর্ট (যেমন: :30005) দিতে হয়। কিন্তু প্রফেশনাল কাজে আমরা ডোমেইন (যেমন: myapp.local) ব্যবহার করতে চাই। ইনগ্রেস এই ডোমেইন নেমকে আপনার সার্ভিসের সাথে কানেক্ট করে।২. কী কী লাগবে? (Prerequisites)১. একটি রানিং কুবারনেটিস ক্লাস্টার (যেমন: Kind)।২. ইনগ্রেস কন্ট্রোলার (Ingress Controller)।৩. হোস্ট ফাইল এডিট করার পারমিশন।৩. সেটআপ গাইড (Step-by-Step)Step A: ইনগ্রেস কন্ট্রোলার ইনস্টল করাকুবারনেটিসে ইনগ্রেস রুল নিজে নিজে কাজ করতে পারে না। তার জন্য একটি "ইঞ্জিন" বা কন্ট্রোলার লাগে। আমরা NGINX ব্যবহার করবো:Bashkubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
যাচাই: কন্ট্রোলার পডটি রানিং কি না দেখুন:Bashkubectl get pods -n ingress-nginx
Step B: অ্যাপ এবং সার্ভিস তৈরি করাইনগ্রেস যাকে ট্রাফিক পাঠাবে, সেই সার্ভিসটি আগে তৈরি থাকতে হবে।Bashkubectl apply -f app-service.yaml
Step C: ইনগ্রেস রুল অ্যাপ্লাই করাএবার ডোমেইন ম্যাপিং রুলটি অ্যাপ্লাই করুন:Bashkubectl apply -f ingress-rule.yaml
Step D: হোস্ট ফাইল এডিট (Local DNS)আপনার পিসিকে myapp.local চিনিয়ে দিন।Windows: C:\Windows\System32\drivers\etc\hosts (Run as Admin)Linux/Mac: sudo nano /etc/hostsলাইন যোগ করুন: 127.0.0.1 myapp.local৪. প্রয়োজনীয় কমান্ডস (Cheat Sheet)কাজকমান্ডApplykubectl apply -f <filename>List Ingresskubectl get ingressDescribekubectl describe ingress main-ingressDelete Rulekubectl delete ingress main-ingressCheck Controllerkubectl get pods -n ingress-nginxDelete Controllerkubectl delete -f <controller-url-or-file>৫. ডেব্যাগিং এবং ট্রাবলশুটিং (Debug Like a Pro)যদি ব্রাউজারে myapp.local কাজ না করে, তবে নিচের স্টেপগুলো চেক করুন:Address Check: kubectl get ingress দিন। যদি ADDRESS কলামে কোনো আইপি বা localhost না থাকে, তবে বুঝবেন কন্ট্রোলার এখনো রেডি হয়নি।Ping Test: টার্মিনালে ping myapp.local দিন। যদি রিপ্লাই না আসে, তবে আপনার হোস্ট ফাইল এডিট করা ভুল হয়েছে।Controller Logs: কন্ট্রোলারে কোনো ভুল হচ্ছে কি না দেখতে:Bashkubectl logs -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx
Service Check: ইনগ্রেস রুলে দেওয়া service name আর আপনার আসল সার্ভিসের নাম মিল আছে কি না নিশ্চিত করুন।৬. ডিলিট বা ক্লিনআপ (Reset Everything)সবকিছু মুছে ফেলতে চাইলে:Bash# ইনগ্রেস রুল মুছতে
kubectl delete ingress main-ingress

# সার্ভিস এবং ডিপ্লয়মেন্ট মুছতে
kubectl delete -f app-service.yaml

# ইনগ্রেস কন্ট্রোলার পুরোপুরি সরাতে
kubectl delete ns ingress-nginx
ইন্টারভিউ ভাইভা ফোকাস:প্রশ্ন: ইনগ্রেস রুলে pathType: Prefix এর মানে কী?উত্তর: এর মানে হলো ওই পাথের পরে যা-ই আসুক (যেমন: /shop/item1), সব ওই সার্ভিসে যাবে।প্রশ্ন: ইনগ্রেস কি ক্লাস্টারের বাইরে থেকে এক্সেস করা যায়?উত্তর: হ্যাঁ, তবে তার জন্য একটি পাবলিক আইপি (LoadBalancer) বা লোকাল মেশিনে হোস্ট ফাইল ম্যাপিং প্রয়োজন।
