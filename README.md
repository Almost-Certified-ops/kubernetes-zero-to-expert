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