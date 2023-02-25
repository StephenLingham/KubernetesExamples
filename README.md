# Summary sheet of useful commands

Further command summaries are available in the kubernetes documentation here:
https://kubernetes.io/docs/reference/kubectl/cheatsheet/

### Aliases

- `alias k=kubectl`

### Misc

- `kubectl api-resources -o wide`
- `kubectl api-resources --api-group apps -o wide`
- `kubectl explain replicaset --api-version apps/v1`
- `kubectl api-versions`
- `kubectl edit rs [replica set name]`
- `kubectl describe rs [rs name] | grep -i image`
- `kubectl scale rs [rs name] --replicas [num replicas]`
- `kubectl get all`
- `kubectl delete all --all`
- `kubectl rollout status deploy [deployment name]`
- `kubectl rollout history deploy [deployment name]`
- `kubectl create cm [config map name] --from-literal=[key]=[value]`
- `kubectl get resourcequota -n [namespace]` **// Gets the resource quota for a namespace showing the memory and CPU limits**

### Config

- `kubectl config view` **// View the config**
- `kubectl config current-context` **// Get the current context**
- `kubectl config set-context --current --namespace=[namespace name]` **// Set the namespace**
- `kubectl config view -o jsonpath='{..namespace}'` **// Get the current namespace if it's set**

### Pods

- `kubectl create -f [pod-definition.yaml]`
- `kubectl apply -f [pod-definition.yaml]`
- `kubectl get pods --all-namespaces`
- `kubectl get pods -n [namespace]`
- `kubectl get pods -o wide`
- `kubectl get pod [pod name] -o jsonpath='{.spec.containers[*].name}'` **// Get names of the containers in a pod**
- `kubectl get pod [pod name] -o jsonpath='{.spec.containers[*].image}'` **// Get the image for each container in a pod**
- `kubectl delete pod [pod name]`
- `kubectl delete --all pods`
- `kubectl get pod [pod-name] -o yaml > pod-definition.yaml`
- `kubectl run [pod name] --image [image name] -l [label=value]`
- `kubectl run [pod name] --image [image] --port [port] --expose`
- `kubectl run [pod name] --image [image] --dry-run=client -o yaml > pod-definition.yaml`
- `kubectl exec [pod name] -- [command e.g. whoami]`
- `kubectl exec -it [pod name] -n [namespace] -- [command e.g. bash or sh]`
- `kubectl explain pod --recursive | less`
- `kubectl explain pod -- recursive | grep -A5 tolerations`
- `kubectl explain pods --recursive | grep envFrom -A3`

### Imperative commands

- `kubectl expose pod [pod name] --port [port] --name [name]`
- `kubectl run [pod name] --image [image] --port [port]`
- `kubectl create deployment [name] --image [image]`
- `kubectl scale deploy [name] --replicas [number]`

### Create deployment yaml file

- `kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml`

### Create service yaml file

- `kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml`
- `kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml`

### Create a Service named nginx of type NodePort to expose pod nginx's port 80 on port 30080 on the nodes

- `kubectl expose pod nginx --port=80 --name nginx-service --type=NodePort --dry-run=client -o yaml`
- `kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml`

### Service account commands

- `kubectl get serviceaccounts`
- `kubectl create serviceaccount [service account name]`

### Taints and tolerations commands

- `kubectl taint nodes [node name] key=value:effect`
- `kubectl taint nodes [node name] [taint key]-`

### Node selectors and node affinity

- `kubectl label nodes [node name] [label key]=[label value]`
- `kubectl label nodes [node name] [label key]-`

### Observability

- `k logs [pod name] [container name]`
- `k top` **// Provides a list of all running pods or nodes with a snapshot of their resource utilisation**
- `k top pod --namespace [namespace]`
- `k top node`
