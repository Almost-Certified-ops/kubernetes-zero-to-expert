# Episode 01 — Kubernetes From Zero: Your First Cluster

In this episode, we build our first local Kubernetes cluster using Minikube and deploy a simple nginx application.

This lab is designed for absolute beginners. The goal is to understand the first Kubernetes mental model: **you describe the desired state, and Kubernetes works to make the cluster match that state**.

---

## What You Will Learn

By the end of this episode, you will understand:

- What Kubernetes is
- Why Kubernetes exists
- What a cluster is
- What a node is
- What a Pod is
- What a Deployment is
- What a Service is
- How to start a local Kubernetes cluster
- How to deploy nginx
- How to scale an application
- How to expose an application with a Service
- How to use a declarative YAML manifest
- How to clean up Kubernetes resources

---

## Lab Architecture

This lab creates one Kubernetes Deployment and one Kubernetes Service.

```text
Local Machine
└── Minikube Cluster
    └── Worker Node
        ├── Deployment: hello-k8s-yaml
        │   └── 3 nginx Pods
        └── Service: hello-k8s-yaml
            └── NodePort access to nginx
```

---

## Requirements

Before starting this lab, install:

- Docker Desktop, Podman, VirtualBox, Hyper-V, KVM, or another supported Minikube driver
- Minikube
- kubectl
- Git
- VS Code or another code editor
- Basic terminal access

You do **not** need a cloud account for this episode.

Not required yet:

- GCP
- Azure
- AWS
- Terraform
- Helm
- Bare-metal servers

---

## Folder Structure

This episode should use the following structure:

```text
01-first-cluster/
├── README.md
├── commands.md
└── manifests/
    └── nginx.yaml
```

---

## Kubernetes Manifest

Create this file:

```text
manifests/nginx.yaml
```

Paste the following manifest:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-k8s-yaml
spec:
  replicas: 3
  selector:
    matchLabels:
      app: hello-k8s-yaml
  template:
    metadata:
      labels:
        app: hello-k8s-yaml
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80

---
apiVersion: v1
kind: Service
metadata:
  name: hello-k8s-yaml
spec:
  type: NodePort
  selector:
    app: hello-k8s-yaml
  ports:
    - port: 80
      targetPort: 80
```

Important: the `---` separator is required because this file contains two Kubernetes resources: a Deployment and a Service.

---

## Start the Cluster

Start Minikube:

```bash
minikube start
```

Check the cluster node:

```bash
kubectl get nodes
```

Check cluster information:

```bash
kubectl cluster-info
```

Check all Kubernetes system Pods:

```bash
kubectl get pods -A
```

---

## Deploy the Application

From the `01-first-cluster` folder, apply the manifest:

```bash
kubectl apply -f manifests/nginx.yaml
```

Expected output:

```text
deployment.apps/hello-k8s-yaml created
service/hello-k8s-yaml created
```

---

## Verify the Deployment

Check the Deployment, ReplicaSet, Pods, and Services:

```bash
kubectl get deploy,rs,pods,svc
```

You should see:

```text
deployment.apps/hello-k8s-yaml
replicaset.apps/hello-k8s-yaml-xxxxx
pod/hello-k8s-yaml-xxxxx
service/hello-k8s-yaml
```

Because the Deployment uses `replicas: 3`, you should see three nginx Pods.

---

## Open the Application

Use Minikube to open the NodePort Service:

```bash
minikube service hello-k8s-yaml
```

This should open nginx in your browser.

---

## Important Concept: Deployment vs Service

A Deployment creates and manages Pods.

A Service does not create Pods.

A Service provides stable networking to Pods that already exist and match the Service selector.

In this lab, the Service selector is:

```yaml
selector:
  app: hello-k8s-yaml
```

The Pod label is:

```yaml
labels:
  app: hello-k8s-yaml
```

Because these match, the Service can route traffic to the Pods.

If the selector and labels do not match, the Service will have no endpoints.

Check endpoints with:

```bash
kubectl get endpoints hello-k8s-yaml
```

---

## Common Beginner Mistake

If you put the Deployment and Service in the same YAML file, you must separate them with:

```yaml
---
```

Without the separator, Kubernetes may not process the resources the way you expect.

Correct pattern:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-k8s-yaml
spec:
  replicas: 3

---
apiVersion: v1
kind: Service
metadata:
  name: hello-k8s-yaml
spec:
  type: NodePort
```

---

## Troubleshooting Commands

Check all core resources:

```bash
kubectl get deploy,rs,pods,svc
```

Describe the Deployment:

```bash
kubectl describe deployment hello-k8s-yaml
```

Describe a Pod:

```bash
kubectl describe pod POD_NAME
```

Check Pod logs:

```bash
kubectl logs POD_NAME
```

Check Service details:

```bash
kubectl describe service hello-k8s-yaml
```

Check Service endpoints:

```bash
kubectl get endpoints hello-k8s-yaml
```

Check all namespaces:

```bash
kubectl get pods -A
```

Check Minikube status:

```bash
minikube status
```

---

## Clean Up

Delete the resources created by this lab:

```bash
kubectl delete -f manifests/nginx.yaml
```

Stop Minikube if you are done working:

```bash
minikube stop
```

Delete the local cluster completely if needed:

```bash
minikube delete
```

---

## Commands Used in This Episode

```bash
minikube start
kubectl get nodes
kubectl cluster-info
kubectl get pods -A
kubectl apply -f manifests/nginx.yaml
kubectl get deploy,rs,pods,svc
kubectl get endpoints hello-k8s-yaml
minikube service hello-k8s-yaml
kubectl delete -f manifests/nginx.yaml
minikube stop
```

---

## What You Learned

In this episode, you learned that:

- Kubernetes manages desired state.
- A Pod runs your application container.
- A Deployment manages Pods and keeps the desired number of replicas running.
- A Service gives stable networking to matching Pods.
- Labels and selectors connect Services to Pods.
- One YAML file can define multiple Kubernetes resources when separated with `---`.

---

## Next Episode

Episode 02 will focus on Pods.

We will cover:

- What a Pod really is
- Why Kubernetes does not just run containers directly
- Pod lifecycle
- Pod logs
- Executing commands inside a Pod
- CrashLoopBackOff
- Basic Pod debugging
