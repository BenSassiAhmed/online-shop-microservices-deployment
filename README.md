# 🛒 Online Shop — Microservices Deployment to EKS

A complete deployment repository for a **microservices-based online shop**, orchestrated with **Kubernetes (Amazon EKS)**, **Helm**, and **Helmfile**.  
This project demonstrates how to deploy, manage, and automate a scalable cloud-native e-commerce system using DevOps best practices.

---

## 📘 Table of Contents
- [Overview](#overview)
- [Architecture](#architecture)
- [Repository Structure](#repository-structure)
- [Prerequisites](#prerequisites)
- [Quick Installation](#quick-installation)
- [Helm / Helmfile Usage](#helm--helmfile-usage)
- [CI/CD with Jenkins](#cicd-with-jenkins)
- [Kubernetes Configuration](#kubernetes-configuration)
- [Uninstallation](#uninstallation)
- [Troubleshooting](#troubleshooting)
- [Security Notes](#security-notes)
- [Contributing](#contributing)
- [License & Contact](#license--contact)

---

## 🧭 Overview

This repository automates the **deployment of an Online Shop composed of multiple microservices** onto a **Kubernetes cluster**, targeting **Amazon EKS** for production environments.

It includes:

- **Helm charts** for packaging each service  
- **Helmfile orchestration** to manage multiple releases  
- **CI/CD pipeline** powered by Jenkins  
- **Shell scripts** for installation and cleanup  
- **Configuration files** (YAML, values, architecture diagrams) to ensure full reproducibility

The project can be reused as a **reference architecture** for deploying any microservice-based app to Kubernetes using Infrastructure as Code (IaC) principles.

---

## 🏗️ Architecture

The architecture is documented in the [`architecture/`](architecture/) folder.

It follows a **microservices pattern** with separate components for:
- Frontend  
- Backend (multiple microservices)  
- Databases and cache layers  
- Networking and Ingress management  
- CI/CD automation through Jenkins  

Each service is deployed as an independent Helm release, allowing isolated scaling and updates.

---

## 📂 Repository Structure

```bash
.
├── architecture/            # Diagrams and architecture documentation
├── charts/                  # Helm charts for each microservice
├── k8s-config/              # Raw Kubernetes manifests (YAML files)
├── values/                  # Helm values files for different environments
├── Jenkinsfile              # CI/CD pipeline definition
├── helmfile.yaml            # Orchestration file for managing multiple Helm releases
├── install.sh               # Script to install/deploy all components
├── uninstall.sh             # Script to remove the deployment
└── README.md                # This file
