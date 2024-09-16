# Virtual Cloud Networks (VCN)

Oracle 데이터 센터에 서버 자원들이 사용할 가상의 네트워크 환경을 구성하는 것이다.

* 네트워크 주소 할당
* 방화벽
* 라우팅 규칙
* 게이트웨이

작업이 해당한다.

VCN통해 구성할 수 있는 예시는 아래와 같다.

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

단일 Virtual Machine이 인터넷 게이트웨이를 통해 외부와 통신

**Public Subnet A**와 **Private Subnet B**로 나뉘어, Public Subnet A의 VM만 인터넷 게이트웨이를 통해 외부와 직접 연결되고, Private Subnet B의 VM은 외부 연결 없이 내부 통신만 수행



<figure><img src="../../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

**Public Load Balancer**가 있는 아키텍처입니다. 로드 밸런서는 가용 도메인 내의 여러 Fault Domain에 위치한 VM들에 트래픽을 분산시키며, 이는 고가용성을 위해 설계된 구조

**Load Balancer Subnet** 및 **Backend App Subnet** 보안 규칙 명명, 서브넷에 VM 위치

## **Load Balancer 생성**

1. OCI 콘솔에서 내비게이션 메뉴를 엽니다. **Networking** > **Load Balancers** 항목으로 이동합니다.
2. **Create Load Balancer** 클릭합니다.
3.  Load Balancer 를 타입으로 선정합니다.

    * **Load Balancer Type**: L7 로드밸런서로 HTTP Listener로 분배할때 사용합니다.
    * Network Load Balancer Type: L4 로드밸런서로 일반 IP, Port로 분배할때 사용합니다.

    ![image-20230509131145882](https://thekoguryo.github.io/oci/chapter10/images/image-20230509131145882.png)
