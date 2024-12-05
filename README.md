# ☸️ Certified Kubernetes Administrator (CKA) Study Guide for December 2024


<p align="center">
  <img src="assets/cka.png" alt="CKA EXAM">
</p>


The [Certified Kubernetes Administrator (CKA) certification](https://www.cncf.io/certification/cka/) exam certifies that candidates have the skills, knowledge, and competency to perform the responsibilities of Kubernetes administrators.
 

## CKA Exam details

| **CKA Exam Details**                     | **Information**                                                                                     |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------|
| **Exam Type**                             | Performance Based NOT MCQ )                                    |
| **Exam Duration**                         | 2 hours                                                                                            |
| **Pass Percentage**                       | 66%                                                                                                |
| **CKA Exam Kubernetes Version**          | Kubernetes v1.31                                                                                 |
| **CKA Validity**                         | 2 Years  |
| **Exam Cost**                            | $395 USD (GET 30% OFF using Coupon **TECK30**) 💥INCREASE PRICE:  $434 in January 2025         |


* 📚 [Guide to Certified Kubernetes Administrator (CKA)](https://teckbootcamps.com/cka-exam-study-guide/)<sup>Blog</sup>


## 💰💰 [50% OFF] Kubernetes Certification Coupon CKA 

Save 50% using Coupon code **CYBER24CC** on all the Linux Foundation training and certification programs. This is a limited-time offer for this month. This offer is applicable for CKA, CKAD, CKS, KCNA, LFCS, PCA FINOPS, NodeJS, CHFA, and all the other certification, training, and BootCamp programs.

-  Kubernetes CKA VOUCHER ($395 —> $197): [teckbootcamps/cka](https://teckbootcamps.com/go/cka-exam-2024/)

> Announcement: The CKA exam syllabus will be updated on January 15th, 2025. Read our CKA exam update [blog] (https://teckbootcamps.com/cka-exam-update-new-features-and-removed-content-explained/) to learn more.


## CKA Exam Syllabus (Kubernetes 1.31)

| **Topic**                                 | **Concepts**                                                                                                                                                       | **Weightage** |
|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| [**Cluster Architecture, Installation & Configuration - 25%**](a.cluster-Architecture-Installation-Configuration.md) | 1. Manage role-based access control (RBAC)<br>2. Use Kubeadm to install a basic cluster<br>3. Manage a highly-available Kubernetes cluster<br>4. Provision underlying infrastructure to deploy a Kubernetes cluster<br>5. Perform a version upgrade on a Kubernetes cluster using Kubeadm<br>6. Implement etcd backup and restore | 25%          |
| [**Workloads & Scheduling - 15%**](b.workloads-Scheduling.md) | 1. Understand deployments and how to perform rolling updates and rollbacks<br>2. Use ConfigMaps and Secrets to configure applications<br>3. Know how to scale applications<br>4. Understand the primitives used to create robust, self-healing application deployments<br>5. Understand how resource limits can affect Pod scheduling<br>6. Awareness of manifest management and common templating tools | 15%          |
| [**Services & Networking - 20%**](c.services-Networking.md)                | 1. Understand host networking configuration on the cluster nodes<br>2. Understand connectivity between Pods<br>3. Understand ClusterIP, NodePort, LoadBalancer service types and endpoints<br>4. Know how to use Ingress controllers and Ingress resources<br>5. Know how to configure and use CoreDNS<br>6. Choose an appropriate container network interface plugin | 20%          |
| [**Storage - 10%**](d.storage.md)               | 1. Understand storage classes and persistent volumes<br>2. Understand volume modes, access modes, and reclaim policies for volumes<br>3. Understand persistent volume claims primitive<br>4. Know how to configure applications with persistent storage | 10%          |
| [**Troubleshooting - 30%**](e.troubleshooting.md) | 1. Evaluate cluster and node logging<br>2. Understand how to monitor applications<br>3. Manage container stdout & stderr logs<br>4. Troubleshoot application failure<br>5. Troubleshoot cluster component failure<br>6. Troubleshoot networking | 30%          |



# CKA Exam Questions And Answers

Practice a lot with Kubernetes:

- [CKA Exam Questions And Answers](f.cka-exam-questions-and-answers.md)
 

# Additional Resources
* 💬 [Kubernetes Slack Channel #certifications](https://kubernetes.slack.com/)<sup>Slack</sup>
* 📚 [Guide to Certified Kubernetes Administrator (CKA)](https://teckbootcamps.com/cka-exam-study-guide/)<sup>Blog</sup>
* 🎞️ [Udemy: CKA Certified Kubernetes AdministratorCrash Course](https://www.udemy.com/course/certified-kubernetes-administrator-with-practice-tests)<sup>Video Course</sup>
* 🎞️ [Certified Kubernetes Administrator (CKA) - A Cloud Guru (formerly Linux Academy)](https://acloudguru.com/course/cloud-native-certified-kubernetes-administrator-cka/)<sup>Video Course</sup>
* 🎞️ [Kubernetes Fundamentals (LFS258) - Linux Foundation](https://training.linuxfoundation.org/training/kubernetes-fundamentals/)<sup>Official Course</sup>
* 🎞️ [Kubernetes Deep Dive - A Cloud Guru](https://acloud.guru/learn/kubernetes-deep-dive)<sup>Video Course</sup>

# Practice
Practice a lot with Kubernetes:

- [CKA Simulator - killer.sh](https://killer.sh/cka)
- [Kubernetes the Hard Way by Kelsey Hightower](https://github.com/kelseyhightower/kubernetes-the-hard-way)
- [CKA Scenarios - killercoda.com](https://killercoda.com/killer-shell-cka)
- [Learning Playground - by Docker](https://labs.play-with-k8s.com/)


# kubectl Ninja

Tip: Use [kubectl Cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/) during the exam. You don't need to decorate everything.

## Useful commands or parameters during the exam:

```bash
# Use "kubectl describe" for related events and troubleshooting
kubectl describe pods <podid>

# Use "kubectl explain" to check the structure of a resource object.
kubectl explain deployment --recursive

## Add "-o wide" in order to use wide output, which gives you more details.
kubectl get pods -o wide

## Check always all namespaces by including "--all-namespaces"
kubectl get pods --all-namespaces
```

Generate a manifest template from imperative spec using the output option "-o yaml" and the parameter "--dry-run=client":

```shell
# create a service
kubectl create service clusterip my-service --tcp=8080 --dry-run=client -o yaml

# create a deployment
kubectl create deployment nginx --image=nginx --dry-run=client -o yaml

# create a pod
kubectl run nginx --image=nginx --restart=Never --dry-run=client -o yaml
```

Create resources using kubectl + stdin instead of creating them from manifest files. It helps a lot and saves time. You can use the output of the command above and modify as required:

```shell
cat <<EOF | kubectl create -f -
...
EOF
```

It saves lots of time, believe me.

Kubectl Autocomplete

```shell
source <(kubectl completion bash)
```

## TIPS

* 💬 Be fast
Use the history command to reuse already entered commands or use even faster history search through Ctrl r .

If a command takes some time to execute, like sometimes kubectl delete pod x. You can put a task in the background using Ctrl z and pull it back into foreground running command fg.

You can delete pods fast with:

``` bash
k delete pod x --grace-period 0 --force

k delete pod x $now # if export from above is configured
```

* 💬 Vim

Be great with vim.

toggle vim line numbers

When in vim you can press Esc and type :set number or :set nonumber followed by Enter to toggle line numbers. This can be useful when finding syntax errors based on line - but can be bad when wanting to mark&copy by mouse. You can also just jump to a line number with Esc :22 + Enter.

copy&paste

Get used to copy/paste/cut with vim:

``` shell
Mark lines: Esc+V (then arrow keys)
Copy marked lines: y
Cut marked lines: d
Past lines: p or P
Indent multiple lines
```

To indent multiple lines press Esc and type :set shiftwidth=2. First mark multiple lines using Shift v and the up/down keys. Then to indent the marked lines press > or <. You can then press . to repeat the action.


# 💬 Share To Your Network
If this repo has helped you in any way, feel free to share !

