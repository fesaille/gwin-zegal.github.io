## K8S components

![Node components](https://d33wubrfki0l68.cloudfront.net/7016517375d10c702489167e704dcb99e570df85/7bb53/images/docs/components-of-kubernetes.png)

### Control Plane Components

* **kube-apiserver** exposes K8S API.
* **etcd** is used as Kubernetes' store for all cluster data.
* **kube-scheduler** watches and decide on why node to run newly created pods.
* **kube-controller-manager** 
      - *Node controller*: notices and responds when nodes go down.
      - *Replication controller*: maintains the correct number of pods for every replication controller object
      - *Endpoints controller*: populates the Endpoints object (that is, joins Services & Pods).
      - *Service Account & Token controllers*: creates default accounts and API access tokens.
* **cloud-controller-manager** embeds cloud-specific control logic, e.g.:
     * *Node controller*: checks the cloud provider to determine if a node has been deleted in the cloud after it stops responding
     * *Route controller*: sets up routes
     * *Service controller*: creates, updates and deletes cloud provider load balancers

### Node Components

* **kubelet** is an agent running on each node that starts and monitor the container runtime workloads.
* **kube-proxy** routes inter-pod and internet requests.
* **Container runtime** is responsible for running containers (usually Docker).
