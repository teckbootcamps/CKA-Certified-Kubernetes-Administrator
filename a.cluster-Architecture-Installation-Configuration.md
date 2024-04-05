# Cluster Architecture, Installation & Configuration (20%)

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


- Manage a highly-available Kubernetes cluster.

    - [Kubernetes Documentation > Getting started > Production environment > Installing Kubernetes with deployment tools > Bootstrapping clusters with kubeadm > Creating Highly Available clusters with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/)<sup>Doc</sup>

- Provision underlying infrastructure to deploy a Kubernetes cluster.

    - [Kubernetes Documentation > Getting started](https://kubernetes.io/docs/setup/)<sup>Doc</sup>

- Perform a version upgrade on a Kubernetes cluster using Kubeadm.

    - [Kubernetes Documentation > Tasks > Administer a Cluster > Administration with kubeadm > Upgrading kubeadm clusters](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)<sup>Doc</sup>

    - [How To Setup Kubernetes Cluster Using Kubeadm](https://teckbootcamps.com/how-to-setup-kubernetes-cluster-using-kubeadm/)<sup><blog</sup>
    
- Implement etcd backup and restore.


    - [Exploring Kubernetes : Basic Usage of ETCD](https://teckbootcamps.com/exploring-kubernetes-basic-usage-of-etcd/)<sup>Blog</sup>

    - [Kubernetes Documentation > Tasks > Administer a Cluster > Operating etcd clusters for Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)<sup>Doc</sup>


Helpful commands:

```bash
# Display addresses of the master and services
kubectl cluster-info

# Dump current cluster state to stdout
kubectl cluster-info dump

# List the nodes
kubectl get nodes

# Show metrics for a given node
kubectl top node my-node

# List all pods in all namespaces, with more details
kubectl get pods -o wide --all-namespaces

# List all services in all namespaces, with more details
kubectl get svc  -o wide --all-namespaces
```
