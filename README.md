# Configuration Settings

## Apply DNS Changes

```bash
kubectl apply -f k8s/
# force dns reload
kubectl delete pod --namespace kube-system --selector k8s-app=kube-dns
```
