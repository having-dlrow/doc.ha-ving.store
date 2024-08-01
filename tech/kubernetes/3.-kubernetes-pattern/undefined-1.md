# 🚦 배포 전략

## Rolling

### 컨셉

Rolling 배포는 애플리케이션을 중단 없이 업데이트하기 위해 기존 버전을 새로운 버전으로 점진적으로 교체하는 전략이다. Kubernetes 기본 배포 방식

### 단점&#x20;

* 업데이트 프로세스 동안, 두 버전의 컨테이너가 동시에 실행된다. ( 오류 생성 가능성 )
* 업데이트 프로세스가 느리거나 긴 시간이 걸릴 수 있다.

### 상세 내용

```yaml
Kind: Deployment
Spec:
  replicas: 3
  strategy: 
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1                <-- 업데이트 동안 일시적으로 지정된 레플리카 수에 더해짐, 총4개
      maxUnavailable : 1         <-- 업데이트 동안 사용 불가능하게 될 수 있는 파드의 수 
```

***

## Blue - Green&#x20;

### 컨셉

Blue-Green 배포는 두 개의 환경을 설정하여, 하나는 프로덕션(예: Blue)이고 다른 하나는 대기 상태(예: Green)로 유지합니다. 신속한 롤백을 위해 사용한다. Kubernetes 설정으로 제공되지는 않는다. Argo Rollout을 통해 구현 가능하다.

### 단점&#x20;

* 두 환경을 유지해야 하므로 인프라 비용이 높다.
* 스위칭 과정에서 데이터 동기화 문제가 발생할 수 있다.

### 상세 설명

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Rollout
metadata:
  name: rollout-bluegreen
spec:
  replicas: 2
  revisionHistoryLimit: 2
  selector:
    matchLabels:
      app: rollout-bluegreen
  template:
    metadata:
      labels:
        app: rollout-bluegreen
    spec:
      containers:
      - name: rollouts-demo
        image: argoproj/rollouts-demo:blue
        imagePullPolicy: Always
        ports:
        - containerPort: 8080
  strategy:
    blueGreen: 
      activeService: rollout-bluegreen-active
      previewService: rollout-bluegreen-preview
      autoPromotionEnabled: false
---
kind: Service
apiVersion: v1
metadata:
  name: rollout-bluegreen-active
spec:
  selector:
    app: rollout-bluegreen
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080

---
kind: Service
apiVersion: v1
metadata:
  name: rollout-bluegreen-preview
spec:
  selector:
    app: rollout-bluegreen
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080      
```

***

## Canary

### **컨셉**

새로운 버전을 일부 사용자에게만 노출하여 네트워크 및 안정성을 테스트하는 전략이다. \
업데이트의 위험을 줄이고, 잠재적인 문제를 사전에 감지할 수 있다. Kubernetes 설정으로 제공되지는 않는다. Argo Rollout을 통해 구현 가능하다.

### **단점**

* 작은 규모로 테스트하므로, 모든 문제를 완전히 검증할 수 없을 수 있다.

### 상세 내용

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Rollout
metadata:
  name: rollout-canary
spec:
  replicas: 5
  revisionHistoryLimit: 2
  selector:
    matchLabels:
      app: rollout-canary
  template:
    metadata:
      labels:
        app: rollout-canary
    spec:
      containers:
      - name: rollouts-demo
        image: argoproj/rollouts-demo:blue
        imagePullPolicy: Always
        ports:
        - containerPort: 8080
  strategy:
    canary:
      steps:
      - setWeight: 20
      - pause: {}
      - setWeight: 40
      - pause: {duration: 40s}
      - setWeight: 60
      - pause: {duration: 20s}
      - setWeight: 80
      - pause: {duration: 20s}
```
