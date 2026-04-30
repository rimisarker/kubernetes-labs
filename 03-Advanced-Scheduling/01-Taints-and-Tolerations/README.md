# Kubernetes Taints and Tolerations Lab

Ei lab-e amra shikhechi kivabe Node-er upore control rakha jay jate nirdishto Pod chara onno keu shekhane schedule na hote pare.

## Step 1: Cluster Setup (Kind)
Prothome amra multi-node cluster use korechi:
```bash
kind create cluster --name k8s-learning --config kind-config.yaml


Step 2: Tainting the Nodes
Amra worker node-ke taint korechi jate normal Pod shekhane na jete pare:

kubectl taint nodes kind-worker color=blue:NoSchedule
kubectl taint nodes kind-worker2 color=blue:NoSchedule

Step 3: Deployment & Testing
1.Normal Pod: Eti Pending obosthay thakbe karon er kono toleration nei.

kubectl run normal-pod --image=nginx
2.Toleration Pod: Eti Running hobe karon er YAML-e color=blue toleration dewa ache.

Step 4: Debugging
Pod keno Pending seta check korar command:

kubectl describe pod normal-pod

Step 5: Cleanup
Taint muche fela:
kubectl taint nodes --all color:NoSchedule-
