## Node Affinity: বিস্তারিত বিশ্লেষণ (Line-by-Line)

Node Affinity ব্যবহার করে আমরা পডকে বলি যে তার কোন নোডে যাওয়া উচিত।

### গুরুত্বপূর্ণ কীওয়ার্ডসমূহ:
1. **requiredDuringSchedulingIgnoredDuringExecution:** 
   - এটি একটি **Hard Rule**। অর্থাৎ, পডটি যদি তার শর্ত পূরণ করে এমন নোড না পায়, তবে সে কোনোভাবেই অন্য নোডে বসবে না। পডটি **Pending** হয়ে থাকবে।
   
2. **nodeSelectorTerms & matchExpressions:**
   - এটি ফিল্টার করার প্রক্রিয়া। আমরা এখানে `key: disktype` এবং `operator: In` ব্যবহার করেছি। এর মানে হলো, নোডের লেবেলের সাথে এই ভ্যালুগুলো মিলতে হবে।

### ল্যাব রেজাল্ট বিশ্লেষণ:
- **ssd-app:** এটি `kind-worker2` নোডে গিয়েছে কারণ আমরা নোডটিকে `disktype=ssd` লেবেল দিয়েছিলাম।
- **hdd-app:** এটি `kind-worker` নোডে গিয়েছে কারণ তার রুল ছিল `disktype=hdd` খোঁজা।
- **pending-app:** এটি **Pending** হয়ে আছে। কেন?
  - কারণ পডটি খুঁজছে `disktype=gpu` লেবেলওয়ালা নোড।
  - আমাদের ক্লাস্টারে এমন কোনো নোড নেই।
  - যেহেতু এটি `requiredDuringScheduling` (Hard Rule), তাই সে ভুল নোডে না গিয়ে শিডিউলারের জন্য অপেক্ষা করছে।

### ডিবাগিং কমান্ড:
পেন্ডিং পডটি কেন আটকে আছে দেখতে নিচের কমান্ডটি দিন:
\\\bash
kubectl describe pod pending-app
\\\
আপনার আউটপুটের নিচের দিকে 'Events' সেকশনে দেখবেন লেখা আছে: 
`0/3 nodes are available: 3 node(s) didn't match Pod's node affinity/selector.`

### Soft Affinity (Preferred Rule) বিশ্লেষণ:

**Keyword:** `preferredDuringSchedulingIgnoredDuringExecution`

- **লজিক:** এটি একটি "অনুরোধ" (Best effort), কোনো "হুকুম" নয়।
- **Weight:** এটি ০-১০০ এর মধ্যে একটি স্কোর। একাধিক প্রেফারেন্স থাকলে এটি সিদ্ধান্ত নিতে সাহায্য করে।
- **রিয়েল লাইফ উদাহরণ:** 
  - আমি চাই আমার ডাটাবেস পডটি SSD নোডে চলুক (পছন্দ)। 
  - কিন্তু যদি কোনো SSD নোড খালি না থাকে, তবে সার্ভিস বন্ধ না রেখে সাধারণ HDD নোডেই চালু হয়ে যাও (বাস্তবতা)।
সারাংশ:
Hard Rule (required): Strict. শর্ত না মিললে কাজ হবে না।

Soft Rule (preferred): Flexible. শর্ত না মিললে "Backup Plan" হিসেবে অন্য নোড ব্যবহার করবে।
