# CKA Exam Questions And Answers


## Schedule Pod on Master Node
Create a single Pod of image httpd:2.4.41-alpine in Namespace default. The Pod should be named pod1 and the container should be named pod1-container. This Pod should only be scheduled on a master node, do not add new labels any nodes.
Shortly write the reason on why Pods are by default not scheduled on master nodes into /opt/course/2/master_schedule_reason .

<details><summary>Show Answer</summary>
<p>

First we find the master node(s) and their taints:

``` bash
k get node # find master node

k describe node cluster1-master1 | grep Taint # get master node taints

k describe node cluster1-master1 | grep Labels -A 10 # get master node labels

k get node cluster1-master1 --show-labels # OR: get master node labels
```

Next we create the Pod template:

``` bash
# check the export on the very top of this document so we can use $do
k run pod1 --image=httpd:2.4.41-alpine $do > 2.yaml

vim 2.yaml
```

Perform the necessary changes manually. Use the Kubernetes docs and search for example for tolerations and nodeSelector to find examples:


``` yaml
# 2.yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: pod1
  name: pod1
spec:
  containers:
  - image: httpd:2.4.41-alpine
    name: pod1-container                  # change
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  tolerations:                            # add
  - effect: NoSchedule                    # add
    key: node-role.kubernetes.io/master   # add
  nodeSelector:                           # add
    node-role.kubernetes.io/master: ""    # add
status: {}
```

Important here to add the toleration for running on master nodes, but also the nodeSelector to make sure it only runs on master nodes. If we only specify a toleration the Pod can be scheduled on master or worker nodes.

Now we create it:
``` bash
k -f 2.yaml create
```

Let's check if the pod is scheduled:

``` bash
➜ k get pod pod1 -o wide
NAME   READY   STATUS    RESTARTS   ...    NODE               NOMINATED NODE
pod1   1/1     Running   0          ...    cluster1-master1   <none>     

```


Finally the short reason why Pods are not scheduled on master nodes by default:

``` bash
# /opt/course/2/master_schedule_reason
master nodes usually have a taint defined
```

</p>
</details>


## Storage, PV, PVC, Pod volume

Create a new PersistentVolume named safari-pv. It should have a capacity of 2Gi, accessMode ReadWriteOnce, hostPath /Volumes/Data and no storageClassName defined.

Next create a new PersistentVolumeClaim in Namespace project-tiger named safari-pvc . It should request 2Gi storage, accessMode ReadWriteOnce and should not define a storageClassName. The PVC should bound to the PV correctly.

Finally create a new Deployment safari in Namespace project-tiger which mounts that volume at /tmp/safari-data. The Pods of that Deployment should be of image httpd:2.4.41-alpine.

<details><summary>Show Answer</summary>
<p>
``` bash
vim 6_pv.yaml
```
Find an example from https://kubernetes.io/docs and alter it:

``` yaml
# 6_pv.yaml
kind: PersistentVolume
apiVersion: v1
metadata:
 name: safari-pv
spec:
 capacity:
  storage: 2Gi
 accessModes:
  - ReadWriteOnce
 hostPath:
  path: "/Volumes/Data"
```
Then create it:
``` bash
k -f 6_pv.yaml create

```
Next the PersistentVolumeClaim:

``` bash
vim 6_pvc.yaml

```
Find an example from https://kubernetes.io/docs and alter it:

``` yaml
# 6_pvc.yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: safari-pvc
  namespace: project-tiger
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
     storage: 2Gi

```
Then create:

``` bash
k -f 6_pvc.yaml create

```
And check that both have the status Bound:

``` bash 
k -n project-tiger get pv,pvc
NAME                         CAPACITY  ... STATUS   CLAIM                    ...
persistentvolume/safari-pv   2Gi       ... Bound    project-tiger/safari-pvc ...

NAME                               STATUS   VOLUME      CAPACITY ...
persistentvolumeclaim/safari-pvc   Bound    safari-pv   2Gi      ...
Next we create a Deployment and mount that volume:

k -n project-tiger create deploy safari \
  --image=httpd:2.4.41-alpine $do > 6_dep.yaml

vim 6_dep.yaml
```
Alter the yaml to mount the volume:

``` yaml 
# 6_dep.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: safari
  name: safari
  namespace: project-tiger
spec:
  replicas: 1
  selector:
    matchLabels:
      app: safari
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: safari
    spec:
      volumes:                                      # add
      - name: data                                  # add
        persistentVolumeClaim:                      # add
          claimName: safari-pvc                     # add
      containers:
      - image: httpd:2.4.41-alpine
        name: container
        volumeMounts:                               # add
        - name: data                                # add
          mountPath: /tmp/safari-data               # add
```
``` bash 
k -f 6_dep.yaml create

```
We can confirm its mounting correctly:

