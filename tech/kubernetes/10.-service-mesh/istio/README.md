---
coverY: 0
---

# Istio

* [https://github.com/DickChesterwood/istio-fleetman](https://github.com/DickChesterwood/istio-fleetman) Kubernetes Istio : 완벽 실습 과정
* [https://fastcampus.co.kr/dev\_online\_devops\_kubernetes](https://fastcampus.co.kr/dev\_online\_devops\_kubernetes) 실무까지 한번에 끝내는 DevOps를 위한 Docker & Kubernetes

<figure><img src="../../../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

## Istio 기능

1. Service Discovery
2. Circuit Breaker
3. Load balancing
4. authenticating

## Istiod 구성요소

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (17) (1).png" alt=""><figcaption></figcaption></figure>

### <mark style="color:red;">Pilot</mark> :&#x20;

* Envoy Sidecar을 위한 **Service Discovery 역할**
* Envoy 생명주기 담당 및 다른 인스턴스  정보 전달
* Platform Adapter&#x20;
  * 새로운 인스턴스가 생성되면, Platform Adapter에게 알림
  * 그럼 envoy proxy들 에게 알림

### Mixer

* 액세스 제어 및 정책 관리
* 모니터링 지표 수집

### Gallery :&#x20;

* istio 설정 관리

### <mark style="color:red;">Citadel</mark> :&#x20;

* 서비스 사용을 위한 인증/인가 담당
* TLS 통신 사용, Certification 관리



### Istio Profile

* default
* demo

### Istio Operator

istio설정을 file로 관리하는 기능을 제공하고 있으며, 이것을 istio Operator라고 부릅니다.



요약

VirtualService 와 Destination Rule을 가지고, 트래픽이 어디로 갈지 조절하는 것이라고 생각하면됨





<figure><img src="../../../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

## Gateway 란?

* 라우팅 및 프로토콜 변환 담당
* 중개자 역할
* 공통 로직(인증) 처리를 하며, 이를 업스트림 서버로 넘겨준

### Gateway 처리 로직 ( Toss )

1. Request Mapping
2. Request Sanitize
3. Netflix Passport (토큰) 구조
4. API 데이터 복호화
5. 토큰 위변조 감지 ( Delayed Request Block, Replaying Attack Block )
6. mTLS API



## Istio 와 Eureka

1. istio의 virtualService는 Eureka에 등록되지 않는다.&#x20;
2. Eureka는 등록된 서비스를 기반으로 제공하고, istio는 네트워크 레벨에서 트래픽을 제어하게 된다.
3. 둘을 같이 사용할 수 있다. 서로가 영향을 주는 레벨이 다르다.

## Circuit Breaking&#x20;

1. istio
2. Resilience4J
3. Hystrix ( Client )



카나리 배포



Ref&#x20;

* [https://dramasamy.medium.com/life-of-a-packet-in-istio-part-1-8221971d77de](https://dramasamy.medium.com/life-of-a-packet-in-istio-part-1-8221971d77de)
* [https://lapee79.github.io/article/setup-a-production-ready-istio/](https://lapee79.github.io/article/setup-a-production-ready-istio/)
* [https://toss.tech/article/slash23-server](https://toss.tech/article/slash23-server)
* [https://www.freecodecamp.org/news/jhipster-microservices-with-istio-service-mesh-on-kubernetes-a7d0158ba9a3/](https://www.freecodecamp.org/news/jhipster-microservices-with-istio-service-mesh-on-kubernetes-a7d0158ba9a3/)
