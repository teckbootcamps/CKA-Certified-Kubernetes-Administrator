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
| **Exam Cost**                            | $395 USD ([GET 30% OFF CKA Exam Coupon](#30-off-cka-exam-coupon)) 💥INCREASE PRICE:  $434 in January 2025         |


## [30% OFF]  CKA Exam Coupon

Save 30% using Coupon code **TECK30** on all the Linux Foundation training and certification programs. This is a limited-time offer for this month. This offer is applicable for CKA, CKAD, CKS, KCNA, LFCS, PCA FINOPS, NodeJS, CHFA, and all the other certification, training, and BootCamp programs.

-  Kubernetes CKA VOUCHER ($395 —> $276): [teckbootcamps/cka](https://teckbootcamps.com/go/cka-exam-2024/)

> Announcement: The CKA exam syllabus will be updated on January 15th, 2025. Read our CKA exam update [blog] (https://teckbootcamps.com/cka-exam-update-new-features-and-removed-content-explained/) to learn more.


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



# 3. Services & Networking (20%)

- [x] Understand host networking configuration on the cluster nodes
- [x] Understand connectivity between Pods
- [x] Understand ClusterIP, NodePort, LoadBalancer service types and endpoints
- [x] Know how to use Ingress controllers and Ingress resources
- [x] Know how to configure and use CoreDNS
- [x] Choose an appropriate container network interface plugin


- Understand host networking configuration on the cluster nodes.

    - [Kubernetes Documentation > Concepts > Cluster Administration > Cluster Networking](https://kubernetes.io/docs/concepts/cluster-administration/networking/)<sup>Doc</sup>

- Understand connectivity between Pods.

    - [Kubernetes Documentation > Concepts > Workloads > Pods > Networking](https://kubernetes.io/docs/concepts/workloads/pods/#pod-networking)<sup>Doc</sup>

    - [GitHub > Kubernetes Community Documentation > Design Proposals > Networking](https://raw.githubusercontent.com/kubernetes/design-proposals-archive/main/network/networking.md)<sup>Doc</sup>

- Understand ClusterIP, NodePort, LoadBalancer service types and endpoints.

    - [Working with Kubernetes Services](https://teckbootcamps.com/working-with-kubernetes-services/))<sup>Blog</sup>

    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Service](https://kubernetes.io/docs/concepts/services-networking/service/)<sup>Doc</sup>


- Know how to use Ingress controllers and Ingress resources.

    - [Introducing  Gateway API , Ingress gateway and Service Mesh in Kubernetes](https://teckbootcamps.com/introducing-gateway-api-ingress-gateway-and-service-mesh-in-kubernetes/))<sup>Blog</sup>

    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)<sup>Doc</sup>
    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Ingress Controllers](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/)<sup>Doc</sup>

- Know how to configure and use CoreDNS.

    - [Kubernetes Documentation > Tasks > Administer a Cluster > Using CoreDNS for Service Discovery](https://kubernetes.io/docs/tasks/administer-cluster/coredns/)<sup>Doc</sup>

- Choose an appropriate container network interface plugin.

    - [Kubernetes Documentation > Concepts > Extending Kubernetes > Compute, Storage, and Networking Extensions > Network Plugins](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)<sup>Doc</sup>


# 4. Storage (10 %)

- [x] Understand storage classes, persistent volumes
- [x] Understand volume mode, access modes and reclaim policies for volumes
- [x] Understand persistent volume claims primitive
- [x] Know how to configure applications with persistent storage


- Understand storage classes, persistent volumes.

    - [Understanding Kubernetes Volumes and Configuration Data](https://teckbootcamps.com/understanding-kubernetes-volumes-and-configuration-data/)<sup>Blog</sup>
    - [Kubernetes Documentation > Concepts > Storage > Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/)<sup>Doc</sup>
    - [Kubernetes Documentation > Concepts > Storage > Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)<sup>Doc</sup>

- Understand volume mode, access modes and reclaim policies for volumes.

    - [Kubernetes Documentation > Concepts > Storage > Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volumes)<sup>Doc</sup>

- Understand persistent volume claims primitive.
    - [Understanding Kubernetes Volumes and Configuration Data](https://teckbootcamps.com/understanding-kubernetes-volumes-and-configuration-data/)<sup>Blog</sup>
    - [Kubernetes Documentation > Concepts > Storage > Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)<sup>Doc</sup>

- Know how to configure applications with persistent storage.

    - [Kubernetes Documentation > Tasks > Configure Pods and Containers > Configure a Pod to Use a PersistentVolume for Storage](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#create-a-persistentvolume)<sup>Doc</sup>


# 5. Troubleshooting (30 %)

- [x] Evaluate cluster and node logging
- [x] Understand how to monitor applications
- [x] Manage container stdout & stderr logs
- [x] Troubleshoot application failure
- [x] Troubleshoot cluster component failure
- [x] Troubleshoot networking


- Evaluate cluster and node logging.

    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Troubleshoot Clusters](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/)<sup>Doc</sup>

- Understand how to monitor applications.
    - [Kubernetes Monitoring and Logging By Examples](https://teckbootcamps.com/kubernetes-monitoring-and-logging-by-examples/)<sup>Blog</sup>
    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Tools for Monitoring Resources](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/)<sup>Doc</sup>

- Manage container stdout & stderr logs.

    - [Kubernetes Documentation > Concepts > Cluster Administration > Logging Architecture](https://kubernetes.io/docs/concepts/cluster-administration/logging/)<sup>Doc</sup>

- Troubleshoot application failure.

    - [Troubleshooting the Process of a Kubernetes Pod being killed](https://teckbootcamps.com/troubleshooting-the-process-of-a-kubernetes-pod-being-killed/)<sup>Blog</sup>
    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Troubleshoot Applications](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-application/)<sup>Doc</sup>
    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Application Introspection and Debugging](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-application-introspection/)<sup>Doc</sup>

- Troubleshoot cluster component failure.

    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Troubleshoot Clusters](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/)<sup>Doc</sup>

- Troubleshoot networking.

    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Debug Services](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-service/)<sup>Doc</sup>

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

