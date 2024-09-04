# Docker K8s

#### Docker는 언제 쓸까?

* 내 서버에 node.js가 있고, 서버에도 node.js가 있으니 내 서버에서 개발한 js파일을 서버에 배포하면 자동으로 동작하겠지? → 배포 → 에러 발생
  * 내 PC에서는 되는데 서버에 배포하니까 왜 안되는거지?
  * 서버와 내 PC의 node.js 버전이 안맞기 때문

#### Docker란?

* 컨테이너라고 불리는 하나의 작은 소프트웨어 유닛안에 어플리케이션, 환경 설정, 디펜던시, 그에 필요한 시스템 툴 등을 하나에 묶어서 다른 서버, 다른 PC, 그 어느곳에서도 쉽게 배포하고 안정적으로 구동할 수 있게 도와주는 툴

#### Docker vs VM

* VM : 하드웨어 위에 올라가는 vmware나 virtualbox와 같은 hypervisor을 이용해 독립적인 가상의 머신을 만들 수 있음
  * 다양한 OS위에서 구동하는 소프트웨어로, 각각의 VM에는 OS가 올라가기 때문에 굉장히 무겁고 느림
* Docker : 하드웨어에 설치된 운영체제에 Container Engine이라는 소프트웨어를 설치해 개별적인Container를 만들어 각각의 어플리케이션을 고립된 환경에서 구동할 수 있게 해줌
  * Container Engine = VM의 경량화 버전

#### K8S는 언제 쓸까?

* 아래와 같은 상황을 상상해보자
  * 어느 컨테이너에 쓸까? 리소스서버가 남아있나? 엇 이 컨테이너는 죽었네.. 다시 살려줘
* 도커의 사용이 대두화되면서, 컨테이너를 쉽게 관리하기 위한 툴의 필요성이 증가됨
* 이에따라 컨테이너를 쉽고 빠르게 배포, 확장, 관리해줄 수 있는 오픈소스플랫폼이 등장

#### K8S 특징

* Deployment, StatefulSets, DaemonSet, Job, CronJob 등 다양한 배포 방식을 지원
  * 여러 어플리케이션을 띄우고 싶은 경우엔 Deployment
  * 로그나 모니터링 등 모든 서버에 설치가 필요한 경우엔 DaemonSet
  * 배치성 작업은 Job이나 CronJob 이용
  * **결론적으로 모든 상황을 위해 모든 배치 시나리오를 준비**
* NameSpace & Label 지원

<figure><img src="../../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

* **Auto Scaling 지원**
  * 손쉽게 리소스 확장 가능

Ref&#x20;

* 도커 : [https://be-developer.tistory.com/18](https://be-developer.tistory.com/18) \
  쿠버네티스 : [https://velog.io/@holicme7/K8s-쿠버네티스란-무엇인가](https://velog.io/@holicme7/K8s-%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)
