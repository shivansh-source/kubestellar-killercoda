# Install KubeStellar and Create a Multi-WEC Environment

In this step, you will set up a fresh multi-cluster environment and install **KubeStellar**.

This scenario is self-contained. Everything is installed from scratch.

---

## Verify prerequisites

KubeStellar requires Docker and Kubernetes tooling.  
First, confirm Docker is available in this environment.

```bash
docker version
```{}

> If Docker is not available or fails here, this scenario cannot proceed.

---

## Install kind (Kubernetes in Docker)

We will use **kind** to create multiple Kubernetes clusters locally.

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.23.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```{}

Verify the installation:

```bash
kind version
```{}

---

## Create Kubernetes clusters

Create one hosting cluster and **two Workload Execution Clusters (WECs)**.

```bash
kind create cluster --name hosting
kind create cluster --name wec1
kind create cluster --name wec2
```{}

Verify that all clusters were created:

```bash
kind get clusters
```{}

You should see output similar to:
hosting
wec1
wec2
---

## Install kubectl

Install `kubectl` to interact with the Kubernetes clusters.

```bash
curl -LO https://dl.k8s.io/release/v1.30.0/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```{}

Verify the installation:

```bash
kubectl version --client
```{}

---

## Install KubeStellar

Clone the KubeStellar repository:

```bash
git clone https://github.com/kubestellar/kubestellar.git
cd kubestellar
```{}

Install KubeStellar using the demo environment script:

```bash
./scripts/create-kubestellar-demo-env.sh
```{}

> ⏳ This step may take several minutes to complete.

---

## Verify KubeStellar installation

Check that KubeStellar namespaces exist:

```bash
kubectl get namespaces
```{}

Check that KubeStellar CRDs are installed:

```bash
kubectl get crds | grep kubestellar
```{}

Verify that all KubeStellar components are running:

```bash
kubectl get pods -A
```{}

At this point, you should have:

- One hosting/control environment
- Two Workload Execution Clusters (WECs)
- KubeStellar fully installed and running

Continue to the next step to deploy a workload and observe initial placement.