``` bash
k -n project-tiger describe pod safari-5cbf46d6d-mjhsb  | grep -A2 Mounts:   
    Mounts:
      /tmp/safari-data from data (rw) # there it is
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-n2sjj (ro)
```
</p>
</details>


## RBAC ServiceAccount Role RoleBinding
Create a new ServiceAccount processor in Namespace project-hamster. Create a Role and RoleBinding, both named processor as well. These should allow the new SA to only create Secrets and ConfigMaps in that Namespace.

<details><summary>Show Answer</summary>
<p>

``` bash
k -n project-tiger describe pod safari-5cbf46d6d-mjhsb  | grep -A2 Mounts:   
    Mounts:
      /tmp/safari-data from data (rw) # there it is
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-n2sjj (ro)
```

Let's talk a little about RBAC resources
A ClusterRole|Role defines a set of permissions and where it is available, in the whole cluster or just a single Namespace.

A ClusterRoleBinding|RoleBinding connects a set of permissions with an account and defines where it is applied, in the whole cluster or just a single Namespace.

Because of this there are 4 different RBAC combinations and 3 valid ones:

Role + RoleBinding (available in single Namespace, applied in single Namespace)
ClusterRole + ClusterRoleBinding (available cluster-wide, applied cluster-wide)
ClusterRole + RoleBinding (available cluster-wide, applied in single Namespace)
Role + ClusterRoleBinding (NOT POSSIBLE: available in single Namespace, applied cluster-wide)

To the solution
We first create the ServiceAccount:

``` bash
k -n project-hamster create sa processor
serviceaccount/processor created
```
Then for the Role:

``` bash
k -n project-hamster create role -h # examples

```
So we execute:
``` bash
k -n project-hamster create role processor \
  --verb=create \
  --resource=secret \
  --resource=configmap
```
Which will create a Role like:

``` yaml 
# kubectl -n project-hamster create role accessor --verb=create --resource=secret --resource=configmap
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: processor
  namespace: project-hamster
rules:
- apiGroups:
  - ""
  resources:
  - secrets
  - configmaps
  verbs:
  - create

```
Now we bind the Role to the ServiceAccount:

``` bash
k -n project-hamster create rolebinding -h # examples

```

So we create it:

``` bash
k -n project-hamster create rolebinding processor \
  --role processor \
  --serviceaccount project-hamster:processor
```
This will create a RoleBinding like:

``` yaml 
# kubectl -n project-hamster create rolebinding processor --role processor --serviceaccount project-hamster:processor
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: processor
  namespace: project-hamster
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: processor
subjects:
- kind: ServiceAccount
  name: processor
  namespace: project-hamster
```

To test our RBAC setup we can use kubectl auth can-i:

```bash
k auth can-i -h # examples
```

Like this:

``` bash
k -n project-hamster auth can-i create secret \
  --as system:serviceaccount:project-hamster:processor
yes

k -n project-hamster auth can-i create configmap \
  --as system:serviceaccount:project-hamster:processor
yes

k -n project-hamster auth can-i create pod \
  --as system:serviceaccount:project-hamster:processor
no

k -n project-hamster auth can-i delete secret \
  --as system:serviceaccount:project-hamster:processor
no

k -n project-hamster auth can-i get configmap \
  --as system:serviceaccount:project-hamster:processor
no
```

</p>
</details>
 
##  DaemonSet on all Nodes
Use Namespace project-tiger for the following. Create a DaemonSet named ds-important with image httpd:2.4-alpine and labels id=ds-important and uuid=18426a0b-5f59-4e10-923f-c0e078e82462. The Pods it creates should request 10 millicore cpu and 10 mebibyte memory. The Pods of that DaemonSet should run on all nodes, master and worker.

<details><summary>Show Answer</summary>
<p>

As of now we aren't able to create a DaemonSet directly using kubectl, so we create a Deployment and just change it up:

``` bash
k -n project-tiger create deployment --image=httpd:2.4-alpine ds-important $do > 11.yaml
vim 11.yaml

```
(Sure yuu could also search for a DaemonSet example yaml in the Kubernetes docs and alter it.)
Then we adjust the yaml to:

