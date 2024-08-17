# Controller



## #Controller

Kubernetes의 Kind 항목에 ReplicaSet, Deployment, Statefulset 같은 Resource가 정의 된다. ReplicaSet처럼 정의된 스펙에 따라 파드의 LifeCycle을 관리하는 것을 Controller라 한다.

## #Controller Manager

Kubernetes  마스터  노드에서만 동작되는 controller Manager 구성요소가 있다. 기본적으로 Kubernetes가 제공하는 ReplicaSet, statefulSet 같은 Controller 이외 Custom Controller를 정의하고, 이를 통해 특정기능이 추가 될 수 있도록 한다.

## #CodeGenerator

Kubernetes API에 사용되는 모든 객체는 Runtime.Object 인터페이스를 구현한다. 따라서 Resource 정의를 위해 Runtime.Object 인터페이스 구현이 필요하다. \
또한 Resource 배포/생성  과정에서, 객체를 복사하여 관리하기 때문에 정의한 객체에   대해 DeepCopy Function 구현이 필요하다.

## #Client-go

Kubernetes API와 상호작용을 위해 필요한 Client 라이브러리이다. Reflector(Lister), Informer, Indexer 구성요소에서 리소스 변화를 감지하는데 사용된다.

* Reflector : 목록 및 Watching 역할, 인스턴스 생성 알람을 받고, Delta Fifo Queue에 해당 Object 정보를 넣는다.
* Informer : Queue에 Object을 꺼내어 작업을 하는, controller 역할을 한다.
* Indexer : Thread Safe 하게 Data을 저장하는 역할을 한다.
