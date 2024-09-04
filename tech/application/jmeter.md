---
icon: monero
---

# Jmeter

해야 할 일&#x20;

<table><thead><tr><th width="187">이름</th><th>설명</th><th>비고</th></tr></thead><tbody><tr><td>Load Test</td><td>목표/예상 Request 테스트</td><td></td></tr><tr><td>Stress Test</td><td>최대 부하 테스트</td><td></td></tr><tr><td>Spike Test</td><td>일시적 부하 테스트 </td><td></td></tr><tr><td>Endurance Test</td><td>1일  이상 운영 테스트</td><td>목표 Request로 노출</td></tr></tbody></table>



## 설치

1. Jmeter 홈페이지 다운로드
2. Plugin 설치 ( https://jmeter-plugins.org/get/ )

### 맨날 헷갈리는 개념

⚠️ 주의 할 것

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption><p>Think Time (대기 시간)이 발생 할 수 있다.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption><p>TPS = 동시사용자/ (응답시간 + 대기시간)</p></figcaption></figure>

Ramp-Up Period :&#x20;

* 몇초 동안 나눠서 가상 사용자를 차례대로 생성할지 설정
* 정교하게 설정할 수 없음, 목표한 시간 이내에 설정한 Thread를 생성
* 정교하게 Thread을 생성하려면, Thread Group Plugin 필요

Loop Count

* Thread \* Loop  Count = 총 Request



## Load Test

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

Thread Group

* Number of Thread (Users) : 1000
* Ramp-up period (seconds) : 50&#x20;
* Loop count : 2
* Same user on each iteration  : 체크 안함
  * 동일한세션  사용자를 유지하여 사용하는 기능
* Specify Thread lifetime
  * Duration : 50
  * Startup deplay : 1

해석,&#x20;

* 사용자 수  : 1000명
* 실행 시간 : 50초
* 반복 수 : 2
* 1초 지연 시



## Endurance Test

* Add > Timer > Constant Timer





Ref

* [https://devmango.tistory.com/40](https://devmango.tistory.com/40)
* [https://sooo-9.tistory.com/34](https://sooo-9.tistory.com/34)
* [https://optimumbrew.com/api-load-testing-using-apache-jmeter/](https://optimumbrew.com/api-load-testing-using-apache-jmeter/)
* [https://search.shopping.naver.com/book/catalog/32441516840](https://search.shopping.naver.com/book/catalog/32441516840)