``` yaml 
# 11.yaml
apiVersion: apps/v1
kind: DaemonSet                                     # change from Deployment to Daemonset
metadata:
  creationTimestamp: null
  labels:                                           # add
    id: ds-important                                # add
    uuid: 18426a0b-5f59-4e10-923f-c0e078e82462      # add
  name: ds-important
  namespace: project-tiger                          # important
spec:
  #replicas: 1                                      # remove
  selector:
    matchLabels:
      id: ds-important                              # add
      uuid: 18426a0b-5f59-4e10-923f-c0e078e82462    # add
  #strategy: {}                                     # remove
  template:
    metadata:
      creationTimestamp: null
      labels:
        id: ds-important                            # add
        uuid: 18426a0b-5f59-4e10-923f-c0e078e82462  # add
    spec:
      containers:
      - image: httpd:2.4-alpine
        name: ds-important
        resources:
          requests:                                 # add
            cpu: 10m                                # add
            memory: 10Mi                            # add
      tolerations:                                  # add
      - effect: NoSchedule                          # add
        key: node-role.kubernetes.io/master         # add
#status: {}                                         # remove
```
It was requested that the DaemonSet runs on all nodes, so we need to specify the toleration for this.
Let's confirm:

``` bash
k -f 11.yaml create
k -n project-tiger get ds
NAME           DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
ds-important   3         3         3       3            3           <none>          8s
k -n project-tiger get pod -l id=ds-important -o wide
NAME                      READY   STATUS          NODE
ds-important-6pvgm        1/1     Running   ...   cluster1-worker1
ds-important-lh5ts        1/1     Running   ...   cluster1-master1
ds-important-qhjcq        1/1     Running   ...   cluster1-worker2
```
</p>
</details>

##  Deployment on all Nodes
Use Namespace project-tiger for the following. Create a Deployment named deploy-important with label id=very-important (the Pods should also have this label) and 3 replicas. It should contain two containers, the first named container1 with image nginx:1.17.6-alpine and the second one named container2 with image kubernetes/pause.

There should be only ever one Pod of that Deployment running on one worker node. We have two worker nodes: cluster1-worker1 and cluster1-worker2. Because the Deployment has three replicas the result should be that on both nodes one Pod is running. The third Pod won't be scheduled, unless a new worker node will be added.

In a way we kind of simulate the behaviour of a DaemonSet here, but using a Deployment and a fixed number of replicas.

<details><summary>Show Answer</summary>
<p>

There are two possible ways, one using podAntiAffinity and one using topologySpreadConstraint.

### PodAntiAffinity
The idea here is that we create a "Inter-pod anti-affinity" which allows us to say a Pod should only be scheduled on a node where another Pod of a specific label (here the same label) is not already running.
Let's begin by creating the Deployment template:

``` bash
k -n project-tiger create deployment \
  --image=nginx:1.17.6-alpine deploy-important $do > 12.yaml

vim 12.yaml
```

Then change the yaml to:

``` yaml 
# 12.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    id: very-important                  # change
  name: deploy-important
  namespace: project-tiger              # important
spec:
  replicas: 3                           # change
  selector:
    matchLabels:
      id: very-important                # change
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        id: very-important              # change
    spec:
      containers:
      - image: nginx:1.17.6-alpine
        name: container1                # change
        resources: {}
      - image: kubernetes/pause         # add
        name: container2                # add
      affinity:                                             # add
        podAntiAffinity:                                    # add
          requiredDuringSchedulingIgnoredDuringExecution:   # add
          - labelSelector:                                  # add
              matchExpressions:                             # add
              - key: id                                     # add
                operator: In                                # add
                values:                                     # add
                - very-important                            # add
            topologyKey: kubernetes.io/hostname             # add
status: {}

```

Specify a topologyKey, which is a pre-populated Kubernetes label, you can find this by describing a node.

### TopologySpreadConstraints
We can achieve the same with topologySpreadConstraints. Best to try out and play with both.

``` yaml 
# 12.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    id: very-important                  # change
  name: deploy-important
  namespace: project-tiger              # important
spec:
  replicas: 3                           # change
  selector:
    matchLabels:
      id: very-important                # change
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        id: very-important              # change
    spec:
      containers:
      - image: nginx:1.17.6-alpine
        name: container1                # change
        resources: {}
      - image: kubernetes/pause         # add
        name: container2                # add
      topologySpreadConstraints:                 # add
      - maxSkew: 1                               # add
        topologyKey: kubernetes.io/hostname      # add
        whenUnsatisfiable: DoNotSchedule         # add
        labelSelector:                           # add
          matchLabels:                           # add
            id: very-important                   # add
status: {}
 
```

Apply and Run
Let's run it:

``` bash
k -f 12.yaml create
```

Then we check the Deployment status where it shows 2/3 ready count:

