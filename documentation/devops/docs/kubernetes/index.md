# Overview

Handy things to know about k8s.

## Delete old jobs

```shell
kubectl get \
  jobs -A -o json|jq -r \
  '.items[]|select(.status.failed == 1)|\"kubectl delete job -n \" + .metadata.namespace + \" \" + .metadata.name '"
```

## Exec into a devops utility pod

```shell
alias du="kubectl exec -ti \$(kubectl get pods -lapp.kubernetes.io/instance=devops-utility-box -o json|jq -r '.items[0].metadata.name') -- /bin/bash"
```
