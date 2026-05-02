
# Kyverno Policy Enforcement

## Overview

This repository contains a curated set of production-grade [Kyverno](https://kyverno.io/) policies and supporting manifests for Kubernetes clusters. Kyverno is a Kubernetes-native policy engine that helps you validate, mutate, and generate resources to ensure best practices, security, and compliance.

## Features
- **Ready-to-use Kyverno policies** for common production scenarios
- **Kind cluster configuration** for local testing
- **Sample manifests** to test policy enforcement
- **Step-by-step installation and usage guide**

## Folder Structure

```
├── kind_cluster/           # Kind cluster configuration
│   └── kind-config.yaml
├── kyverno_install/        # Kyverno installation instructions
│   └── install.txt
├── kyverno_policy/         # Kyverno policy YAMLs
│   ├── policy-01.yaml
│   ├── policy-02.yaml
│   └── ...
├── manifests/              # Test manifests for policy validation
│   ├── deployment_failed.yaml
│   ├── deployment_passed.yaml
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
Follow the instructions in `kyverno_install/install.txt` or run:
```sh
kubectl create -f https://raw.githubusercontent.com/kyverno/kyverno/main/config/release/install.yaml
```

### 4. Apply Kyverno Policies
```sh
kubectl apply -f kyverno_policy/
```

### 5. Test Policy Enforcement
Apply the test manifests to see policy enforcement in action:
```sh
kubectl apply -f manifests/deployment_passed.yaml   # Should pass
kubectl apply -f manifests/deployment_failed.yaml   # Should be blocked
```

## Policy List
- **policy-01.yaml**: [require-resources]
- **policy-02.yaml**: [disallow-latest-tag]
- **policy-03.yaml**: [create-resourcequota]
- **policy-04.yaml**: [add-team-label]
- **policy-05.yaml**: [restrict-image-registries]
- **policy-06.yaml**: [enforce-security-context]
- **policy-07.yaml**: [enforce-replica-range]

> _Update the above with specific policy details as needed._

## Resources
- [Kyverno Documentation](https://kyverno.io/docs/)
- [Kyverno Policy Library](https://kyverno.io/policies/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)

## License

This project is licensed under the MIT License.