``` bash
k -n project-tiger get deploy -l id=very-important
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
deploy-important   2/3     3            2           2m35s
```

And running the following we see one Pod on each worker node and one not scheduled.

``` bash
k -n project-tiger get pod -o wide -l id=very-important
NAME                                READY   STATUS    ...   NODE             
deploy-important-58db9db6fc-9ljpw   2/2     Running   ...   cluster1-worker1
deploy-important-58db9db6fc-lnxdb   0/2     Pending   ...   <none>          
deploy-important-58db9db6fc-p2rz8   2/2     Running   ...   cluster1-worker2

```
If we kubectl describe the Pod deploy-important-58db9db6fc-lnxdb it will show us the reason for not scheduling is our implemented podAntiAffinity ruling:
Warning  FailedScheduling  63s (x3 over 65s)  default-scheduler  0/3 nodes are available: 1 node(s) had taint {node-role.kubernetes.io/master: }, that the pod didn't tolerate, 2 node(s) didn't match pod affinity/anti-affinity, 2 node(s) didn't satisfy existing pods anti-affinity rules.
Or our topologySpreadConstraints:
Warning  FailedScheduling  16s   default-scheduler  0/3 nodes are available: 1 node(s) had taint {node-role.kubernetes.io/master: }, that the pod didn't tolerate, 2 node(s) didn't match pod topology spread constraints.
 
</p>
</details>

## Multi Containers and Pod shared Volume
Create a Pod named multi-container-playground in Namespace default with three containers, named c1, c2 and c3. There should be a volume attached to that Pod and mounted into every container, but the volume shouldn't be persisted or shared with other Pods.

Container c1 should be of image nginx:1.17.6-alpine and have the name of the node where its Pod is running available as environment variable MY_NODE_NAME.

Container c2 should be of image busybox:1.31.1 and write the output of the date command every second in the shared volume into file date.log. You can use while true; do date >> /your/vol/path/date.log; sleep 1; done for this.

Container c3 should be of image busybox:1.31.1 and constantly send the content of file date.log from the shared volume to stdout. You can use tail -f /your/vol/path/date.log for this.

Check the logs of container c3 to confirm correct setup.

<details><summary>Show Answer</summary>
<p>

First we create the Pod template:
``` bash
k run multi-container-playground --image=nginx:1.17.6-alpine $do > 13.yaml
vim 13.yaml
``` 
And add the other containers and the commands they should execute:

``` yaml
# 13.yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: multi-container-playground
  name: multi-container-playground
spec:
  containers:
  - image: nginx:1.17.6-alpine
    name: c1                                                                      # change
    resources: {}
    env:                                                                          # add
    - name: MY_NODE_NAME                                                          # add
      valueFrom:                                                                  # add
        fieldRef:                                                                 # add
          fieldPath: spec.nodeName                                                # add
    volumeMounts:                                                                 # add
    - name: vol                                                                   # add
      mountPath: /vol                                                             # add
  - image: busybox:1.31.1                                                         # add
    name: c2                                                                      # add
    command: ["sh", "-c", "while true; do date >> /vol/date.log; sleep 1; done"]  # add
    volumeMounts:                                                                 # add
    - name: vol                                                                   # add
      mountPath: /vol                                                             # add
  - image: busybox:1.31.1                                                         # add
    name: c3                                                                      # add
    command: ["sh", "-c", "tail -f /vol/date.log"]                                # add
    volumeMounts:                                                                 # add
    - name: vol                                                                   # add
      mountPath: /vol                                                             # add
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  volumes:                                                                        # add
    - name: vol                                                                   # add
      emptyDir: {}                                                                # add
status: {}
```
``` bash
k -f 13.yaml create
```
Oh boy, lot's of requested things. We check if everything is good with the Pod:

``` bash
k get pod multi-container-playground
NAME                         READY   STATUS    RESTARTS   AGE
multi-container-playground   3/3     Running   0          95s
```

Good, then we check if container c1 has the requested node name as env variable:

``` bash
k exec multi-container-playground -c c1 -- env | grep MY
MY_NODE_NAME=cluster1-worker2
```
And finally we check the logging:

``` bash
k logs multi-container-playground -c c3
Sat Dec  7 16:05:10 UTC 2077
Sat Dec  7 16:05:11 UTC 2077
Sat Dec  7 16:05:12 UTC 2077
Sat Dec  7 16:05:13 UTC 2077
Sat Dec  7 16:05:14 UTC 2077
Sat Dec  7 16:05:15 UTC 2077
Sat Dec  7 16:05:16 UTC 2077

```

</p>
</details>
 




 


