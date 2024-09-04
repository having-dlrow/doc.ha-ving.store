# ☁️ Cloud Foundry

## Concept

{% embed url="https://docs.cloudfoundry.org/concepts/architecture/" %}

<figure><img src="../../../.gitbook/assets/image (19) (1).png" alt=""><figcaption><p>@copyright. cloudfoudnry.org</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (20) (1).png" alt="" width="563"><figcaption><p>Deigo architecture</p></figcaption></figure>

<table><thead><tr><th width="178">컴포넌트</th><th width="270">역할</th><th>특징</th></tr></thead><tbody><tr><td>Gorouter</td><td>외부 요청 라우팅 및 로드 밸런싱</td><td>HTTP 트래픽 관리, 다양한 애플리케이션에 대한 동적 라우팅 제공</td></tr><tr><td>UAA</td><td>사용자 인증 및 권한 부여</td><td>OAuth2 프로토콜 지원, 시스템 보안 및 사용자 관리 담당</td></tr><tr><td>Cloud Controller</td><td>애플리케이션 수명 주기 관리 <br>(배포, 업데이트, 삭제 등)</td><td>REST API를 제공, 애플리케이션 관리 중앙 집중식 처리</td></tr><tr><td>Diego</td><td>애플리케이션 컨테이너 오케스트레이션</td><td>애플리케이션 실행 환경 제공, 확장성 및 고가용성 보장</td></tr><tr><td>Blobstore</td><td>애플리케이션 코드, 빌드팩, 도커 이미지 등의 저장소</td><td>파일 저장 및 접근 관리, 데이터 영속성 제공</td></tr><tr><td>Service Broker</td><td>외부 서비스와의 통합 관리</td><td>다양한 서비스(데이터베이스, 메시징 시스템 등) 제공 및 관리</td></tr><tr><td>Loggregator</td><td>로그 및 메트릭 수집 및 전달</td><td>실시간 로그 스트리밍, 시스템 모니터링 및 분석 지원</td></tr></tbody></table>

<details>

<summary>Bosh</summary>

배포, 업데이트를 포함한 전 라이프사이클을 관리하는 CF CLI 도구

"CF push" 명령어를 사용하여, CF API을 통해, 최종 수행될 CFAR(Cloud Foundry Application Runtime) 이미지가 생성되며, 이를 Diego에 의해 지정된 VM에서 실행된다.

</details>

## CF가 쿠버네티스와 호환되기 위해선 최소한 두 가지 조건

1. Kubernetes 호환 컨테이너 이미지가 생성되어야 한다
2. 이미지가 Kubernetes Cluster에 배포 할 수 있어야한다

### Kubo

CFAR이 아니라, CFCR (CloudFoundry Container Runtime)을 생성, 이를 쿠버네티스 클러스터에 배포.

### Quark

CFAR을 Docker 컨테이너 이미지로 패키징하는 방법, 이를 Kubernetes에 적용가능하다.



## Scheduling은 누가하는가?

기존 VM 스케줄링을 담당하던 Diego을 대체해야, Kubernetes 컨테이너 라이프사이클 관리가 가능하다

### Eirini (에이리니)

쿠버네티스 컨테이너 이미지로 패키징된 CF 애플리케이션을 쿠버네티스 클러스터에서 실행시키는 역할을 담당한다



## Cloud Foundry Incubating Project

#### KubeCF

CF 호환성을 위해 기존 컴포넌트들을 최대한 유지하며 쿠버네티스 네이티브에 가깝게 가고 있는 방향

#### CF-for-k8s

쿠버네티스 네이티브를 표방하며 최소한의 CF 호환성을 유지

### :white\_check\_mark: Korifi

{% embed url="https://github.com/cloudfoundry/korifi/" %}

* 기존 CF의 라우팅 컴포넌트(gorouter)가 이스티오(Istio)로 대체되었다.
* CF의 패키지 빌드 컴포넌트도 kpack으로 교체되었다. kpack으로 생성된 이미지는 에이리니를 통해 쿠버네티스 클러스터에 배포된다.



Ref.

* [https://materialplus.srijan.net/resources/getting-started-with-korifi-cloud-foundry-a-comprehensive-guide](https://materialplus.srijan.net/resources/getting-started-with-korifi-cloud-foundry-a-comprehensive-guide)
* [\[2021-05\] 디지털서비스 이슈리포트 01 쿠버네티스를 품은 클라우드 파운드리의 미래](https://www.digitalmarket.kr/web/board/BD\_board.view.do?domainCd=2\&bbsCd=1030\&bbscttSeq=20210528180441332\&monarea=00008)
