# Scale Out: Multi-WEC Propagation via Policy

In this step, you will scale the workload from **one cluster to multiple clusters** by changing **only the BindingPolicy**.

The workload definition will remain unchanged.

---

## Update the BindingPolicy to target multiple WECs

Create a new BindingPolicy that targets **both `wec1` and `wec2`**.

```bash
cat <<EOF > bindingpolicy-multi-wec.yaml
apiVersion: control.kubestellar.io/v1alpha1
kind: BindingPolicy
metadata:
  name: demo-nginx-to-multi-wec
spec:
  clusterSelectors:
  - matchLabels:
      kubestellar.io/cluster-name: wec1
  - matchLabels:
      kubestellar.io/cluster-name: wec2
  downsync:
  - objectSelectors:
    - matchLabels:
        app: demo-nginx
EOF
```{}

---

## Apply the updated BindingPolicy

Apply the new policy from the control environment:

```bash
kubectl apply -f bindingpolicy-multi-wec.yaml
```{}

> The workload itself is **not** modified or reapplied.

---

## Observe workload propagation

Verify that the workload is running on **both WECs**.

Check `wec1`:

```bash
kubectl --context wec1 get pods
```{}

Check `wec2`:

```bash
kubectl --context wec2 get pods
```{}

You should now see a `demo-nginx` pod running in **both clusters**.

---

## Confirm identical behavior

Both clusters received:
- The same workload
- From the same definition
- Without per-cluster deployment commands

This demonstrates that **cluster count does not increase operational complexity**.

---

## Key takeaway

- Scaling is achieved by **changing intent**
- Workloads remain unchanged
- KubeStellar distributes Kubernetes objects across clusters automatically

Continue to the final step to summarize what you learned.
