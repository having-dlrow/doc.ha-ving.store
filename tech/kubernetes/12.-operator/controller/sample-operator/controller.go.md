# Controller.go

controller 구조는 아래와 같다.

```
type Controller struct {
	// 기본 Kubernetes 클라이언트셋
	kubeclientset kubernetes.Interface
	// 사용자 정의 API 그룹 클라이언트셋
	sampleclientset clientset.Interface

        // 리소스 인덱스 조회기
	deploymentsLister appslisters.DeploymentLister
	foosLister        listers.FooLister

        // informer cache을 통한 동기화 여부
	deploymentsSynced cache.InformerSynced
	foosSynced        cache.InformerSynced

	// 작업 큐
	workqueue workqueue.TypedRateLimitingInterface[cache.ObjectName]
	// 이벤트 기록기
	recorder record.EventRecorder
}
...
	controller := &Controller{
		kubeclientset:     kubeclientset,
		sampleclientset:   sampleclientset,
		deploymentsLister: deploymentInformer.Lister(),
		deploymentsSynced: deploymentInformer.Informer().HasSynced,
		foosLister:        fooInformer.Lister(),
		foosSynced:        fooInformer.Informer().HasSynced,
		workqueue:         workqueue.NewTypedRateLimitingQueue(ratelimiter),
		recorder:          recorder,
	}
```



### 정의된 Schema 등록

{% hint style="success" %}
generated 디렉토리에 정의된다. 재 정의를 위해 ./hack/update-codegen.sh 실행
{% endhint %}

```
      import ( samplescheme "k8s.io/sample-controller/pkg/generated/clientset/versioned/scheme" )
      ...
      utilruntime.Must(samplescheme.AddToScheme(scheme.Scheme))
```

### Recorder 생성

```
	eventBroadcaster := record.NewBroadcaster(record.WithContext(ctx))
        // 이벤트 브로드캐스터가 로깅을 시작한다.(0은 로깅 레벨을 의미한다.)
	eventBroadcaster.StartStructuredLogging(0)
        // Kubernetes API 서버의 이벤트 싱크에 이벤트를 기록하도록 설정한다.
	eventBroadcaster.StartRecordingToSink(&typedcorev1.EventSinkImpl{Interface: kubeclientset.CoreV1().Events("")})
        // 이벤트 레코드 생성. Controller에서 발생하는 이벤트를 기록하는데 사용한다.
	recorder := eventBroadcaster.NewRecorder(scheme.Scheme, corev1.EventSource{Component: controllerAgentName})	
```

\`kubectl get events\` 명령어로 Event을조회 할 수 있다.  Record을 통해 Controller 변경사항을 알 수 있다.

### Informer의 Add/ Update EventHandler 등록

```
	fooInformer.Informer().AddEventHandler(cache.ResourceEventHandlerFuncs{
		AddFunc: controller.enqueueFoo,
		UpdateFunc: func(old, new interface{}) {
			controller.enqueueFoo(new)
		},
	})

	deploymentInformer.Informer().AddEventHandler(cache.ResourceEventHandlerFuncs{
		AddFunc: controller.handleObject,
		UpdateFunc: func(old, new interface{}) {
			newDepl := new.(*appsv1.Deployment)
			oldDepl := old.(*appsv1.Deployment)
			if newDepl.ResourceVersion == oldDepl.ResourceVersion {
				// Periodic resync will send update events for all known Deployments.
				// Two different versions of the same Deployment will always have different RVs.
				return
			}
			controller.handleObject(new)
		},
		DeleteFunc: controller.handleObject,
	})	
```

Informer는 Foo 리소스 변화를 감지한다. 추가/변경에 대해 지정된 함수가 실행 되도록 한다.

```
type ResourceEventHandlerFuncs struct {
	// 새 리소스가 생성 될 때 호출되는 callback
	AddFunc    func(obj interface{})
	
	UpdateFunc func(oldObj, newObj interface{})
	// 리소스가 지워질 때 호출되는 callback
	DeleteFunc func(obj interface{})           
}
```

ResourceEventHandlerFuncs 인터페이스를 통해 생성/수정/삭제 이벤트를 지정할 수 있다.\
단, UpdateFunc는 리소스가 업데이트 될 때 호출 되거나 re-syncronization이 일어나는 경우, 변경사항이 없더라도 호출된다.&#x20;

#### enqueueFoo()

```
	func (c *Controller) enqueueFoo(obj interface{}) {
		if objectRef, err := cache.ObjectToName(obj); err != nil {
			utilruntime.HandleError(err)
			return
		} else {
			c.workqueue.Add(objectRef)
		}
	}
```

cache.ObjectToName(obj) 을 통해 Object의 Meta정보를 기반으로 키를 만들고, 이를 workqueue의 키로 하여 작업 대상을 등록한다.

#### handleObject()
