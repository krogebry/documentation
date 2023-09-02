# Overview

Overview stuff

## Bash shortcuts

Thanks to *Stefan Gloutnikov* for this little gem:

```shell
# Impersonate -admin in Kubie namespace
kubieKubectlAsAdmin() {
  KUBENS=$(cat $KUBIE_KUBECONFIG | yq '.contexts[0].context.namespace')
  kubectl $(echo "$@") --as $KUBENS-admin
}
alias ka='kubieKubectlAsAdmin'
```

Put this into your `~/.zshrc` or `~/.bashrc` and use as such:

```shell
ka port-forward svc/service-name 8080:8080
```

`port-forward` requires admin permissions, so `ka` will do that for you as a one-off from your normal commands.

You can also use this for various other commands like secrets:

```shell
ka get secrets
```

### Helm

In the case of a helm deployment, you might have to use something slightly different:

```shell
# Impersonate -admin in Kubie namespace
kubieHelmAsAdmin() {
  KUBENS=$(cat $KUBIE_KUBECONFIG | yq '.contexts[0].context.namespace')
  helm --as-kube-user $KUBENS-admin $(echo "$@") 
}
alias ha='kubieHelmAsAdmin'
```

And use like this to list helm charts:

```shell
ha list 
```

## Events

Another handy trick is to use something you'll see me use quite often:

```shell
alias kge='kubectl get events --sort-by='\''{.lastTimestamp}'\'''
```

This will sort events from the event log, giving you the most recent first.


## Autocomplete

This snippet enables `kubectl` autocomplete ( tab out ) and an alias for `k`
```shell
source <(kubectl completion zsh)
alias k=kubectl
complete -F __start_kubectl k
```

It might not seem like much, but this shortens `kubectl` to `k`, and if you're doing *a lot* of kubectl commands, this
can end up being a huge time saver.

