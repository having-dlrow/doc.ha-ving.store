# Docker

\[문제] Docker 개념을 설명해주세요. 가상화 개념을 설명해주세요.



### 컨테이너란

프로그래밍 언어 런타임 및 라이브러리와 같은 종속 항목(코드 및 라이브러리)들의 집합. 경량 패키지

각각의 application을 컨테이너라고 하며, 특정 호스트 OS위에서 동작하도록 구성한다.

### 도커란

1. 환경에 구애 받지 않는다.
2. 어플리케이션을 이미지화 하여, 빠르고 가볍게 구동할 수 있다.

#### 용어

* `도커 컨테이너` : 도커 이미지가 실행되는 가상화 공간을 말한다.
* 도커 컨테이너들을 클러스터 이룬것을 **`도커 swarm`** 이라고 한다

### 도커 구조

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. **도커 엔진** (도커 서버) : 도커의 CLI 명령어를 해석한다.
2. **Containerd**
   1. 도커가 처음 나올 때, Monolithic 하게 출시함 ( Api + CLI + 스토리지 )
   2. 추후 표준화 작업을 진행( OCI프로젝트 )
   3. OCI 표준을 준수한 Container Runtime을 만듦 ( Docker Engine(Monolithic 아키텍처) 에서 분리 시킴 )
   4. 도커 입장에서 인터페이스 구현한 Container Runtime 이름이 Containerd (참고 Kubernetes 진영에서 구현한 Container Runtime 이름이 CRI-O )

## 도커 이미지 구조

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 레이어로 이루어진다.
2. base layer에 Linux boot filesystem 이미지를 두고 시작한다. ( bootfs )
3. 그다음 layer에 root filesystem, OS을 설치한다. ( rootfs )
4. 도커는 `union mount` 기법으로 하나의 파일 시스템으로 보이도록 한다.

`union mount` : 여러 개의 파일 시스템을 mount 하되, 하나의 파일 시스템으로 mount 된 것처럼 하는 방법



* [https://rampart81.github.io/post/docker\_ima](https://rampart81.github.io/post/docker\_image/)&#x20;
* [들리는 도커(Docker)의 위상 - OCI와 CRI 중심으로 재편되는 컨테이너 생태계](https://www.samsungsds.com/kr/insights/docker.html)
