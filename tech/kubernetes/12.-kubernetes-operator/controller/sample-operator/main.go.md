# main.go

### Server Shutdown

```
      func SetupSignalHandler() context.Context {
            close(onlyOneSignalHandler) // panics when called twice
   
            c := make(chan os.Signal, 2)
            ctx, cancel := context.WithCancel(context.Background())
            signal.Notify(c, shutdownSignals...)
            go func() {
            <-c
            cancel()           
            <-c
            os.Exit(1)          // second signal. Exit directly.
            }()
           
            return ctx
      }
      
      ...
// set up signals so we handle the first shutdown signal gracefully
stopCh := signals.SetupSignalHandler()
```

프로그램 종료 처리를 위한 Handler을 등록합니다.

SIGTERM, SIGINT이 처음 발생하면 context을 취소, 두번째 발생하면 즉시 프로그램을 종료합니다.

### clientset을 생성

```
	cfg, err := clientcmd.BuildConfigFromFlags(masterURL, kubeconfig)
	kubeClient, err := kubernetes.NewForConfig(cfg)   // Deployment 
	exampleClient, err := clientset.NewForConfig(cfg) // CustomResource 
```

kubernetes API 사용을   위한 Client 객체 생성

### Informer 생성

```
	kubeInformerFactory := kubeinformers.NewSharedInformerFactory(kubeClient, time.Second*30)
	exampleInformerFactory := informers.NewSharedInformerFactory(exampleClient, time.Second*30)
```

kubeInformerFactory을 통해, Informer 생성

### Controller 생성

```
	controller := NewController(ctx, kubeClient, exampleClient,
		kubeInformerFactory.Apps().V1().Deployments(),
		exampleInformerFactory.Samplecontroller().V1alpha1().Foos())
```

client 객체와 Informer에 동록한Deployment , CustomResource(Foo) 인자 전달 하여 Controller 생성

