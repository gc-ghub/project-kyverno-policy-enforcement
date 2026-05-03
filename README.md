
# Kyverno Policy Enforcement

## Overview

This repository contains a curated set of production-grade [Kyverno](https://kyverno.io/) policies and supporting manifests for Kubernetes clusters. Kyverno is a Kubernetes-native policy engine that helps you validate, mutate, and generate resources to ensure best practices, security, and compliance.

## Features
- **Ready-to-use Kyverno policies** for common production scenarios
- **Kind cluster configuration** for local testing
- **Sample manifests** to test policy enforcement
- **ArgoCD application manifests for GitOps deployment**
- **Automated policy validation with GitHub Actions**
- **Step-by-step installation and usage guide**

## Folder Structure

```
├── argocd/                 # ArgoCD application manifests
│   ├── app-manifests.yaml
│   └── kyverno-argocd-app.yaml
├── .github/
│   └── workflows/
│       └── policy_validation.yaml   # GitHub Actions workflow for policy validation
├── kind_cluster/           # Kind cluster configuration
│   └── kind-config.yaml
├── kyverno_install/        # Kyverno installation instructions
│   └── install.txt
├── kyverno_policy/         # Kyverno policy YAMLs
│   ├── policy-01.yaml
│   ├── policy-02.yaml
│   ├── policy-03.yaml
│   ├── policy-04.yaml
│   ├── policy-05.yaml
│   ├── policy-06.yaml
│   └── policy-07.yaml
├── manifests/              # Test manifests for policy validation
│   ├── deployment.yaml
│   └── namespace.yaml
└── README.md               # Project documentation
```

## Getting Started

### 1. Prerequisites
- [Docker](https://www.docker.com/)
- [Kind](https://kind.sigs.k8s.io/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)

### 2. Create a Kind Cluster
```sh
kind create cluster --config kind_cluster/kind-config.yaml
```

### 3. Install Kyverno
Follow the instructions in `kyverno_install/install.txt` (Helm-based) or run:
```sh
kubectl create -f https://raw.githubusercontent.com/kyverno/kyverno/main/config/release/install.yaml
```

### 4. Apply Kyverno Policies
```sh
kubectl apply -f kyverno_policy/
```

### 5. Deploy with ArgoCD (Optional)
If you use [ArgoCD](https://argo-cd.readthedocs.io/), you can deploy the application and policies using the manifests in the `argocd/` folder:

```sh
# Create ArgoCD Applications
kubectl apply -f argocd/app-manifests.yaml
kubectl apply -f argocd/kyverno-argocd-app.yaml
```

### 6. Test Policy Enforcement
Apply the test manifests to see policy enforcement in action:
```sh
kubectl apply -f manifests/deployment.yaml   # Should be validated by policies
kubectl apply -f manifests/namespace.yaml    # Should be validated by policies
```

### 7. Automated Policy Validation (CI)
On every pull request to `main`, [GitHub Actions](https://github.com/features/actions) will automatically validate your manifests against the Kyverno policies using the workflow in `.github/workflows/policy_validation.yaml`.

Artifacts and validation results are uploaded for review in the PR.

## Policy List
- **policy-01.yaml**: Enforces CPU and memory requests/limits for all containers.
- **policy-02.yaml**: Disallows use of the `latest` image tag.
- **policy-03.yaml**: Automatically generates a `ResourceQuota` for each namespace.
- **policy-04.yaml**: Adds a `team: platform` label to all Pods.
- **policy-05.yaml**: Restricts images to only those from `docker.io` registry.
- **policy-06.yaml**: Enforces `runAsNonRoot` and disables privilege escalation for containers.
- **policy-07.yaml**: Ensures Deployments have replicas between 2 and 4.

## Resources
- [Kyverno Documentation](https://kyverno.io/docs/)
- [Kyverno Policy Library](https://kyverno.io/policies/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [ArgoCD Documentation](https://argo-cd.readthedocs.io/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)

## License

This project is licensed under the MIT License.
