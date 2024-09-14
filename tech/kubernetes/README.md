# 🐳 Kubernetes

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 설계원칙

1. 쿠버네티스 API는 선언적이어야 한다. ( 명령형 보다)
   1. 원하는 상태를 정의
2. 제어판은 투명해야 한다. 숨겨진 API는 없다.
   1. kube api server  -> "  새 파드 생성해!" -> scheduler
   2. scheduler -> \[ 최적의 노드를 결정 ]&#x20;
3. 사용자가 있는 곳에서 사용자를 만나야 한다.
4. 다양한 클러스터 간에 이식 가능해야 한다.

## 구성요소소

### Master Node

* Kube-api server : kubelet이 해석한 내용을 통해, API 요청을 처리한다.
* Kube-scheduler : 파드 할당 스케줄
* Kube-controller-manager : ReplicaSet, Deployment, Statefulset 관리, 확장, 상태 관리
* etcd : cluster 상태 설정

### Slave Node

* Kube-proxy : Service 에 속한 Pod에게 트래픽을 라우팅한다.



### Replicaset 생성 Flow

`kubectl apply -f replicaset.yaml`&#x20;

1. kubectl :  yaml 해석 및  kube-api 전송
2. kube-api :  `Replicaset` 생성
   1. etcd 생성 상태 저장
   2. kube-api Pod 생성
3. kube-schedule :  etcd 변경 감지,  Pod 할당할 노드 지정
4. kube-controller-manager : etcd 설정값을 기반으로 관리
   1. Replicaset Pod가 지정된 수로 실행되는지
   2. 노드상태가 안좋아 노드를 변경해야하는것은 아닌지
   3. Pod 재시작 해야하면 Rollback 전략 실행
   4. Service 네트워크 연결이 되었는지 확인



### Pod Network Flow

> * Kubernetes Calico 네트워크를 설정한다.
> * Ingress는 Loadbalancer 타입으로 지정하였으며,  'myapp' Service로 연결한다.
> * Pod는 `10.0.1.2` 이며, Slave 노드에 할당 되었다.
> * Master 노드는 `192.168.56.100`  이다.

1. 클라이언트가  `222.111.10.2(마스터 노드)`로 요청 전송
2. `Ingress Controller`  가 External-IP 을 통해 들어온 요청을 'myapp'에 전달한다.&#x20;
3. calico 는 내부 트래픽을 관리한다. 'myapp' 서비스에서 slave노드로 트래픽을 전달한다.
4. Slave 노드의kube-proxy는 'myapp'에 속한 Pod로  전달한다.
5. Pod의 응답데이터는 kube-proxy을 거쳐 'myapp'에 반환되고, Ingress controller을 거쳐 전송된다.
