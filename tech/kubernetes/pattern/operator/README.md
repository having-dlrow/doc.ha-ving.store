# Operator

## kubebuilder vs operator-sdk <a href="#kubebuilder-vs-operator-sdk" id="kubebuilder-vs-operator-sdk"></a>

* 2018년 1.0.0 이 출시된 프로젝트 ( operator-sdk 가 먼저 출시되었다 )
* 두 프로젝트 실행이 비슷하다.

```
├── Dockerfile
├── Gopkg.lock
├── Gopkg.toml
├── Makefile
├── PROJECT
├── README.md
├── bin
├── cmd
│   └── manager
├── config      // yaml 
│   ├── crds
│   ├── default
│   ├── manager
│   ├── rbac
│   └── samples
├── crd         // custom definition
├── hack
├── pkg
│   ├── apis
│   ├── controller
│   └── webhook
└── vendor
```

1단계. Create API

`Kubebuilder create api --group {mygroup}  --version v1 --Kind {MyKind}`

* Custom API 정의를 만드는 것



2단계. Manifests 정의

* CRD 객체를 정의한다.
* (주의) 주석을 통해서 생성되므로, 코드의 주석에 주의하자

```
# in code
type IPAddressSpec struct {
    // IPAllocatorName is the IPAllocator's name used to allocate this ip.
    // +kubebuilder:validation:MinLength=1
    IPAllocatorName string `json:"ipallocatorName"`
}

# in CRD yaml
ipallocatorName:
  description: IPAllocatorName is the IPAllocator's name used to allocate
    this ip.
  minLength: 1
  type: string
```

```
# in code
// IPAllocator is the Schema for the ipallocators API
// +genclient
// +k8s:deepcopy-gen:interfaces=k8s.io/apimachinery/pkg/runtime.Object
// +kubebuilder:printcolumn:name="source",type="string",JSONPath=".spec.source"
// +kubebuilder:printcolumn:name="state",type="string",JSONPath=".status.state"
// +kubebuilder:printcolumn:name="free",type="string",JSONPath=".status.capacity.free"
// +kubebuilder:subresource:status
// +k8s:openapi-gen=true
type IPAllocator struct { ... }

# in CRD yaml
  additionalPrinterColumns:
  - JSONPath: .spec.source
    name: source
    type: string
  - JSONPath: .status.state
    name: state
    type: string
  - JSONPath: .status.capacity.free
    name: free
    type: string
...
  subresources:
    status: {}
```

