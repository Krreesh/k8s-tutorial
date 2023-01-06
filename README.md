# k8s-tutorial
<h1> Set alias k to kubectl </h1>
alias k=kubectl
<h1> Create nginx pod </h1>
kubectl run mynginx --image=nginx
kubectl run nginx-pod --image=nginx:alpine
kubectl get pods
<h1> Displays node on which pod is running </h1>
k get po -o wide 
