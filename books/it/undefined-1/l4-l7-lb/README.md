# L4, L7 LB

\[ 문제 ]

* L4 스위치와 L7 스위치, 그리고 Nginx의 로드 밸런싱 역할
  * 무중단 배포 시나리오와 함께 공부하면 좋을것 같습니다.
  * 대표적으로 롤링 배포 시나리오는 아래와 같습니다.
  *

      <figure><img src="../../../../.gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure>

\[ 정답 ]

#### L4

* OSI 7계층 중 4번째 레이어(Transport)에 해당
  * IP와 Port같은 데이터는 포함하지만 URL같은 데이터는 식별 불가능
  * 따라서 IP, Port를 기준으로 로드 밸런싱
* TCP, UDP와 같은 프로토콜에 대한 책임이 있음
* ex ) 한 대의 서버에 각기 다른 포트 번호를 부여하여 다수의 서버 프로그램을 운영하는 경우

#### L7

* OSI 7계층 중 7번째 레이어(Application)에 해당
  * 7계층이라 모든 계층을 포함
  * IP, Port를 비롯하여 URL도 식별 + 로드 밸런싱 가능
* HTTP, HTTPS와 같은 프로토콜에 대한 책임이 있음

#### Nginx

* OSI 계층 중 4번째, 7번째 레이어 모두 위에서 동작 가능
* 때문에 UDP, TCP, HTTP, HTTPS와 같은 프로토콜에 책임이 있음



Ref

* [https://velog.io/@znftm97/무중단-배포를-위한-환경-이해하기](https://velog.io/@znftm97/%EB%AC%B4%EC%A4%91%EB%8B%A8-%EB%B0%B0%ED%8F%AC%EB%A5%BC-%EC%9C%84%ED%95%9C-%ED%99%98%EA%B2%BD-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
