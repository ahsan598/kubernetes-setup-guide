# 🚀 Kubernetes Setup Guides (Kind + Helm)

This repository provides practical, step-by-step guides for setting up Kubernetes locally using **KIND (Kubernetes in Docker)** and managing applications with **Helm**, the Kubernetes package manager.

These guides are ideal for **DevOps practice, learning Kubernetes, CI environments, and local testing**.


### 📘 Guides Included

| Guide                                           | Description                                                             | Link                                            |
| ------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------- |
| **Kubernetes Local Setup using Kind**             | Create a single-node local Kubernetes cluster for development & testing | ➤ [View Guide](/kind-setup/)      |
| **Multi-Node Kind Cluster Setup**                 | Create a 3-node (1 control-plane + 2 worker) Kind cluster               | ➤ [View Guide](/multinode-setup/) |
| **Helm Guide for Kubernetes (With Kind Cluster)** | Install & use Helm, deploy charts, upgrades, rollbacks                  | ➤ [View Guide](/helm-setup/)      |


### 🛠️ Prerequisites

Ensure the following tools are installed before using any guide:
| Requirement | Purpose                                               |
| ----------- | ----------------------------------------------------- |
| **Docker**  | Required to run Kind nodes (Kubernetes inside Docker) |
| **kubectl** | CLI to interact with Kubernetes clusters              |
| **Kind**    | Create & manage Kubernetes clusters locally           |
| **Helm**    | Install, upgrade, and manage Kubernetes applications  |



###  🚀 Get Started
Navigate into any guide folder:
```sh
cd kind-setup
cd multinode-setup
cd helm-setup
```
Each folder contains its own README with complete instructions.

---

### 📚 Official Reference

- [Kind Installation](https://kind.sigs.k8s.io/docs/user/quick-start/)
- [Kubectl Installation](https://kubernetes.io/docs/tasks/tools/)
- [Docker Installation](https://docs.docker.com/engine/install/)
- [Helm Installation](https://helm.sh/docs/intro/install/)