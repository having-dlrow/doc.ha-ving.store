# 🦄 MicroService

## Goal

* 도메인별 서비스와 배포/모니터링을 분리하자.
* 내부 서비스  통신은 gRPC를 이용해 통신 오버헤드를 줄이고 싶다.
* Event Driven 구조를 구축하자.
* Scheduele Worker 구조를 만들자.

## 원칙

* Goal Oriented Service
* Front Door API
* <mark style="color:red;">Independently Testable</mark>
* Loosely coupled ( 느슨한 결합 )
* 높은 테스트와 자동화 수준

## 어려운 점

* Transaction :  ~~P2C~~ , Saga Pattern
* Data
* Event
* API 조합 & Query : A 서비스 성공 데이터 left Join 계좌 조회 성공 데이터

## 고려사항

* 서버 자원이 그 무엇보다 중요하다면 MSA를 도입하면 안 된다.
* 그렇다면 ? 누가 해야하는가?
  * 안정성을 원하는 서비스
  * 업무 효율을 높이고 싶은 서비스
  * 돈은 써도 되는 서비스
