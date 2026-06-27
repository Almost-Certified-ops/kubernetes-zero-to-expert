# Kubernetes Zero to Expert

A lab-focused Kubernetes learning repository for the **Kubernetes Zero to Expert** YouTube series.

This repo is designed to take you from absolute beginner to production-level Kubernetes engineer through real labs, real commands, real infrastructure, and real troubleshooting.

We start simple with local Kubernetes, then move into managed cloud Kubernetes on **GCP**, **Azure**, and comparisons with **AWS**. Later, we introduce **Terraform**, production patterns, GitOps, observability, security, and bare-metal Kubernetes.

---

## Channel Mission

Kubernetes can feel overwhelming at first: clusters, Pods, Deployments, Services, Ingress, RBAC, storage, networking, Helm, Terraform, cloud IAM, and production operations.

This series breaks Kubernetes down step by step.

The goal is not just to memorize commands.

The goal is to understand:

- How Kubernetes works
- Why Kubernetes exists
- How to deploy applications
- How to troubleshoot failures
- How cloud-managed Kubernetes works
- How to build infrastructure with Terraform
- How to operate Kubernetes like a real engineer

---

## Learning Path

We go from easy to hard.

### Phase 1 — Kubernetes Foundations

Local development and core Kubernetes concepts.

Topics include:

- What Kubernetes is
- Minikube
- kubectl
- Pods
- Deployments
- ReplicaSets
- Services
- Labels and selectors
- Namespaces
- ConfigMaps
- Secrets
- Basic troubleshooting

### Phase 2 — Application Deployment

Deploying real applications into Kubernetes.

Topics include:

- Multi-container apps
- Environment variables
- Health checks
- Readiness probes
- Liveness probes
- Rolling updates
- Rollbacks
- Resource requests and limits
- Horizontal Pod Autoscaling

### Phase 3 — Kubernetes Networking

Understanding how traffic moves inside and outside the cluster.

Topics include:

- ClusterIP
- NodePort
- LoadBalancer
- Ingress
- DNS
- CoreDNS
- NetworkPolicies
- Service discovery
- TLS basics

### Phase 4 — Cloud Kubernetes

Managed Kubernetes across major cloud providers.

Primary platforms:

- GKE — Google Kubernetes Engine
- AKS — Azure Kubernetes Service

Comparison platform:

- EKS — Amazon Elastic Kubernetes Service

We compare cloud providers so you understand Kubernetes beyond one vendor.

### Phase 5 — Infrastructure as Code

Infrastructure automation using Terraform.

Topics include:

- Terraform basics
- Providers
- Modules
- Remote state
- GKE with Terraform
- AKS with Terraform
- EKS comparison
- Kubernetes provider
- Helm provider

### Phase 6 — Production Operations

Operating Kubernetes like a production engineer.

Topics include:

- Helm
- GitOps
- Argo CD
- Observability
- Prometheus
- Grafana
- Logging
- Security
- RBAC
- Pod Security
- Backup and restore
- Upgrade strategy
- Cost optimization

### Phase 7 — Bare-Metal Kubernetes

Understanding what managed Kubernetes hides from you.

Topics include:

- Bare-metal cluster planning
- kubeadm
- Control plane setup
- Worker node setup
- CNI plugins
- MetalLB
- Ingress controllers
- Storage
- Cluster upgrades
- Failure recovery

---

## Repository Structure

```text
kubernetes-zero-to-expert/
├── README.md
├── episodes/
│   ├── 01-first-cluster/
│   │   ├── README.md
│   │   ├── commands.md
│   │   └── manifests/
│   │       └── nginx.yaml
│   ├── 02-pods/
│   ├── 03-deployments/
│   ├── 04-services/
│   └── ...
├── terraform/
│   ├── gcp/
│   ├── azure/
│   └── aws-comparison/
├── scripts/
├── diagrams/
└── notes/
```

---

## Episode 1 — Kubernetes From Zero: Your First Cluster

