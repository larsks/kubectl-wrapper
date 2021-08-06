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

## Per-project environment variables

If there is a `.kubeconfig.env` file next to the selected
`.kubeconfig` file, the contents will be sourced into
`kubectl-wrapper` inside a `set -a` context (which means any variables
set or modified in the file are exported to the environment).

This can be used to configure proxies (by setting e.g. the
`https_proxy` environment variable), or to automatically prefer `oc`
over `kubectl` for some projects (by setting `K_USE_OC=1`).

## Support for `oc`

If the first argument passed to the wrapper is `oc`, `kubectl-wrapper`
will execute the remainder of the command line using `oc` instead of
`kubectl`:

```
$ k oc whoami
```

If you use `oc` all the time, you can instead set the `K_USE_OC`
environment variable, which will cause the wrapper to always use `oc`:

```
$ export K_USE_OC=1
$ k whoami
```

## Logging

The `$K_LOGLEVEL` environment variable controls logging verbosity. Set
`K_LOGLEVEL=1` for verbose messages, and `K_LOGLEVEL=0` for debug
messages.
