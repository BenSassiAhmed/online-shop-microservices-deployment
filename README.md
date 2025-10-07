
## README (Draft)

## Online Shop — Microservices deployment to EKS

```
A deployment repository for a 10-microservice online-shop example targeted at
Amazon EKS (Kubernetes). This repo contains Helm/helmfile manifests, Kubernetes
YAML, CI/CD pipeline configuration (Jenkinsfi le), and convenience scripts to
install/uninstall the stack.
```
## Table of Contents

```
Project overview
Architecture
Repository structure
Prerequisites
Quick install (example)
Helm / helmfile usage
CI / CD (Jenkins)
Kubernetes configuration and values
Uninstall / cleanup
Troubleshooting
Contributing
License & contact
```
## Project overview


This repository automates the deployment of a multi-service online shop onto a
Kubernetes cluster (intended for EKS). It collects Helm charts and Kubernetes
manifests, contains a Jenkinsfile for pipeline automation, and provides
install.sh / uninstall.sh convenience scripts. Use this repo to reproduce the full
microservices deployment or to adapt parts of it for learning CI/CD + Kubernetes.

## Architecture

High-level architecture (included in the architecture/ folder) documents how the
services communicate, ingress/load-balancing strategy, and other infra elements.
Check the architecture/ directory for diagrams and notes.

## Repository structure

(Top-level items — adjust if I missed anything)

You can explore k8s-config/ for specific resources and values/ for environment-
specific overrides.

## Prerequisites

Before deploying, make sure you have:

```
An AWS account and permissions to create EKS resources (or any Kubernetes
cluster with similar capabilities).
```
```
perl
```
```
.
├─ architecture/ # diagrams and architecture notes
├─ charts/ # Helm charts (per microservice or umbrella charts)
├─ k8s-config/ # Kubernetes manifests & resources
├─ values/ # Helm values files per environment
├─ Jenkinsfile # Jenkins pipeline
├─ helmfile.yaml # helmfile orchestration for the charts
├─ install.sh # script to install/deploy the stack
├─ uninstall.sh # script to remove the deployment
```

```
kubectl installed and configured to target your cluster.
helm and helmfile installed (if using helmfile).
(Optional) awscli configured and eksctl if you want the scripts to create the
EKS cluster.
A working Docker registry access for images (Docker Hub, ECR, etc.) — ensure
images for each microservice are accessible.
```
## Quick install (example)

If you prefer to run Helm/helmfile manually, see the Helm section.

## Helm / helmfile usage

This repo includes a helmfile.yaml to orchestrate the installation of multiple charts
at once.

Basic helmfile workflow:

```
These commands are conservative and assume install.sh is the primary
orchestrator. Inspect install.sh before running in production (it may configure
cluster resources and apply helmfile).
```
```
bash
```
```
# 1) Clone the repo
git clone https://github.com/BenSassiAhmed/online-shop-microservices-deployment.git
cd online-shop-microservices-deployment
```
```
# 2) Make install script executable
chmod +x install.sh
```
```
# 3) (OPTIONAL) Export any env vars the install script expects
# Example placeholders — replace with real values:
export AWS_PROFILE=myprofile
export EKS_CLUSTER_NAME=my-online-shop
export IMAGE_REGISTRY=your.registry.example
```
```
# 4) Run install (this will typically run helmfile/helm to deploy)
./install.sh
```

Edit values files in the values/ directory before applying to match your environment
(image registry, credentials, resource sizes, etc.).

## CI / CD (Jenkins)

A Jenkinsfile is present for pipeline automation. Typical responsibilities you can
expect in this pipeline:

```
Checkout code
Build images (or trigger builds) for each microservice
Push images to registry
Run helmfile/helm steps or apply k8s manifests to the target cluster
```
Inspect Jenkinsfile in the repo to map the stages and required Jenkins credentials
(Docker registry creds, kubeconfig, AWS credentials, etc.).

## Kubernetes configuration & environment values

```
Kubernetes manifests and configuration are inside k8s-config/ — check there
for Services, Deployments, Ingress, ConfigMaps and Secrets (or references to
secrets).
values/ contains Helm values files for environments — set the container image
tags, resource requests/limits, replicas, and any secrets/URLs.
```
Tip: use kubectl apply -f k8s-config/ for a quick local deploy, but prefer
Helm/helmfile to keep releases manageable.

```
bash
```
```
# 1) Preview what helmfile will do
helmfile -f helmfile.yaml diff
```
```
# 2) Apply (install/upgrade) everything
helmfile -f helmfile.yaml apply
```
```
# 3) To selectively apply a release:
helmfile -f helmfile.yaml -l name=<release-name> apply
```

## Uninstall / cleanup

There is an uninstall.sh script for removing the deployed resources. Example:

Double-check the script before running — ensure it will not remove unrelated
resources in your AWS account/cluster.

## Troubleshooting

```
kubectl get pods -A — check pods across namespaces.
kubectl logs <pod> — view logs for failing pods.
If Helm fails, run helm status <release> and helm -n <ns> get all
<release>.
Ensure imagePullSecrets exist if private registry images are used.
If helmfile fails, run helmfile -f helmfile.yaml sync and inspect the diff
output.
```
## Security notes

```
Do not commit plaintext credentials. Use Kubernetes Secrets, HashiCorp Vault,
or SOPS for secrets management.
Limit IAM permissions used to create/manage the cluster (principle of least
privilege).
Clean up IAM roles, load balancers, and EBS volumes to avoid unexpected
charges.
```
## Contributing

Pull requests welcome. If you want me to add a CONTRIBUTING.md or to:

```
Add sample values for staging/dev
Add example Jenkins pipeline that builds the microservices
```
```
bash
```
```
chmod +x uninstall.sh
./uninstall.sh
```

```
Add GitHub Actions instead of Jenkins
tell me and I’ll generate those files.
```
## License & contact

Add a license file if you want this project to be redistributable. Common choices:
MIT, Apache-2.0.
If you want, I can add a suitable LICENSE file and badges (build, license, docker
pulls).

## What I inspected & where (sources)

```
Repo root and file list (shows architecture, charts, k8s-config, values,
Jenkinsfile, helmfile.yaml, install.sh, uninstall.sh).
architecture/ folder listing.
k8s-config/ folder listing.
```
Would you like me to:

```
Commit this README.md to the repository (I can prepare the file contents for
you to paste), or
Create the README directly in the repo (I can prepare a ready-to-commit file and
show it here), or
Expand any section (detailed Jenkinsfile explanation, sample values files, or
example kubectl commands and expected outputs)?
```
I can also produce:

```
A CONTRIBUTING.md, LICENSE, and badges.
A step-by-step walkthrough to deploy locally (Minikube) or on EKS with eksctl if
you want an explicit, tested deployment script.
```
Tell me which of these (or just say “commit README”) and I’ll produce the file content
ready to paste/commit.


