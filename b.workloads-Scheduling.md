# Workloads & Scheduling (15%)

- [x]  Understand deployments and how to perform rolling update and rollbacks
- [x]  Use ConfigMaps and Secrets to configure applications
- [x]  Know how to scale applications
- [x]  Understand the primitives used to create robust, self-healing, application deployments
- [x]  Understand how resource limits can affect Pod scheduling
- [x]  Awareness of manifest management and common templating tools


- Understand deployments and how to perform rolling update and rollbacks.

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

- Use ConfigMaps and Secrets to configure applications.

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

    - [Kubernetes Documentation > Tasks > Configure Pods and Containers > Configure Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)<sup>Doc</sup>

- Understand how resource limits can affect Pod scheduling.

    - [Kubernetes Documentation > Concepts > Configuration > Managing Resources for Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)<sup>Doc</sup>

- Awareness of manifest management and common templating tools.

    - [Kubernetes Documentation > Concepts > Cluster Administration > Managing Resources](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/)<sup>Doc</sup>

    - [Kubernetes Documentation > Tasks > Manage Kubernetes Objects](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/)<sup>Doc</sup>
