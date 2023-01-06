# k8s-tutorial
<h1> Set alias k to kubectl </h1>
alias k=kubectl
<h1> Create nginx pod </h1>
kubectl run mynginx --image=nginx
kubectl run nginx-pod --image=nginx:alpine
kubectl get pods
<h1> Displays node on which pod is running </h1>
k get po -o wide 
<h1> Get pods from ALL NAMESPACES </h1>
k get pods -A 
kubectl describe pod newpods-77pqk
kubectl delete pod webapp
<h1> DELETE ALL PODS </h1>
k delete pod -l name=busybox-pod 
kubectl run redis --image=redis123 --dry-run=client -o yaml > redis.yaml
kubectl run nginx --image=nginx --dry-run=client -o yaml
kubectl run nginx --image=nginx --dry-run=client -o yaml > nginx-deployment.yaml
k run yellow --image=busybox --dry-run=client -o yaml
kubectl create -f redis.yaml
kubectl create -f replicaset-definition.yml
k run messaging --image=redis:alpine --labels="tier=msg"
kubectl get replicaset
kubectl delete replicaset myapp-replicaset
kubectl replace -f replicaset-definition.yml
kubectl scale -replicas=6 -f replicaset-definition.yml
kubectl describe replicaset new-replica-set
kubectl edit replicaset new-replica-set
kubectl delete replicaset replicaset-1 replicaset-2
kubectl delete --all pods --namespace=default
kubectl delete --all pods -n default
kubectl get namespaces
 or kubectl get ns
<h1> Create Namespace </h1>
kubectl create ns dev-ns
kubectl scale --replicas=2 rs/new-replica-set
kubectl get all
kubectl get pods --all-namespaces
kubectl get pods --namespace=research
kubectl get deployments
<h1> CREATE DEPLOYMENT </h1>
kubectl create deployment --image=nginx nginx
kubectl create deployment --image=nginx nginx --dry-run -o yaml
kubectl create deployment nginx --image=nginx --replicas=4
kubectl create deployment redis-deploy --image=redis --replicas=2 --namespace=dev-ns
k create deployment redis --iamge=redis:alpine --replica=1
k expose deployment redis --name=redis --port=6379 --target-port=6379
k expose deployment redis --port=6379 --type=ClusterIP --name=redis --target-port=6379
kubectl scale deployment nginx --replicas=4
kubectl create deployment nginx --image=nginx--dry-run=client -o yaml > nginx-deployment.yaml
kubectl describe deployment frontend-deployment
kubectl create -f deployment-definition-1.yaml
kubectl get pods --namespace=dev
k get pods -n elastic-stack
<h1> GET LOGS FROM POD </h1>
k logs app -n elastic-stack
k replace --force -f m.yaml
kubectl get pod webapp-color -o yaml > pod.yaml
kubectl create -f redis.yaml --namespace=finance
<h1> CHANGE NAMESPACE FOR CURRENT CONTEXT </h1>
kubectl config set $(kubectl config current-context) --namespace=dev 
<h1> Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379 </h1>
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml

<h1>CREATE POD & SERVICE AT ONCE</h1>
kubectl run httpd --image=httpd:alpine --port=80 --expose=true

