# Linkerd

[Linkerd vs. Istio (Rust vs. C++) performance benchmark (2023) ](https://www.youtube.com/watch?v=pzcuE0aVvP0)

<figure><img src="../../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

* CPU 사용량 및 Latency 에서 Linked 가 우수한 성과를 보였다.

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