In Episode 1, we build the first local Kubernetes cluster using Minikube.

You will learn:

- What Kubernetes is
- Why Kubernetes exists
- What a cluster is
- What a node is
- What a Pod is
- What a Deployment is
- What a Service is
- How to start Minikube
- How to deploy nginx
- How to scale Pods
- How to expose an app using NodePort
- How to clean up resources

Episode folder:

```text
episodes/01-first-cluster/
```

Run the lab:

```bash
cd episodes/01-first-cluster
kubectl apply -f manifests/nginx.yaml
kubectl get deploy,rs,pods,svc
minikube service hello-k8s-yaml
```

Clean up:

```bash
kubectl delete -f manifests/nginx.yaml
```

---

## Requirements

For the first phase, you need:

- Linux, macOS, or Windows with WSL2
- Docker Desktop, Podman, VirtualBox, Hyper-V, KVM, or another supported Minikube driver
- Minikube
- kubectl
- Git
- VS Code or another code editor
- Basic terminal knowledge

Later phases will require:

- Google Cloud account
- Azure account
- Optional AWS account for comparison
- Terraform
- Helm
- GitHub account
- Multiple VMs or bare-metal machines for advanced labs

---

## Quick Start

Clone the repo:

```bash
git clone https://github.com/YOUR_USERNAME/kubernetes-zero-to-expert.git
cd kubernetes-zero-to-expert
```

Start Minikube:

```bash
minikube start
```

Check your cluster:

```bash
kubectl get nodes
kubectl cluster-info
```

Run Episode 1:

```bash
cd episodes/01-first-cluster
kubectl apply -f manifests/nginx.yaml
kubectl get deploy,rs,pods,svc
```

Open the app:

```bash
minikube service hello-k8s-yaml
```

Clean up:

```bash
kubectl delete -f manifests/nginx.yaml
```

---

## Important Kubernetes Lesson

A Kubernetes Service does not create Pods.

A Deployment creates Pods.

A Service provides stable networking to Pods that already exist and match its selector.

Example:

```yaml
selector:
  app: hello-k8s-yaml
```

That selector must match the Pod labels:

```yaml
labels:
  app: hello-k8s-yaml
```

If the labels do not match, the Service will have no endpoints.

---

## YAML Multi-Document Reminder

One YAML file can contain multiple Kubernetes resources.

Each resource must be separated with:

```yaml
---
```

Example:

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

---

## Troubleshooting

Check all core resources:

```bash
kubectl get deploy,rs,pods,svc
```

Check all namespaces:

```bash
kubectl get pods -A
```

Describe a Deployment:

```bash
kubectl describe deployment hello-k8s-yaml
```

Describe a Pod:

```bash
kubectl describe pod POD_NAME
```

Check logs:

```bash
kubectl logs POD_NAME
```

Check Service endpoints:

```bash
kubectl get endpoints hello-k8s-yaml
```

Delete and recreate resources:

```bash
kubectl delete -f manifests/nginx.yaml
kubectl apply -f manifests/nginx.yaml
```

---

## Recommended Workflow

For every episode:

1. Read the episode README.
2. Review the manifests.
3. Run the commands manually.
4. Break something on purpose.
5. Troubleshoot it.
6. Clean up resources.
7. Commit your changes.

---

## Naming Convention

Episodes use this format:

```text
episodes/01-first-cluster
episodes/02-pods
episodes/03-deployments
episodes/04-services
```

Manifest files use descriptive names:

```text
nginx.yaml
pod.yaml
deployment.yaml
service.yaml
configmap.yaml
secret.yaml
```

---

## Disclaimer

This repository is for learning and lab environments.

Do not treat early labs as production-ready Kubernetes configurations.

Production Kubernetes requires additional work around:

- Security
- RBAC
- Secrets management
- Image scanning
- Network policies
- Resource limits
- Observability
- Backup and restore
- Upgrade planning
- Cost management

---

## License

MIT License

---

## Author

Created for the **Kubernetes Zero to Expert** YouTube series.
