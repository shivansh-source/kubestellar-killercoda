# KubeStellar: Multi-WEC Topology

In this scenario, you will see how **KubeStellar scales from one cluster to many** without changing how workloads are defined or deployed.

In real environments, platform teams manage:
- Multiple Kubernetes clusters
- Different regions, zones, or edge locations
- Growing numbers of Workload Execution Clusters (WECs)

KubeStellar is designed so that **adding more clusters does not add more operational complexity**.

---

## What you will do

In this scenario, you will:

- Install KubeStellar in a fresh environment
- Create multiple Workload Execution Clusters (WECs)
- Deploy a workload **once**
- Use a BindingPolicy to control where that workload runs
- Scale the workload to multiple clusters **by changing policy only**

---

## What you will NOT do

- You will not run `kubectl apply` against WEC clusters
- You will not copy manifests between clusters
- You will not manage per-cluster deployments

KubeStellar handles distribution for you.

---

## Key idea to keep in mind

> **Scaling with KubeStellar is a policy change, not a deployment change.**

When you are ready, continue to install KubeStellar and set up a multi-cluster environment.
