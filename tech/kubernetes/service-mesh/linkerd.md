# Linkerd

### CLI 설치 <a href="#step-1-install-the-cli" id="step-1-install-the-cli"></a>

```bash
curl --proto '=https' --tlsv1.2 -sSfL https://run.linkerd.io/install-edge | sh
```

```bash
Add the linkerd CLI to your path with:

  export PATH=$PATH:/home/ysyoop/.linkerd2/bin

Now run:

  linkerd check --pre                         # validate that Linkerd can be installed
  linkerd install --crds | kubectl apply -f - # install the Linkerd CRDs
  linkerd install | kubectl apply -f -        # install the control plane into the 'linkerd' namespace
  linkerd check                               # validate everything worked!

You can also obtain observability features by installing the viz extension:

  linkerd viz install | kubectl apply -f -  # install the viz extension into the 'linkerd-viz' namespace
  linkerd viz check                         # validate the extension works!
  linkerd viz dashboard                     # launch the dashboard
```



