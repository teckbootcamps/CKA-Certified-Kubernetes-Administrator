# ☸️ Certified Kubernetes Administrator (CKA) Exam Guide - V1.31 (2024)

<p align="center">
  <img src="assets/cka.png" alt="CKA EXAM">
</p>

> This guide is part of our blog [Pass the CKA Certification Exam: The Complete Study Guide ](https://teckbootcamps.com/cka-exam-study-guide/).

## Hit the Star! :star:

If you are using this repo for guidance, please hit the star. Thanks A lot !

>  The [Certified Kubernetes Administrator (CKA) certification](https://www.cncf.io/certification/cka/) exam certifies that candidates have the skills, knowledge, and competency to perform the responsibilities of Kubernetes administrators.
 
## CKA Exam details (v1.31  2024 ) 

| **CKA Exam Details**                     | **Information**                                                                                     |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------|
| **Exam Type**                             | Performance Based NOT MCQ )                                    |
| **Exam Duration**                         | 2 hours                                                                                            |
| **Pass Percentage**                       | 66%                                                                                                |
| **CKA Exam Kubernetes Version**          | [Kubernetes v1.31](#cka-exam-syllabus-updated-kubernetes-131-2024)                                                                               |
| **CKA Validity**                         | 2 Years  |
| **Exam Cost**                            | $395 USD ([GET 30% OFF CKA Exam Coupon](https://github.com/teckbootcamps/linux-foundation-coupon?tab=readme-ov-file#-30-off-kubernetes-certification-coupon-ckad--cka--cks)) 💥INCREASE PRICE:  $434 in January 2025         |


## [30% OFF]  CKA Exam Coupon

Save 30% using Coupon code **TECK30** on all the Linux Foundation training and certification programs. This is a limited-time offer for this month. This offer is applicable for CKA, CKAD, CKS, KCNA, LFCS, PCA FINOPS, NodeJS, CHFA, and all the other certification, training, and BootCamp programs.

-  Kubernetes CKA VOUCHER ($395 —> $276): [teckbootcamps-30%off/cka](https://teckbootcamps.com/go/cka-exam-2024/)

> Announcement: The CKA exam syllabus will be updated on January 15th, 2025. Read our CKA exam update [SEE BLOG POST](https://teckbootcamps.com/cka-exam-update-new-features-and-removed-content-explained/) to learn more.


## CKA Exam Syllabus (Updated Kubernetes 1.31  )

| **Topic**                                 | **Concepts**                                                                                                                                                       | **Weightage** |
|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| [**1. Cluster Architecture, Installation & Configuration - 25%**](#1-cluster-architecture-installation--configuration-25) | 1. Manage role-based access control (RBAC)<br>2. Use Kubeadm to install a basic cluster<br>3. Manage a highly-available Kubernetes cluster<br>4. Provision underlying infrastructure to deploy a Kubernetes cluster<br>5. Perform a version upgrade on a Kubernetes cluster using Kubeadm<br>6. Implement etcd backup and restore | 25%          |
| [**2. Workloads & Scheduling - 15%**](#2-workloads--scheduling-15) | 1. Understand deployments and how to perform rolling updates and rollbacks<br>2. Use ConfigMaps and Secrets to configure applications<br>3. Know how to scale applications<br>4. Understand the primitives used to create robust, self-healing application deployments<br>5. Understand how resource limits can affect Pod scheduling<br>6. Awareness of manifest management and common templating tools | 15%          |
| [**3. Services & Networking - 20%**](#3-services--networking-20)                | 1. Understand host networking configuration on the cluster nodes<br>2. Understand connectivity between Pods<br>3. Understand ClusterIP, NodePort, LoadBalancer service types and endpoints<br>4. Know how to use Ingress controllers and Ingress resources<br>5. Know how to configure and use CoreDNS<br>6. Choose an appropriate container network interface plugin | 20%          |
| [**4. Storage - 10%**](#4-storage-10-)               | 1. Understand storage classes and persistent volumes<br>2. Understand volume modes, access modes, and reclaim policies for volumes<br>3. Understand persistent volume claims primitive<br>4. Know how to configure applications with persistent storage | 10%          |
| [**5. Troubleshooting - 30%**](#5-troubleshooting-30-) | 1. Evaluate cluster and node logging<br>2. Understand how to monitor applications<br>3. Manage container stdout & stderr logs<br>4. Troubleshoot application failure<br>5. Troubleshoot cluster component failure<br>6. Troubleshoot networking | 30%          |


# 1. Cluster Architecture, Installation & Configuration (25%)

This section focuses on the core concepts of Kubernetes cluster architecture, installation, and configuration, which make up 25% of the CKA Exam. Below is a simplified breakdown of the topics covered:

### Manage Role-Based Access Control (RBAC)
RBAC allows you to control access to your Kubernetes cluster. You can define roles and assign them to users or applications to limit what they can do within the cluster.- [Learn more about RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

### Use Kubeadm to Install a Basic Cluster
Kubeadm is a tool that helps you set up a Kubernetes cluster quickly and easily. It handles the necessary configurations to initialize a cluster and add worker nodes.
- [Learn more about Kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/)

### Manage a Highly-Available Kubernetes Cluster
High availability ensures your Kubernetes cluster remains operational even if some components fail. This involves setting up multiple control plane nodes and using a load balancer.
- [Learn more about high availability](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/)

### Provision Underlying Infrastructure to Deploy a Kubernetes Cluster
Before deploying a cluster, you need to set up the underlying infrastructure, such as servers, networking, and storage, either on-premises or in the cloud.
- [Learn more about cluster infrastructure](https://kubernetes.io/docs/setup/)

### Perform a Version Upgrade on a Kubernetes Cluster Using Kubeadm
Keeping your Kubernetes cluster updated is important for security and new features. Kubeadm provides a streamlined process for upgrading cluster versions.
- [Learn more about upgrading](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

### Implement Etcd Backup and Restore
Etcd is the key-value store used by Kubernetes to store cluster data. Regular backups ensure you can recover your cluster in case of a failure.
- [Learn more about etcd backup and restore](https://etcd.io/docs/latest/op-guide/backup/)


# 2. Workloads & Scheduling (15%)

This section focuses on managing workloads and scheduling in Kubernetes, making up 15% of the CKA Exam. Below are the key topics explained with `kubectl` examples:

### Understand Deployments and How to Perform Rolling Updates and Rollbacks
Deployments manage the lifecycle of applications. Rolling updates allow you to update applications without downtime, while rollbacks revert to a previous version if needed.

#### Example:
**Create a deployment:**
```bash
kubectl create deployment nginx --image=nginx:1.21
```

**Perform a rolling update:**
```bash
kubectl set image deployment/nginx nginx=nginx:1.22
```

**Rollback to a previous version:**
```bash
kubectl rollout undo deployment/nginx
```

- [Learn more about deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

### Use ConfigMaps and Secrets to Configure Applications
ConfigMaps and Secrets store configuration data and sensitive information, allowing you to decouple configuration from application code.

#### Example:
**Create a ConfigMap:**
```bash
kubectl create configmap app-config --from-literal=key1=value1
```

**Create a Secret:**
```bash
kubectl create secret generic app-secret --from-literal=password=mysecret
```

**Use them in a Pod:**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: app-pod
spec:
  containers:
  - name: app-container
    image: myapp:latest
    env:
    - name: CONFIG_KEY
      valueFrom:
        configMapKeyRef:
          name: app-config
          key: key1
    - name: PASSWORD
      valueFrom:
        secretKeyRef:
          name: app-secret
          key: password
```
```bash
kubectl apply -f pod.yaml
```

- [Learn more about ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)
- [Learn more about Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)

### Know How to Scale Applications
Scaling ensures your application can handle varying levels of traffic by adjusting the number of replicas.

#### Example:
**Scale a deployment:**
```bash
kubectl scale deployment nginx --replicas=5
```

**Autoscale based on CPU usage:**
```bash
kubectl autoscale deployment nginx --min=2 --max=10 --cpu-percent=50
```

- [Learn more about scaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)

### Understand the Primitives Used to Create Robust, Self-Healing, Application Deployments
Kubernetes primitives like Deployments, ReplicaSets, and Probes ensure applications are highly available and self-healing.

#### Example:
**Add readiness and liveness probes:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: myapp:latest
        readinessProbe:
          httpGet:
            path: /healthz
            port: 8080
        livenessProbe:
          httpGet:
            path: /healthz
            port: 8080
```
```bash
kubectl apply -f deployment.yaml
```

- [Learn more about probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

### Understand How Resource Limits Can Affect Pod Scheduling
Resource requests and limits ensure fair allocation of cluster resources and influence pod scheduling.

#### Example:
**Set resource requests and limits:**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: resource-demo
spec:
  containers:
  - name: demo-container
    image: nginx
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```
```bash
kubectl apply -f resource-demo.yaml
```

- [Learn more about resource management](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

### Awareness of Manifest Management and Common Templating Tools
Manifest management tools like Helm and Kustomize simplify deploying and managing Kubernetes applications.

#### Example:
**Using Kustomize:**
```bash
kubectl apply -k ./my-kustomization/
```

**Using Helm:**
```bash
helm install my-app ./my-chart
```

- [Learn more about Kustomize](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/)
- [Learn more about Helm](https://helm.sh/docs/)

---

### Resources to Prepare
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- [Kubernetes Workloads](https://kubernetes.io/docs/concepts/workloads/)


## 3. Services & Networking (20%)

This section focuses on Kubernetes services and networking concepts, which make up 20% of the CKA Exam. Below are the key topics explained with `kubectl` examples:

### 1. Understand Host Networking Configuration on the Cluster Nodes
Host networking involves understanding how network interfaces, IPs, and routes are configured on cluster nodes to ensure communication.

#### Key Concepts:
- Check node network interfaces and routes using tools like `ip` or `ifconfig`.
- Ensure proper setup of firewalls and ports for Kubernetes components.

**Example:**
```bash
# List network interfaces on a node
kubectl get nodes -o wide
ssh <node-name> "ip a"
```

- [Learn more about cluster networking](https://kubernetes.io/docs/concepts/architecture/nodes/)

### 2. Understand Connectivity Between Pods
Pods communicate with each other via the cluster network. All Pods are assigned a unique IP and can communicate without NAT.

#### Example:
**Test Pod-to-Pod connectivity:**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod1
spec:
  containers:
  - name: nginx
    image: nginx
---
apiVersion: v1
kind: Pod
metadata:
  name: pod2
spec:
  containers:
  - name: busybox
    image: busybox
    command: ["sh", "-c", "sleep 3600"]
```
```bash
kubectl apply -f pods.yaml
kubectl exec pod2 -- ping pod1
```

- [Learn more about Pod networking](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

### 3. Understand ClusterIP, NodePort, LoadBalancer Service Types and Endpoints
Services expose Kubernetes applications for internal and external access. Common service types include:

- **ClusterIP:** Default; exposes the service inside the cluster.
- **NodePort:** Exposes the service on a static port on each node.
- **LoadBalancer:** Uses cloud provider load balancers to expose services externally.

#### Example:
**Create a ClusterIP service:**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: clusterip-service
spec:
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
  type: ClusterIP
```
```bash
kubectl apply -f service.yaml
```

- [Learn more about services](https://kubernetes.io/docs/concepts/services-networking/service/)

### 4. Know How to Use Ingress Controllers and Ingress Resources
Ingress provides HTTP and HTTPS routing to applications inside the cluster using hostnames and paths.

#### Example:
**Deploy an Ingress resource:**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: clusterip-service
            port:
              number: 80
```
```bash
kubectl apply -f ingress.yaml
```

- [Learn more about Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)

### 5. Know How to Configure and Use CoreDNS
CoreDNS is a DNS server that provides name resolution within the Kubernetes cluster.

#### Example:
**Check CoreDNS ConfigMap:**
```bash
kubectl -n kube-system get configmap coredns -o yaml
```
**Test DNS resolution:**
```bash
kubectl exec -it <pod-name> -- nslookup kubernetes.default
```

- [Learn more about CoreDNS](https://kubernetes.io/docs/tasks/administer-cluster/coredns/)

### 6. Choose an Appropriate Container Network Interface (CNI) Plugin
CNIs enable networking in Kubernetes by providing Pod-to-Pod connectivity.

#### Popular CNI Plugins:
- **Flannel:** Simple and easy-to-configure.
- **Calico:** Offers advanced networking and network policy capabilities.
- **Weave Net:** Supports encrypted communication.

#### Example:
**Install Calico as a CNI:**
```bash
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

- [Learn more about CNIs](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

---

### Resources to Prepare
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- [Kubernetes Services](https://kubernetes.io/docs/concepts/services-networking/service/)


## 4. Storage (10%)

This section focuses on Kubernetes storage concepts, which make up 10% of the CKA Exam. Below are the key topics explained with `kubectl` examples:

### 1. Understand Storage Classes and Persistent Volumes
Storage Classes define the types of storage available, while Persistent Volumes (PVs) represent storage in the cluster.

#### Example:
**Create a Storage Class:**
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-storage
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
```
```bash
kubectl apply -f storageclass.yaml
```

**Create a Persistent Volume:**
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-demo
spec:
  capacity:
    storage: 1Gi
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: fast-storage
  hostPath:
    path: /mnt/data
```
```bash
kubectl apply -f pv.yaml
```

- [Learn more about Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/)
- [Learn more about Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

### 2. Understand Volume Mode, Access Modes, and Reclaim Policies for Volumes
Volumes can have different modes and access settings to fit application needs. Reclaim policies determine what happens to a volume after it is released.

#### Key Modes and Policies:
- **Volume Modes:** Filesystem, Block.
- **Access Modes:** ReadWriteOnce, ReadOnlyMany, ReadWriteMany.
- **Reclaim Policies:** Retain, Delete, Recycle.

**Example:**
Check PV details:
```bash
kubectl describe pv pv-demo
```

- [Learn more about Volume Modes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#volume-modes)
- [Learn more about Access Modes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes)

### 3. Understand Persistent Volume Claims (PVC) Primitive
PVCs allow Pods to request specific storage resources from PVs.

#### Example:
**Create a Persistent Volume Claim:**
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-demo
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
  storageClassName: fast-storage
```
```bash
kubectl apply -f pvc.yaml
```

**Use a PVC in a Pod:**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-with-pvc
spec:
  containers:
  - name: app-container
    image: nginx
    volumeMounts:
    - mountPath: "/data"
      name: storage
  volumes:
  - name: storage
    persistentVolumeClaim:
      claimName: pvc-demo
```
```bash
kubectl apply -f pod.yaml
```

- [Learn more about PVCs](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)

### 4. Know How to Configure Applications with Persistent Storage
Applications often need persistent storage to retain data. Configure storage by mounting volumes to application Pods.

#### Example:
**Deployment with Persistent Storage:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-with-storage
spec:
  replicas: 2
  selector:
    matchLabels:
      app: storage-app
  template:
    metadata:
      labels:
        app: storage-app
    spec:
      containers:
      - name: app-container
        image: nginx
        volumeMounts:
        - name: app-storage
          mountPath: /usr/share/nginx/html
      volumes:
      - name: app-storage
        persistentVolumeClaim:
          claimName: pvc-demo
```
```bash
kubectl apply -f deployment.yaml
```

- [Learn more about configuring applications with storage](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/)

---

### Resources to Prepare
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Persistent Volumes Guide](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
- [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)


## 5. Troubleshooting (30%)

This section focuses on troubleshooting skills, which constitute 30% of the CKA Exam. Below are the key topics explained with `kubectl` examples:

### 1. Evaluate Cluster and Node Logging
Logs from the cluster and nodes help identify issues with Kubernetes components and nodes.

#### Example:
**View cluster events:**
```bash
kubectl get events --sort-by='.metadata.creationTimestamp'
```

**Check kubelet logs on a node:**
```bash
ssh <node-name>
sudo journalctl -u kubelet
```

- [Learn more about Kubernetes logging](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

### 2. Understand How to Monitor Applications
Application monitoring involves tracking application performance and resource usage using tools like `kubectl top` or external monitoring solutions.

#### Example:
**Check resource usage of Pods:**
```bash
kubectl top pod
```

**Check resource usage of nodes:**
```bash
kubectl top node
```

- [Learn more about monitoring](https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-usage-monitoring/)

### 3. Manage Container stdout & stderr Logs
Logs from containerized applications help diagnose issues in application behavior.

#### Example:
**View logs from a Pod:**
```bash
kubectl logs <pod-name>
```

**View logs from a specific container in a Pod:**
```bash
kubectl logs <pod-name> -c <container-name>
```

- [Learn more about container logs](https://kubernetes.io/docs/concepts/cluster-administration/logging/#logging-at-the-node-level)

### 4. Troubleshoot Application Failure
Application failures often arise from misconfigurations, missing dependencies, or resource constraints.

#### Example:
**Describe a failing Pod to identify issues:**
```bash
kubectl describe pod <pod-name>
```

**Debug a failing Pod:**
```bash
kubectl exec -it <pod-name> -- /bin/sh
```

- [Learn more about troubleshooting applications](https://kubernetes.io/docs/tasks/debug/debug-application/)

### 5. Troubleshoot Cluster Component Failure
Cluster component failures can disrupt the entire cluster. Key components include the API server, scheduler, controller manager, and etcd.

#### Example:
**Check the status of cluster components:**
```bash
kubectl get componentstatuses
```

**Check the logs of a specific component:**
```bash
kubectl logs -n kube-system <component-pod-name>
```

- [Learn more about troubleshooting cluster components](https://kubernetes.io/docs/tasks/debug/debug-cluster/)

### 6. Troubleshoot Networking
Networking issues can affect Pod communication, service access, or external connectivity.

#### Example:
**Test Pod connectivity:**
```bash
kubectl exec -it <pod-name> -- ping <target-pod-ip>
```

**Debug Service issues:**
```bash
kubectl describe service <service-name>
```

**Test DNS resolution:**
```bash
kubectl exec -it <pod-name> -- nslookup <service-name>
```

- [Learn more about troubleshooting networking](https://kubernetes.io/docs/tasks/debug/debug-cluster/dns-debugging-resolution/)

---

### Resources to Prepare
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Troubleshooting Guide](https://kubernetes.io/docs/tasks/debug/)
- [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)



# CKA Exam Questions And Answers

Practice a lot with Kubernetes:
- [CKA Exam Questions And Answers](f.cka-exam-questions-and-answers.md)
 

## Additional Resources
* 💬 [Kubernetes Slack Channel #certifications](https://kubernetes.slack.com/)<sup>Slack</sup>
* 📚 [Guide to Certified Kubernetes Administrator (CKA)](https://teckbootcamps.com/cka-exam-study-guide/)<sup>Blog</sup>
* 🎞️ [Udemy: CKA Certified Kubernetes AdministratorCrash Course](https://www.udemy.com/course/certified-kubernetes-administrator-with-practice-tests)<sup>Video Course</sup>
* 🎞️ [Certified Kubernetes Administrator (CKA) - A Cloud Guru (formerly Linux Academy)](https://acloudguru.com/course/cloud-native-certified-kubernetes-administrator-cka/)<sup>Video Course</sup>
* 🎞️ [Kubernetes Fundamentals (LFS258) - Linux Foundation](https://training.linuxfoundation.org/training/kubernetes-fundamentals/)<sup>Official Course</sup>
* 🎞️ [Kubernetes Deep Dive - A Cloud Guru](https://acloud.guru/learn/kubernetes-deep-dive)<sup>Video Course</sup>

## Practice
Practice a lot with Kubernetes:

- [CKA Simulator - killer.sh](https://killer.sh/cka)
- [Kubernetes the Hard Way by Kelsey Hightower](https://github.com/kelseyhightower/kubernetes-the-hard-way)
- [CKA Scenarios - killercoda.com](https://killercoda.com/killer-shell-cka)
- [Learning Playground - by Docker](https://labs.play-with-k8s.com/)


# 💬 Share To Your Network
If this repo has helped you in any way, feel free to share !

