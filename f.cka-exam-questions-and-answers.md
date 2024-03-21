# CKA Exam Questions And Answers


### Schedule Pod on Master Node

Use context: kubectl config use-context k8s-c1-H
Create a single Pod of image httpd:2.4.41-alpine in Namespace default. The Pod should be named pod1 and the container should be named pod1-container. This Pod should only be scheduled on a master node, do not add new labels any nodes.
Shortly write the reason on why Pods are by default not scheduled on master nodes into /opt/course/2/master_schedule_reason .

<details><summary>show</summary>
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



### Storage, PV, PVC, Pod volume

Use context: kubectl config use-context k8s-c1-H

 
Create a new PersistentVolume named safari-pv. It should have a capacity of 2Gi, accessMode ReadWriteOnce, hostPath /Volumes/Data and no storageClassName defined.

Next create a new PersistentVolumeClaim in Namespace project-tiger named safari-pvc . It should request 2Gi storage, accessMode ReadWriteOnce and should not define a storageClassName. The PVC should bound to the PV correctly.

Finally create a new Deployment safari in Namespace project-tiger which mounts that volume at /tmp/safari-data. The Pods of that Deployment should be of image httpd:2.4.41-alpine.
<details><summary>show</summary>
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


###  RBAC ServiceAccount Role RoleBinding

Use context: kubectl config use-context k8s-c1-H

Create a new ServiceAccount processor in Namespace project-hamster. Create a Role and RoleBinding, both named processor as well. These should allow the new SA to only create Secrets and ConfigMaps in that Namespace.

<details><summary>show</summary>
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
 