# Cheat sheet of useful commands

### Aliases

* alias k=kubectl

### Misc

* kubectl api-resources -o wide
* kubectl api-resources --api-group apps -o wide
* kubectl explain replicaset --api-version apps/v1
* kubectl api-versions
* kubectl edit rs [replica set name]
* kubectl describe rs [rs name] | grep -i image
* kubectl scale rs [rs name] --replicas [num replicas]
* kubectl get all
* kubectl delete all --all
* kubectl rollout status deploy [deployment name]
* kubectl rollout history deploy [deployment name]
* kubectl config set-context $(kubectl config current-context) --namespace dev
* kubectl create cm [config map name] --from-literal=[key]=[value]
* kubectl explain pods --recursive | grep envFrom -A3

### Pod commands

* kubectl create -f [pod-definition.yaml]
* kubectl apply -f [pod-definition.yaml]
* kubectl get pods --all-namespaces
* kubectl get pods -n [namespace]
* kubectl get pods -o wide
* kubectl delete pod [pod name]
* kubectl delete --all pods
* kubectl get pod [pod-name] -o yaml > pod-definition.yaml
* kubectl run [pod name] --image [image name] -l [label=value]
* kubectl run [pod name] --image [image] --port [port] --expose
* kubectl run [pod name] --image [image] --dry-run=client -o yaml > pod-definition.yaml
* kubectl exec [pod name] -- [command e.g. whoami]
* kubectl exec -it [pod name] -n [namespace] -- [command e.g. bash or sh]
* kubectl explain pod --recursive | less
* kubectl explain pod -- recursive | grep -A5 tolerations

### Imperative commands

* kubectl expose pod [pod name] --port [port] --name [name]
* kubectl run [pod name] --image [image] --port [port]
* kubectl create deployment [name] --image [image]
* kubectl scale deploy [name] --replicas [number]

### Create deployment yaml file

* kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml

### Create service yaml file

* kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
* kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml

### Create a Service named nginx of type NodePort to expose pod nginx's port 80 on port 30080 on the nodes

* kubectl expose pod nginx --port=80 --name nginx-service --type=NodePort --dry-run=client -o yaml
* kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml

### Service account commands

* kubectl get serviceaccounts
* kubectl create serviceaccount [service account name]

### Taints and tolerations commands

* kubectl taint nodes [node name] key=value:effect
* kubectl taint nodes [node name] [taint key]-

### Node selectors and node affinity

* kubectl label nodes [node name] [label key]=[label value]
* kubectl label nodes [node name] [label key]-
