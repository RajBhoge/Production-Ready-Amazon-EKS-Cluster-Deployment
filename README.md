# Production-Ready Amazon EKS Cluster Deployment

A comprehensive guide to deploying a **production-grade Amazon EKS (Elastic Kubernetes Service)** cluster on AWS — covering cluster setup, node groups, networking, security, and observability.

## Overview

This repository documents the full lifecycle of deploying a hardened, production-ready EKS cluster: from initial provisioning through security hardening, autoscaling configuration, and monitoring setup.

## Architecture

```
EKS Control Plane (Managed by AWS)
         |
  Managed Node Groups (EC2 in private subnets)
         |
  AWS Load Balancer Controller (ALB Ingress)
         |
  CloudWatch / Prometheus / Grafana (Observability)
```

## What's Covered

- **EKS Cluster Provisioning** — Using `eksctl` or Terraform
- **Managed Node Groups** — EC2-backed worker nodes with auto-scaling
- **VPC & Networking** — Private/public subnets and CNI configuration
- **IAM Roles for Service Accounts (IRSA)** — Pod-level AWS permissions via OIDC
- **Cluster Autoscaler** — Automatic node scaling based on pod demand
- **AWS Load Balancer Controller** — ALB/NLB via Kubernetes ingress
- **Monitoring & Logging** — CloudWatch Container Insights, Prometheus, Grafana
- **Security Hardening** — Network policies, secrets encryption, pod security standards

## Quick Start with eksctl

```bash
eksctl create cluster \
  --name prod-cluster \
  --region eu-central-1 \
  --nodegroup-name standard-workers \
  --node-type m5.large \
  --nodes 3 \
  --nodes-min 2 \
  --nodes-max 10 \
  --managed

aws eks update-kubeconfig --name prod-cluster --region eu-central-1
kubectl get nodes
```

## Production Checklist

- [ ] Private endpoint access enabled for control plane
- [ ] Secrets encrypted with AWS KMS
- [ ] Node groups in private subnets
- [ ] IRSA configured (not node IAM roles)
- [ ] Cluster Autoscaler deployed
- [ ] CloudWatch logging enabled
- [ ] Network policies enforced
- [ ] Regular EKS version upgrades scheduled

## Technologies

| Technology | Purpose |
|------------|---------|
| Amazon EKS | Managed Kubernetes control plane |
| EC2 Managed Node Groups | Worker nodes |
| AWS Load Balancer Controller | Ingress and load balancing |
| Cluster Autoscaler | Node auto-scaling |
| CloudWatch | Logging and metrics |
| Terraform / eksctl | Cluster provisioning IaC |

## Author

**Raj Bhoge** — Cloud & AI Engineer  
[GitHub](https://github.com/RajBhoge) | [LinkedIn](https://www.linkedin.com/in/raj-bhoge-834280194/) | [Blog](https://rajbhoge2107.hashnode.dev/)
