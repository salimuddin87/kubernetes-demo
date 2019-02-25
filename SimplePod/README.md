Simple Pod Demonstration
========================================================
$ kubectl create -f pod-nginx.yml
pod/nginx-pod created

$ kubectl get pods
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          98s

$ kubectl describe pod nginx-pod
Name:               nginx-pod
Namespace:          default
Priority:           0
PriorityClassName:  <none>
Node:               minikube/10.0.2.15
Start Time:         Sun, 24 Feb 2019 22:33:42 +0530
Labels:             app=demo
                    env=test
Annotations:        <none>
Status:             Running
IP:                 172.17.0.7
Containers:
  nginx:
    Container ID:   docker://a3fe14788414ff1136bd2857715fd0812c5b8f5c12d4768db81cec7d2f67b246
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:dd2d0ac3fff2f007d99e033b64854be0941e19a2ad51f174d9240dda20d9f534
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Sun, 24 Feb 2019 22:34:08 +0530
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-gxsvn (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  default-token-gxsvn:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-gxsvn
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  2m39s  default-scheduler  Successfully assigned default/nginx-pod to minikube
  Normal  Pulling    2m38s  kubelet, minikube  pulling image "nginx"
  Normal  Pulled     2m14s  kubelet, minikube  Successfully pulled image "nginx"
  Normal  Created    2m14s  kubelet, minikube  Created container
  Normal  Started    2m13s  kubelet, minikube  Started container

$ kubectl expose pod nginx-pod --type=NodePort
service/nginx-pod exposed

$ kubectl get svc
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
nginx-pod    NodePort    10.106.129.217   <none>        80:32267/TCP   40s

$ kubectl describe svc nginx-pod
Name:                     nginx-pod
Namespace:                default
Labels:                   app=demo
                          env=test
Annotations:              <none>
Selector:                 app=demo,env=test
Type:                     NodePort
IP:                       10.106.129.217
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
NodePort:                 <unset>  32267/TCP
Endpoints:                172.17.0.7:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>

$ open http://<Node IP>:<NodePort>
$ open http://http://192.168.99.103:32267/

########################################################
# For reverse engineering
$ kubectl get pod nginx-pod -o json

$ kubectl get pod nginx-pod -o yml
error: unable to match a printer suitable for the output format "yml", allowed formats are: custom-columns,custom-column
s-file,go-template,go-template-file,json,jsonpath,jsonpath-file,name,template,templatefile,wide,yaml

$ kubectl get pod nginx-pod -o yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2019-02-24T17:03:42Z"
  labels:
    app: demo
    env: test
  name: nginx-pod
  namespace: default
  resourceVersion: "205774"
  selfLink: /api/v1/namespaces/default/pods/nginx-pod
  uid: 2373aa09-3856-11e9-ab04-08002770c12c
spec:
  containers:
  - image: nginx
    imagePullPolicy: Always
    name: nginx
    ports:
    - containerPort: 80
      name: http
      protocol: TCP
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: default-token-gxsvn
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: minikube
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - name: default-token-gxsvn
    secret:
      defaultMode: 420
      secretName: default-token-gxsvn
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2019-02-24T17:03:42Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2019-02-24T17:04:09Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2019-02-24T17:04:09Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2019-02-24T17:03:42Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: docker://a3fe14788414ff1136bd2857715fd0812c5b8f5c12d4768db81cec7d2f67b246
    image: nginx:latest
    imageID: docker-pullable://nginx@sha256:dd2d0ac3fff2f007d99e033b64854be0941e19a2ad51f174d9240dda20d9f534
    lastState: {}
    name: nginx
    ready: true
    restartCount: 0
    state:
      running:
        startedAt: "2019-02-24T17:04:08Z"
  hostIP: 10.0.2.15
  phase: Running
  podIP: 172.17.0.7
  qosClass: BestEffort
  startTime: "2019-02-24T17:03:42Z"
