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
2. Controller - Keeps track of whats happening in the cluster. Ex - checks desired state == actual state
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
3. It is also a load balancer.

##### Ingress (External Service)
1. Any request to k8s node goes to Ingress and then Ingress pass the request to service. 
2. Ingress also help in hiding url of actual service running in cluster.

##### Configmap
1. External configuration of your application. Ex - Database URL
2. It is for non-confidential data only.

##### Secret
1. Used to store secret data. Ex - Database user and password.
2. Store data in base64 format.
3. Reference Secret in Deployment/Pod using ENV variable.

##### Volume
1. It is being used for persistancy.
2. External hard disk can be plugged to pod using volume.
3. Kubernetes doesn't manage data persistance.

##### Deployments (stateless)
1. Blueprint for pods you want to create.
2. Specify no of replica and scale up/down.

##### Statefulset
1. DB can't be replicated via Deployment. Because DB has a state which is it's data.
2. If we replicate DB then they all have to access same shared data storage for read/write which may lead to data inconsistency.
