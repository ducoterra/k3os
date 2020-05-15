# Configuration Settings

## Upgrade

```bash
kubectl --context admin label node mainframe plan.upgrade.cattle.io/k3os-latest=enabled
```

wait for upgrade

```bash
kubectl --context admin label node mainframe plan.upgrade.cattle.io/k3os-latest-
kubectl --context admin uncordon mainframe
```
