---
coverY: 0
---

# Istio

* [https://github.com/DickChesterwood/istio-fleetman](https://github.com/DickChesterwood/istio-fleetman) Kubernetes Istio : 완벽 실습 과정
* [https://fastcampus.co.kr/dev\_online\_devops\_kubernetes](https://fastcampus.co.kr/dev\_online\_devops\_kubernetes) 실무까지 한번에 끝내는 DevOps를 위한 Docker & Kubernetes

## istiod 구성요소

<figure><img src="../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

1. Kiali : 연결 관리 툴
2. <mark style="color:red;">Envoy</mark> : Proxy
3. Citadel :&#x20;
   * 서비스 사용을 위한 인증/인가 담당
   * TLS 통신 사용, Certification 관리
4. Gallery :&#x20;
   * 설정 관리
5. <mark style="color:red;">Pilot</mark> : Envoy 생명주기 담당 및 다른 인스턴스  정보 전달
   * Envoy Sidecar을 위한 Service Discovery 제공
   * Platform Adapter&#x20;
     * 새로운 인스턴스가 생성되면, Platform Adapter에게 알림
     * 그럼 envoy proxy 들에게 알림



### Istio Profile

* default
* demo

### Istio Operator

istio설정을 file로 관리하는 기능을 제공하고 있으며, 이것을 istio Operator라고 부릅니다.



Ref&#x20;

* [https://dramasamy.medium.com/life-of-a-packet-in-istio-part-1-8221971d77de](https://dramasamy.medium.com/life-of-a-packet-in-istio-part-1-8221971d77de)
*
