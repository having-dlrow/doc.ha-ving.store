# 1. Install

## 1.Helm 설치



## 2.IstioCtl 설치

## Install&#x20;

[https://istio.io/latest/docs/setup/getting-started/#download](https://istio.io/latest/docs/setup/getting-started/#download)&#x20;

```
curl -L https://istio.io/downloadIstio | sh -
cd istio-1.22.3
cp -v ./bin/istioctl /usr/local/bin
```

특정 버전 다운로드

```
curl -sL https://istio.io/downloadIstioctl | ISTIO_VERSION=1.10.3 TARGET_ARCH=x86_64 sh -
```

***

```
istioctl install istio-operator.yaml
```

```
apiVersion: install.istio.io/v1alpha1
kind: IstioOperator
metadata:
  namespace: istio-system
  name: istiocontrolplane
spec:
  profile: default
  components:
    egressGateways:
    - name: istio-egressgateway
      enabled: true
      k8s:
        hpaSpec:
          minReplicas: 2
    ingressGateways:
    - name: istio-ingressgateway
      enabled: true
      k8s:
        hpaSpec:
          minReplicas: 2
    pilot:
      enabled: true
      k8s:
        hpaSpec:
          minReplicas: 2
  meshConfig:
    enableTracing: true
    defaultConfig:
      holdApplicationUntilProxyStarts: true
    accessLogFile: /dev/stdout
    outboundTrafficPolicy:
      mode: REGISTRY_ONLY
```