kubectl get svc
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
k expose deploy/simple-webapp-deployment --port=8080 --target-port=8080 --type=NodePort --name=webapp-service --node-port=30080 --dry-run=client -o yaml
kubectl expose pod redis --port=6379 --name=redis-service
kubectl expose pod httpd --port=80 --name httpd
k expose deployment redis --port=6379 -n marketing --name=messaging-service
kubectl edit pod ubuntu-pod.yaml
kubectl replace --force -f /tmp/kubectl-edit-22343.yaml
kubectl get configmaps
kubectl describe configmap db-config
kubectl create configmap web-config --from-literal=APP_COLOR=blue
kubectl create configmap web-config --from-file=app_config.properties
kubectl create secret generic my-sec --from-literal=db_pass=superscret --from-literal=DB_HOST=mysql
kubectl create secret generic my-sec --from-file=app_secret.properties
echo -n 'superscretpassword' | base64
echo -n 'b-23=sher' | base64 --decode
kubectl get secrets 
kubectl get secret app-secret -o yaml
k create secret generic db-secret-xxdf --from-literal=DB_HOST=c3FsMDE= --from-literal=DB_User=cm9vdA== --from-literal=DB_Password=cGFzc3dvcmQxMjM=
kubectl create serviceaccount dashboard-sa
kubectl describe secret dashboard-sa-token-kdbm
curl https://192.618.56.72:6443/api -insecure --header "Authorization: Bearer eykskdfj34"
<h1> APPLY CHANGES </h1>
kubectl apply -f dash.yaml 
<h1> taint-effect NoSchedule|PreferNoSchedule|NoExecute </h1>
kubectl taint nodes node-name key=value:taint-effect 
kubectl taint node node01 "spray"="mortein":NoSchedule
<h1> REMOVE TAINT from Node (Add name of taint and '-') </h1>
kubectl taint node controlplane node-role.kubernetes.io/master:NoSchedule-
kubectl describe node kubemaster | grep Taint
kubectl get nodes
kubectl label nodes <node-name> <label-key>=<label-value>
kubectl create deployment blue --image=nginx --replicas=3
k logs kibana -n elastic-stack
k -n elastic-stack exec -it app -- cat /log/app.log
k logs -f event-simulator-pod event-simulator
k logs -f <pod-name> <container-name>
<h1> IDENTITY Node that consumes most memory </h1>
k top node
<h1> IDENTITY pod that consumes most memory </h1>
k top pod  
k get pods --selector app=App1
k get all --selector env=prod
k get pods --selector env=prod,bu=finance,tier=frontend
k rollout status deployment/myapp-dep
k rollout history deployment/myapp-dep
k apply -f deployment-definitin.yaml
<h1> Deployment definition file will have update</h1> 
k set image deployment/myapp-dep nginx=nginx:1.19 
<h1> Create Job </h1>
k create -f job-definition.yaml
k create job throw-dice-job --image=kodekloud/throw-dice
k get jobs 
k delete job math-job
<h1> Create Cron Job </h1>
k create -f cron-job-definition.yaml
k get cronjob
k rollout undo deployment/myapp-dep
k create -f deployment-definitin.yaml
kubectl create deployment nginx --image=nginx:1.16
<h1> Rollout update </h1>
kubectl rollout status deployment nginx
k rollout history deployment nginx
kubectl rollout history deployment nginx --revision=1
kubectl rollout undo deployment nginx --to-revision=1
kubectl describe deployments nginx | grep -i image:

k get deployments
<h1> NETWORK POLICIES </h1>
k get netpolicies
k get netpol
kubectl create ingress <ingress-name> --rule="host/path=service:port"
kubectl create ingress ingress-test --rule="wear.my-online-store.com/wear*=wear-service:80"
<h1> INGRESS RESOURCE </h1>
k get ingress --all-namespaces
k describe ingress -n app-space
kubectl create ingress mypay -n critical-space --rule="/pay=pay-service:8282"
kubectl create ingress ingress-wear-watch --rule="/wear=wear-service:8080" --rule="/watch=video-service:8080" -n app-space
<h1> GET ROLE & ROLEBINDINGS </h1>
k get role -n ingress-space 
k get rolebindings -n ingress-space 
k describe role ingress-role -n ingress-space 
k describe rolebindings ingress-role-binding -n ingress-space
k expose deployment ingress-controller -n ingress-space --name ingress --port=80 --target-port=80 --type NodePort
<h1> STORAGE CLASS </h1>
k get sc
<h1> ANNOTATION </h1>
annotations:
  nginx.ingress.kubernetes.io/rewrite-target: /
  nginx.ingress.kubernetes.io/ssl-redirect: "false"
<h1> Create Persistent Volume </h1>
k get persistentvolume
k get persistentvolumeclaim
k delete persistentvolume myclaim
