##### Kubernetes
A open source container orchestration tool initially developed by Google.

##### Features of Kubernetes
1. High availability or no downtime
2. Scalability or high performance
3. Disaster recovery - backup and restore

##### kubelet
1. An agent which runs on each node.
2. Responsible for communication between nodes.
3. Helps in running applicatons.

##### K8s Components
1. API server - Entry point to k8s cluster.
2. Controller - Keeps track of whats happening in the cluster.
3. Scheduler - Ensures pods placement on different nodes.
4. etcd(key-value storage) - current state of k8s cluster.
5. virtual network - crates one unified machine.

##### Pod
1. Smallest unit in kubernetes.
2. Abstraction over container.
3. Each pods gets it's own new IP address whenever it is being created.

##### Service (Internal Service)
1. Permanent IP address attached to pod to communicate.
2. Lifecycle of pod and service are not connected.

##### Ingress (External Service)
Any request to k8s node goes to Ingress and then Ingress pass the request to service. 
Ingress also help in hiding url of actual service running in cluster.

