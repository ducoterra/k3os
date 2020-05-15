# Configuration Settings

## Upgrade

```bash
kubectl --context admin label node mainframe plan.upgrade.cattle.io/k3os-latest=enabled
```

Wait for upgrade. If the node fails to uncordon itself:

```bash
kubectl --context admin label node mainframe plan.upgrade.cattle.io/k3os-latest-
kubectl --context admin uncordon mainframe
```
