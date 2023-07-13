<h1> Set alias k to kubectl </h1>
<pre>
alias k=kubectl</pre>
<h1> Create nginx pod </h1>
<pre>kubectl run mynginx --image=nginx
kubectl run nginx-pod --image=nginx:alpine
kubectl get pods</pre>
<h1> Displays node on which pod is running </h1>
<pre>k get po -o wide </pre>
<h1> Get pods from ALL NAMESPACES </h1>
<pre>k get pods -A 
kubectl describe pod newpods-77pqk
kubectl delete pod webapp</pre>
<h1> DELETE ALL PODS </h1>
<pre>k delete pod -l name=busybox-pod 
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
 or kubectl get ns</pre>
<h1> Create Namespace </h1>
<pre>kubectl create ns dev-ns
kubectl scale --replicas=2 rs/new-replica-set
kubectl get all
kubectl get pods --all-namespaces
kubectl get pods --namespace=research
kubectl get deployments</pre>
<h1> CREATE DEPLOYMENT </h1>
<pre>kubectl create deployment --image=nginx nginx
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
k get pods -n elastic-stack</pre>
<h1> GET LOGS FROM POD </h1>
<pre>k logs app -n elastic-stack
k replace --force -f m.yaml
kubectl get pod webapp-color -o yaml > pod.yaml
kubectl create -f redis.yaml --namespace=finance</pre>
<h1> CHANGE NAMESPACE FOR CURRENT CONTEXT </h1>
<pre>kubectl config set $(kubectl config current-context) --namespace=dev </pre>
<h1> Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379 </h1>
<pre>kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml</pre>

<h1>CREATE POD & SERVICE AT ONCE</h1>
<pre>kubectl run httpd --image=httpd:alpine --port=80 --expose=true

kubectl get svc
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
k expose deploy/simple-webapp-deployment --port=8080 --target-port=8080 --type=NodePort --name=webapp-service --node-port=30080 --dry-run=client -o yaml
kubectl expose pod redis --port=6379 --name=redis-service
kubectl expose pod httpd --port=80 --name httpd
</pre>
<h1>Access service in browser</h1>
<pre>
kubectl port-forward --address 0.0.0.0 svc/nginx 8080:80
    Forwarding from 0.0.0.0:8080 -> 80
    Handling connection for 8080
kubectl proxy --address 0.0.0.0 --accept-hosts '.*'
  Starting to serve on [::]:8001
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
curl https://192.618.56.72:6443/api -insecure --header "Authorization: Bearer eykskdfj34" </pre>
<h1> APPLY CHANGES </h1>
<pre>kubectl apply -f dash.yaml </pre>
<h1> taint-effect NoSchedule|PreferNoSchedule|NoExecute </h1>
<pre>kubectl taint nodes node-name key=value:taint-effect 
kubectl taint node node01 "spray"="mortein":NoSchedule</pre>
<h1> REMOVE TAINT from Node (Add name of taint and '-') </h1>
<pre>kubectl taint node controlplane node-role.kubernetes.io/master:NoSchedule-
kubectl describe node kubemaster | grep Taint
kubectl get nodes
kubectl label nodes <node-name> <label-key>=<label-value>
kubectl create deployment blue --image=nginx --replicas=3
k logs kibana -n elastic-stack
k -n elastic-stack exec -it app -- cat /log/app.log
k logs -f event-simulator-pod event-simulator
k logs -f <pod-name> <container-name> </pre>
<h1> IDENTITY Node that consumes most memory </h1>
k top node
<h1> IDENTITY pod that consumes most memory </h1>
<pre>k top pod  
k get pods --selector app=App1
k get all --selector env=prod
k get pods --selector env=prod,bu=finance,tier=frontend
k rollout status deployment/myapp-dep
k rollout history deployment/myapp-dep
k apply -f deployment-definitin.yaml</pre>
<h1> Deployment definition file will have update</h1> 
<pre>k set image deployment/myapp-dep nginx=nginx:1.19 </pre>
<h1> Create Job </h1>
<pre>k create -f job-definition.yaml
k create job throw-dice-job --image=kodekloud/throw-dice
k get jobs 
k delete job math-job
<h1> Create Cron Job </h1>
k create -f cron-job-definition.yaml
k get cronjob
k rollout undo deployment/myapp-dep
k create -f deployment-definitin.yaml
kubectl create deployment nginx --image=nginx:1.16</pre>
<h1> Rollout update </h1>
<pre>kubectl rollout status deployment nginx
k rollout history deployment nginx
kubectl rollout history deployment nginx --revision=1
kubectl rollout undo deployment nginx --to-revision=1
kubectl describe deployments nginx | grep -i image:

k get deployments</pre>
<h1> NETWORK POLICIES </h1>
<pre>k get netpolicies
k get netpol
kubectl create ingress <ingress-name> --rule="host/path=service:port"
kubectl create ingress ingress-test --rule="wear.my-online-store.com/wear*=wear-service:80"</pre>
<h1> INGRESS RESOURCE </h1>
<pre>k get ingress --all-namespaces
k describe ingress -n app-space
kubectl create ingress mypay -n critical-space --rule="/pay=pay-service:8282"
kubectl create ingress ingress-wear-watch --rule="/wear=wear-service:8080" --rule="/watch=video-service:8080" -n app-space</pre>
<h1> GET ROLE & ROLEBINDINGS </h1>
<pre>k get role -n ingress-space 
k get rolebindings -n ingress-space 
k describe role ingress-role -n ingress-space 
k describe rolebindings ingress-role-binding -n ingress-space
k expose deployment ingress-controller -n ingress-space --name ingress --port=80 --target-port=80 --type NodePort</pre>
<h1> STORAGE CLASS </h1>
<pre>k get sc</pre>
<h1> ANNOTATION </h1>
<pre>annotations:
  nginx.ingress.kubernetes.io/rewrite-target: /
  nginx.ingress.kubernetes.io/ssl-redirect: "false"</pre>
