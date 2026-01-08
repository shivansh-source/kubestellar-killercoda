# Testing Checklist

## How to Test

1. Push this branch to GitHub
2. Add repo to [Killercoda account](https://killercoda.com/creator/repository)  
3. Run scenario at killercoda.com/\<username>/\<repo>
4. Document results below
5. Update scenario files with actual outputs
6. Remove completed TODOs

## Environment Tests

- [ ] **Docker in Killercoda ubuntu**
  - Run: `docker version`
  - Document: Docker version, any install issues
  - If broken: May need kubernetes-kubeadm backend instead

- [ ] **kind in Killercoda ubuntu**  
  - Run: `kind version`
  - Run: `kind create cluster --name test` (after Docker confirmed)
  - Document: Does kind cluster creation work?
  - If broken: This is a showstopper, scenario won't work

- [ ] **Resource usage**
  - During install, run: `free -h` and `df -h`
  - Document: Memory/disk usage
  - Check: Killercoda session stays responsive

- [ ] **Install timing**
  - Time the install script start to finish
  - Document: Actual install time
  - Critical: Must complete in < 1hr (Killercoda free tier limit)

## Installation Output Tests

- [ ] **Cluster names**
  - Run: `kind get clusters` after install
  - Document: Exact output (cluster name)
  - Update: step3/text.md with expected output

- [ ] **Namespace names**
  - Run: `kubectl get namespaces` after install
  - Document: KubeStellar-specific namespaces
  - Update: step3/text.md with expected namespaces

- [ ] **Context names**
  - Run: `kflex ctx` after install  
  - Document: Exact output (control plane contexts)
  - Update: step3/text.md with expected contexts

- [ ] **Component health**
  - Run: `kubectl get pods -A` after install
  - Document: Expected running pods/namespaces
  - Consider: Adding this check to step3

## Post-Testing Updates

- [ ] Remove TODO from step1/text.md (if install commands work)
- [ ] Remove TODO from step2/text.md (document cluster/namespace/context names)
- [ ] Remove TODO from step3/text.md (add expected outputs)
- [ ] Update index.json comment about ubuntu backend (if Docker/kind confirmed)
- [ ] Update this NOTES.md with findings

## Known Issues

Document any issues found during testing:
- Issue description
- Workaround or fix
- Whether it blocks scenario completion
