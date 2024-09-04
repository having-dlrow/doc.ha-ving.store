# Sample-operator

{% embed url="https://github.com/kubernetes/sample-controller" %}

```
sample-controller/
├── artifacts/examples							
│   └── crd-status-subresource.yaml
│   └── crd.yaml
│   └── example-foo.yaml
├── pkg/
│   └── apis/{version}
│       ├── doc.go
│       ├── register.go
│       ├── types.go
│       └── zz_generated.deepcopy.go
│   └── generated/
│       ├── clientset
│       ├── informers
│       └── listers
├── controller.go                                          -- 2.controller.go
├── main.go						   -- 1.main.go
└── Makefile
```

### main.go

* controller의 진입점 역할, config, log 등을 설정을 하며, informer, clientset을 controller 에게 전달한다.

### controller.go

* Kubernetes resource을 관찰하고 처리하는 핵심 로직을 담고 있는 controller을 정의한다.&#x20;
* workQueue에 Resource의 Meta정보를 키로 하여 저장하며, Resource의 생성, 삭제시 등록된 handler 함수가 실행되도록 처리한다.