<h1> Create Persistent Volume </h1>
<pre>k get persistentvolume
k get persistentvolumeclaim
k delete persistentvolume myclaim</pre>
<h1>List of shortnames</h1>
<pre>
componentstatuses = cs
configmaps = cm
endpoints = ep
events = ev
limitranges = limits
namespace = n
namespaces = ns
nodes = no
persistentvolumeclaims = pvc
persistentvolumes = pv
pods = po
replicationcontrollers = rc
resourcequotas = quota
serviceaccounts = sa
services = svc
customresourcedefinitions = crd, crds
daemonsets = ds
deployments = deploy
replicasets = rs
statefulsets = sts
horizontalpodautoscalers = hpa
cronjobs = cj
certificiaterequests = cr, crs
certificates = cert, certs
certificatesigningrequests = csr
ingresses = ing
networkpolicies = netpol
podsecuritypolicies = psp
replicasets = rs
scheduledscalers = ss
priorityclasses = pc
storageclasses = sc
</pre>
<h1>Check health of ETCD database</h1>
<pre>
 kubectl -n kube-system exec -it etcd-ip-172-31-88-75 -- sh -c \
"ETCDCTL_API=3 \
ETCDCTL_CACERT=/etc/kubernetes/pki/etcd/ca.crt \
ETCDCTL_CERT=/etc/kubernetes/pki/etcd/server.crt \
ETCDCTL_KEY=/etc/kubernetes/pki/etcd/server.key \
etcdctl endpoint health"
</pre>
<h1>NETWORK COMMANDS</h1>
<pre>
ip link
ip addr
ip addr add 192.168.1.10/24 dev eth0
ip route
ip route add 192.168.1.10/24  via 192.168.2.1
cat /proc/sys/net/ipv4/ip_forward
arp
route
netstat -tnlp
</pre>
<h1>How to remove PVC, Pod stuck at terminating state</h1>
<h2>I noticed that one PVC was stuck in “terminating” status for quite a while.</h2><br>
 <br>kubectl get volumeattachment
 <br>
 <pre>
kubectl patch pvc <PVC_NAME> -p '{"metadata":{"finalizers": []}}' --type=merge
</pre>
PVC will be delete after patching. Now delete pod forcefully<br>
k delete po web-0 --force
<h1>How to fix kubernetes disk pressure</h1>
Here are the Linux commands to check this on your Node:

memory.available<100Mi <br>
<pre>free -hm | awk 'NR==2{print $7}' #output has to be higher than 100Mi</pre>
nodefs.available<10%<br> <pre>df -h / | awk 'NR==2{print $5}' #output has to be lower than 90%</pre>
imagefs.available<15% <br>
containerd: <br><pre>df -h /var/lib/containerd/io.containerd.snapshotter.v1.overlayfs | awk 'NR==2{print $5}' #output has to be lower than 85%</pre>
docker: <br><pre>df -h /var/lib/docker | awk 'NR==2{print $5}' #output has to be lower than 85%</pre>
nodefs.inodesFree<5% (Linux nodes) <br> <pre>df -i / | awk 'NR==2{print $5}' #output has to be lower than 95%</pre>
<br>To get a overview to where all your storage went use:<br> <pre>du / -d 1 -h 2> /dev/null | sort -hr </pre>
<br>Using crictl tool to identify and remove unused images<br>
<pre>crictl rmi -q</pre>
<h3>If this does not work, this likely indicates that your workload is simply trying to use more disk space than is available.<br>
If this is the case, your options are to reduce your disk usage or to increase the total disk space on your nodes.</h3>
<h1>INGRESS ERROR: failed calling webhook "validate.nginx.ingress.kubernetes.io": failed to call webhook</h1>
<pre>kubectl create -f ingress.yaml </pre>
Above command fails. Then run below command:<br>
<pre>kubectl api-resources --namespaced=false
NAME                              SHORTNAMES   APIVERSION                             NAMESPACED   KIND
componentstatuses                 cs           v1                                     false        ComponentStatus
namespaces                        ns           v1                                     false        Namespace
nodes                             no           v1                                     false        Node
persistentvolumes                 pv           v1                                     false        PersistentVolume
mutatingwebhookconfigurations                  admissionregistration.k8s.io/v1        false        MutatingWebhookConfiguration
validatingwebhookconfigurations                admissionregistration.k8s.io/v1        false        ValidatingWebhookConfiguration
</pre>
Delete validatingwebhookconfigurations resource<br>
<pre>kubectl delete validatingwebhookconfigurations ingress-nginx-admission</pre>
<p>Run again below command</p>
<pre>kubectl create -f ingress.yaml 
ingress.networking.k8s.io/ingress-test created</pre>

