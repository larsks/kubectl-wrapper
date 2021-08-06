# kubectl-wrapper

`kubectl-wrapper` is a simple wrapper script that supports per-project
kubeconfig files. If run `kubectl-wrapper` instead of `kubectl`, it
will look for a `.kubeconfig` file in your current directory. It will
search parent directories until it finds one (or runs out of parent
directories).

If the wrapper finds a `.kubeconfig` file, it will set the
`KUBECONFIG` environment variable to point to that file before running
`kubectl`.

I put the script in `~/bin/k` so that I can use it like this:

```
k get pod
```

With appropriately placed `.kubeconfig` files, this will Do the Right
Thing as I move between project directories.
