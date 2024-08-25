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

<h3>Install ingress-nginx <a href="https://github.com/kubernetes/ingress-nginx/blob/main/docs/deploy/index.md">Click here</a></h3>

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
<pre>crictl rmi --prune</pre>
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
<h1>Solved "Error while dialing dial unix /var/run/dockershim.sock"</h1>
<p>When trying list containers or images using below command, below error is thrown:</p>
<pre>
 ubuntu@ip-172-31-88-75:~$ crictl ps
E0714 03:59:49.377713    1892 remote_runtime.go:390] "ListContainers with filter from runtime service failed" err="rpc error: code = Unavailable desc = connection error: desc = \"transport: Error while dialing dial unix /run/containerd/containerd.sock: connect: permission denied\"" filter="&ContainerFilter{Id:,State:&ContainerStateValue{State:CONTAINER_RUNNING,},PodSandboxId:,LabelSelector:map[string]string{},}"
FATA[0002] listing containers: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing dial unix /run/containerd/containerd.sock: connect: permission denied" 
ubuntu@ip-172-31-88-75:~$ crictl img
E0714 04:03:07.460050    5529 remote_image.go:119] "ListImages with filter from image service failed" err="rpc error: code = Unavailable desc = connection error: desc = \"transport: Error while dialing dial unix /run/containerd/containerd.sock: connect: permission denied\"" filter="&ImageFilter{Image:&ImageSpec{Image:,Annotations:map[string]string{},},}"
FATA[0000] listing images: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing dial unix /run/containerd/containerd.sock: connect: permission denied" 
</pre>
<p>Before fixing above error, you need to first check the currently installed container runtime in your System by using kubectl get nodes -o wide command as shown below.</p>
<pre>
 ubuntu@ip-172-31-88-75:~$ k get no -o wide
NAME              STATUS     ROLES           AGE   VERSION   INTERNAL-IP    EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION    CONTAINER-RUNTIME
ip-172-31-80-7    NotReady   <none>          23d   v1.25.1   172.31.80.7    <none>        Ubuntu 20.04.6 LTS   5.15.0-1039-aws   containerd://1.6.21
ip-172-31-88-75   Ready      control-plane   23d   v1.26.1   172.31.88.75   <none>        Ubuntu 20.04.6 LTS   5.15.0-1039-aws   containerd://1.6.21
worker            Ready      <none>          17d   v1.26.1   172.31.95.67   <none>        Ubuntu 20.04.6 LTS   5.15.0-1039-aws   containerd://1.6.21
</pre>
<p>As you can see from above, it is containerd runtime in our case. So the error is simply because I have configured dockershim endpoint to be used in crictl configuration which I don't have in my local system. So to fix the above error, I reconfigured crictl endpoint to use containerd runtime instead of dockershim using below command.</p>
<pre>
echo "===================================" &&\
echo "Config BEFORE change:" &&\
sudo cat /etc/crictl.yaml &&\
sudo crictl config --set runtime-endpoint=unix:///run/containerd/containerd.sock --set image-endpoint=unix:///run/containerd/containerd.sock &&\
echo "===================================" &&\
echo "Config AFTER change:" &&\
sudo cat /etc/crictl.yaml
</pre>
<p>Now run <pre>crictl img</pre> or <pre>crictl ps</pre>, it works:</p>
<pre>ubuntu@ip-172-31-88-75:~$ crictl img
IMAGE                                     TAG                 IMAGE ID            SIZE
docker.io/calico/cni                      v3.25.0             d70a5947d57e5       88MB
docker.io/calico/kube-controllers         v3.25.0             5e785d005ccc1       31.3MB
docker.io/calico/node                     v3.25.0             08616d26b8e74       87.2MB
...
 ubuntu@ip-172-31-88-75:~$ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
3081914fada00       5185b96f0becf       13 minutes ago      Running             coredns                   25                  64c5d46f086a1       coredns-787d4945fb-rxzcm
f517b7be7b44e       5185b96f0becf       13 minutes ago      Running             coredns                   25                  5974563a46ccb       coredns-787d4945fb-2dvg2
</pre>
<h1>Solved "Error while dialing dial unix /run/containerd/containerd.sock: connect: permission denied</h1>
Change permission /run/containerd/containerd.sock to 666:
<pre>chmod 666 /run/containerd/containerd.sock
[ec2-user@centosworker ~]$ sudo chmod 666 /var/run/crio/crio.sock
 CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
5e8ef5ac8a88b       46a6bb3c77ce0       43 minutes ago      Running             kube-proxy                34                  7849a2c8836c8       kube-proxy-2gf9z
b28972334bd00       deb04688c4a35       44 minutes ago      Running             kube-apiserver            36                  b7aa5fb37b3ed       kube-apiserver-ip-172-31-88-75
</pre>
<h1>Solved Error Pods stuck in Terminating status</h1>
<pre>
 NAME                        READY   STATUS        RESTARTS   AGE
