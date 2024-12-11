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
| [**1. Cluster Architecture, Installation & Configuration - 25%**](#1-cluster-architecture-installation--configuration-20) | 1. Manage role-based access control (RBAC)<br>2. Use Kubeadm to install a basic cluster<br>3. Manage a highly-available Kubernetes cluster<br>4. Provision underlying infrastructure to deploy a Kubernetes cluster<br>5. Perform a version upgrade on a Kubernetes cluster using Kubeadm<br>6. Implement etcd backup and restore | 25%          |
| [**2. Workloads & Scheduling - 15%**](#2-workloads--scheduling-15) | 1. Understand deployments and how to perform rolling updates and rollbacks<br>2. Use ConfigMaps and Secrets to configure applications<br>3. Know how to scale applications<br>4. Understand the primitives used to create robust, self-healing application deployments<br>5. Understand how resource limits can affect Pod scheduling<br>6. Awareness of manifest management and common templating tools | 15%          |
| [**3. Services & Networking - 20%**](#3-services--networking-20)                | 1. Understand host networking configuration on the cluster nodes<br>2. Understand connectivity between Pods<br>3. Understand ClusterIP, NodePort, LoadBalancer service types and endpoints<br>4. Know how to use Ingress controllers and Ingress resources<br>5. Know how to configure and use CoreDNS<br>6. Choose an appropriate container network interface plugin | 20%          |
| [**4. Storage - 10%**](#4-storage-10-)               | 1. Understand storage classes and persistent volumes<br>2. Understand volume modes, access modes, and reclaim policies for volumes<br>3. Understand persistent volume claims primitive<br>4. Know how to configure applications with persistent storage | 10%          |
| [**5. Troubleshooting - 30%**](#5-troubleshooting-30-) | 1. Evaluate cluster and node logging<br>2. Understand how to monitor applications<br>3. Manage container stdout & stderr logs<br>4. Troubleshoot application failure<br>5. Troubleshoot cluster component failure<br>6. Troubleshoot networking | 30%          |


# 1. Cluster Architecture, Installation & Configuration (20%)

- [x] Manage role based access control (RBAC)
- [x] Use Kubeadm to install a basic cluster
- [x] Manage a highly-available Kubernetes cluster
- [x] Provision underlying infrastructure to deploy a Kubernetes cluster
- [x] Perform a version upgrade on a Kubernetes cluster using Kubeadm
- [x] Implement etcd backup and restore

## Set the context and the namespace.
A "Context" is a combination of a cluster, user, and namespace. It is a way to specify the cluster you want to interact with, the user or authentication credentials you want to use, and the default namespace for that user. Setting a context is important because it helps you manage multiple Kubernetes clusters and switch between them easily.

**Use Cases:**  Multi-cluster Management, User and Authentication, isolate and organize resources, simplifies command-line operations.

**Hint:** Don't change the namespace, change the context as per the question. If there is a namespace add -n `namespace` to lessen the risk of error. Set context before each question using the kubectl config command, and switch between contexts using kubectl config use-context. 


- Manage role based access control (RBAC).

    - [Understanding Kubernetes RBAC](https://teckbootcamps.com/understanding-kubernetes-rbac/)<sup>Blog</sup>

    - [Kubernetes Documentation > Reference > Accessing the API > Using RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)<sup>Doc</sup>


- Use Kubeadm to install a basic cluster.

    - [How To Setup Kubernetes Cluster Using Kubeadm](https://teckbootcamps.com/how-to-setup-kubernetes-cluster-using-kubeadm/)<sup><blog</sup>

    - [Kubernetes Documentation > Getting started > Production environment > Installing Kubernetes with deployment tools > Bootstrapping clusters with kubeadm > Creating a cluster with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)<sup>Doc</sup>


# 2. Workloads & Scheduling (15%)

- [x]  Understand deployments and how to perform rolling update and rollbacks
- [x]  Use ConfigMaps and Secrets to configure applications
- [x]  Know how to scale applications
- [x]  Understand the primitives used to create robust, self-healing, application deployments
- [x]  Understand how resource limits can affect Pod scheduling
- [x]  Awareness of manifest management and common templating tools


- Understand deployments and how to perform rolling update and rollbacks.

    - [Practical Examples for 3 Advanced Kubernetes deployment strategies](https://teckbootcamps.com/practical-examples-for-3-advanced-kubernetes-deployment-strategies/))<sup>Doc</sup>

    - [Kubernetes Documentation > Concepts > Workloads > Controllers > Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)<sup>Doc</sup>

    - Example Deployment File (dep-nginx.yaml) using NGINX

        ```yaml
        apiVersion: apps/v1
        kind: Deployment
        metadata:
            name: nginx-deployment
            labels:
                app: nginx
        spec:
          replicas: 3
          selector:
            matchLabels:
              app: nginx
          template:
            metadata:
              labels:
                app: nginx
            spec:
              containers:
              - name: nginx
                image: nginx:1.21.6
                ports:
                - containerPort: 80
        ```

        ```bash
        # Create Deployment
        kubectl create -f dep-nginx.yaml

        # Get Deployments
        kubectl get deployments

        # Update Deployment
        kubectl edit deployment.v1.apps/nginx-deployment

        # See rollout status
        kubectl rollout status deployment.v1.apps/nginx-deployment

        # Describe Deployment
        kubectl describe deployment

        # Rolling back to a previous revision
        kubectl rollout undo deployment.v1.apps/nginx-deployment
        ```

    - [ Use ConfigMaps and Secrets to configure applications.](https://teckbootcamps.com/understanding-kubernetes-volumes-and-configuration-data/)<sup>Blog</sup>

    - [Kubernetes Secrets: A complete guide to securely managing sensitive information](https://teckbootcamps.com/kubernetes-secrets-a-complete-guide-to-securely-managing-sensitive-information/)<sup>Blog</sup>

    - [Kubernetes Documentation > Concepts > Configuration > ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)<sup>Doc</sup>

    - [Kubernetes Documentation > Concepts > Configuration > Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)<sup>Doc</sup>

- Know how to scale applications.

    - [Kubernetes Documentation > Concepts > Cluster Administration > Managing Resources > Scaling Your Application](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/#scaling-your-application)<sup>Doc</sup>.

        ```bash
        # Increase replicas number for nginx-deployment
        kubectl scale deployment/nginx-deployment --replicas=5

        # Using autoscaling
        kubectl autoscale deployment/nginx-deployment --min=2 --max=5
        ```

- Understand the primitives used to create robust, self-healing, application deployments.

    - [Kubernetes Documentation > Concepts > Workloads > Pods > Pod Lifecycle](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)<sup>Doc</sup>
    
    - [Kubernetes Monitoring and Logging By Examples](https://teckbootcamps.com/kubernetes-monitoring-and-logging-by-examples/)<sup>Blog</sup>

    - [Kubernetes Documentation > Tasks > Configure Pods and Containers > Configure Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)<sup>Doc</sup>

- Understand how resource limits can affect Pod scheduling.

    - [Kubernetes Documentation > Concepts > Configuration > Managing Resources for Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)<sup>Doc</sup>

- Awareness of manifest management and common templating tools.

    - [Kubernetes Documentation > Concepts > Cluster Administration > Managing Resources](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/)<sup>Doc</sup>

    - [Kubernetes Documentation > Tasks > Manage Kubernetes Objects](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/)<sup>Doc</sup>


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

