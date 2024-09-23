# ☸️ Certified Kubernetes Administrator (CKA) Study Guide 2024 ( Updated September 2024) 


<p align="center">
  <img src="assets/cka.png" alt="CKA EXAM">
</p>


The [Certified Kubernetes Administrator (CKA) certification](https://www.cncf.io/certification/cka/) exam certifies that candidates have the skills, knowledge, and competency to perform the responsibilities of Kubernetes administrators.
 
Not sure where to start? You may consider reviewing our suggested CKA learning path.

EXAM SIMULATOR! Learners will now have access to an exam simulator, provided by Killer.sh, to experience the exam environment. You will have two exam simulation attempts (36 hours of access for each attempt from the start of activation).
Simulation includes 20-25 questions (which are exactly the same for every attempt and every user (unlike those found on the actual exams) and graded simulation results).


* 📚 [Mohamed BEN HASSINE: Guide to Certified Kubernetes Administrator (CKA)](https://teckbootcamps.com/cka-exam-study-guide/)<sup>Blog</sup>


## 💰💰 [30% OFF] Kubernetes Certification Coupon CKA 

Save 30% using Coupon code **TECK30** on all the Linux Foundation training and certification programs. This is a limited-time offer for this month. This offer is applicable for CKA, CKAD, CKS, KCNA, LFCS, PCA FINOPS, NodeJS, CHFA, and all the other certification, training, and BootCamp programs.

-  Kubernetes CKA VOUCHER ($395 —> $276): [kube.promo/cka](https://teckbootcamps.com/go/cka-exam-2024/)

> Announcement: The CKA exam syllabus will be updated on November 25th, 2024. Read our CKA exam update [blog] (https://teckbootcamps.com/cka-exam-update-new-features-and-removed-content-explained/) to learn more.


# CKA Exam Syllabus (Kubernetes 1.30) 
- [Cluster Architecture, Installation & Configuration - 25%](a.cluster-Architecture-Installation-Configuration.md)
- [Workloads & Scheduling - 15%](b.workloads-Scheduling.md)
- [Services & Networking - 20%](c.services-Networking.md)
- [Storage - 10%](d.storage.md)
- [Troubleshooting - 30%](e.troubleshooting.md)

# Additional Resources
* 💬 [Kubernetes Slack Channel #certifications](https://kubernetes.slack.com/)<sup>Slack</sup>
* 📚 [Mohamed BEN HASSINE: Guide to Certified Kubernetes Administrator (CKA)](https://teckbootcamps.com/cka-exam-study-guide/)<sup>Blog</sup>
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


# CKA Exam Questions And Answers

Practice a lot with Kubernetes:

- [CKA Exam Questions And Answers](f.cka-exam-questions-and-answers.md)
 

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

# 💬 Author
* 👨 🇹🇳 [Aboute ME : Mohamed BEN HASSINE](https://teckbootcamps.com/about-me/)<sup>Blog</sup>
* 👨 [Contact ME in LinkedIn ](https://www.linkedin.com/in/mohamedbnhassine/)<sup>LinkedIn</sup>
* 👨 [Find ME in Medium ](https://medium.com/@teckbootcamps)<sup>Medium</sup>
* ☸ ☸ 3X Certified Kubernetes([CKAD](https://teckbootcamps.com/ckad-exam-study-guide/)<sup>Blog</sup>, [CKA](https://teckbootcamps.com/cka-exam-study-guide//)<sup>Blog</sup> ,[CKS](https://teckbootcamps.com/cks-exam-study-guide/)<sup>Blog</sup>)
* ☁️ ☁️ Google Cloud Solutions Architect ||  [4X certified GCP Cloud](https://www.credential.net/profile/mohamedbenhassine968370/wallet)<sup>Certifications</sup>
* 👨🏼‍💻 👨🏼‍💻 14+ years of experience in the tech