nginx                       0/1     Terminating   0          7h53m
</pre>
<h3>You can use following command to delete the POD forcefully.</h3>
<pre>
 kubectl delete pod <PODNAME> --grace-period=0 --force --namespace <NAMESPACE>

 [ec2-user@centosworker ~]$ k delete po nginx --grace-period=0 --force
Warning: Immediate deletion does not wait for confirmation that the running resource has been terminated. The resource may continue to run on the cluster indefinitely.
pod "nginx" force deleted
</pre>
<h1>plugin type=\"calico\" failed (delete) error getting clusterinformation: connection is unauthorized: unauthorized" podsandbox</h1>
Above error causes pod to get stuck in ContainerCreating:<br>
<pre>
 ubuntu@ip-172-31-88-75:~$ k get po
NAME                        READY   STATUS              RESTARTS   AGE
nginx                       0/1     ContainerCreating   0          36m
</pre>
Add the following environment variables for the calico-node container in the manifest of the calico-node DaemonSet:
CALICO_MANAGE_CNI="false". <br>
In calico.yaml, search DaemonSet named calico-node and add environment variable CALICO_MANAGE_CNI with false value as below:<br>
<pre>
kind: DaemonSet
apiVersion: apps/v1
metadata:
  name: calico-node
  namespace: kube-system
  labels:
    k8s-app: calico-node
 ...
           env:
            - name: CALICO_MANAGE_CNI
              value: "false"
</pre>
<h3>Apply the calico policy change by running below command:</h3>
<pre>
ubuntu@ip-172-31-88-75:~$ k apply -f calico.yaml 
poddisruptionbudget.policy/calico-kube-controllers configured
serviceaccount/calico-kube-controllers unchanged
serviceaccount/calico-node created
configmap/calico-config created
 ...
ubuntu@ip-172-31-88-75:~$ k get po -w
NAME     READY   STATUS    RESTARTS   AGE
nginx    1/1     Running   0          46m
</pre>
<h1>Set Up an Alias for Kubectl and Enable for Auto-completion</h1>
<pre>
 echo 'alias k=kubectl' >>~/.bashrc
 echo 'complete -o default -F __start_kubectl k' >>~/.bashrc
 source ~/.bashrc
 k - <TAB><TAB> #to test if auto-completion works
</pre>
<h1>Backup resource configuration</h1>
<pre>k get all -A -o yaml > all-deployed-svc.yaml</pre>
<h1>Set up Auto-completion</h1>
<p>Check if bash-completion is already installed:</p>
<pre>type _init_completion
 apt-get install bash-completion 
 or
 yum install bash-completion
</pre>
  <p>Set the kubectl completion script source for your shell sessions:</p>
<pre>
 kubectl completion bash | sudo tee /etc/bash_completion.d/kubectl > /dev/null
</pre>
<p>After installing the auto-complete I will reload the Bash shell using the line below.</p>
<pre>source /usr/share/bash-completion/bash_completion</pre>
<p>Set an alias for kubectl as k</p>
<pre>echo 'alias k=kubectl' >>~/.bashrc
echo 'complete -o default -F __start_kubectl k' >>~/.bashrc
</pre>
<h1>Check memory utilization </h1>
<pre>
 # ps -o pid,user,%mem,command ax | sort -b -k3 -r
 PID USER     %MEM COMMAND
 1234 mysql    25.0 /usr/sbin/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=/usr/lib64/mysql/plugin --user=mysql --log-error=/var/log/mysqld.log --pid-file=/var/run/mysqld/mysqld.pid --socket=/var/lib/mysql/mysql.sock
 5678 apache    1.3 /usr/sbin/httpd
</pre>

<h1>How to get public ip address of your linux machin</h1>
<h2>If you're not sure about your server's public IP address, run the command below to print it to the standard output:</h2>
<pre>curl -4 icanhazip.com</pre>
<br> OR (only for AWS cloud)<br>
<pre>curl http://checkip.amazonaws.com</pre>
<br><h1>Vim Editor setting</h1>
<br>
<pre>
 set expandtab
set tabstop=2
set shiftwidth=2
set autoindent
set smartindent
set bg=dark
set nowrap
set paste
</pre>
<h2>Error-Failed to create pod sandbox: open /run/systemd/resolve/resolv.conf: no such file or directory</h2>
<br>
As your system has systemd-resolved installed and running, it would be the preferred mechanism here. Symlink /etc/resolv.conf to either /run/systemd/resolve/resolv.conf for direct access to the configured DNS servers, or to /run/systemd/resolve/stub-resolv.conf for using systemd-resolved as a local DNS cache.
<hr>
