# ⭐ PART 2 - 개발자 안내서

## 안내서 목차

1. 개발 절차
   1. 단계 별 개발 절차
2. 분석 단계
   1. **마이크로 서비스 도출**
      1. 도메인 주도 설계를 통한 마이크로 서비스 도출&#x20;
      2. 이벤트스토밍을 통한 마이크로 서비스 도출
      3. 업무긴으 분해를 통한 마이크로 서비스 도출
   2. 아키텍처 설계
      1. 아키텍처 구성
         1. API Gateway
         2. 서비스 메시
         3. 런타임 플랫폼
         4. CI/CD
         5. 백엔드 서비스
         6. 모니터링
3. 설계 단계
   1. 도메인 모델링을 통한 마이크로 서비스 설계
      1. 도메인모델 패턴
      2. 마이크로 서비스 프로젝트 설계
   2. **마이크로 서비스 아키텍터 설계**
      1. 쿼리 패턴
      2. <mark style="background-color:blue;">API 조합 패턴</mark>
      3. <mark style="background-color:blue;">CQRS 패턴</mark>
      4. <mark style="background-color:blue;">트랜잭션 관리 설계</mark>
      5. 서비스 간 통신 설계
      6. 서비스 매시 설계
   3. 12 Factor 기반 개발
      1. 코드 베이스
      2. 종속성
      3. 설정
      4. 백엔드 서비스
      5. 빌드/릴리즈/실행환경
      6. 무상태 서비스
      7. 포트 바인딩
      8. 동시성
      9. 폐기 가능성
      10. 개발/운영환경 일치
      11. 로그
      12. 관리 프로세스
   4. 운영 단계
      1. 스프링 부트 기반 마이크로 서비스 개발
         1. 카탈로그 서비스 개발
         2. 고객 서비스 개발
         3. 카탈로그 와 고객 서비스 연동 및 테스트
      2. 스프링 클라우드 기반 마이크로 서비스 구축
         1. Hystrix ( 서킷 브레이커 )
         2. Ribbon ( 로드밸런서 )
         3. Eureka ( 서비스 등록 )
         4. Zuul (게이트 웨이)
         5. Config Server ( Config )
         6. Cloud Bus ( Bus )
         7. Polyglot ( Sidecar )
         8. ELK ( 로깅 )
         9. Prometheus (모니터링/매트릭)
         10. Jaeger, Zipkin ( Tracing )
      3. 빌드/배포
         1. 도커 배포
         2. 쿠버네티스 배포

## 안내서 내용&#x20;

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### 마이크로 서비스 도출

#### 도출 방안 유형

1. DDD (도메인 주도 설계) : 업무단위(도메인)을 식별
2. Event Storming (이벤트 스토밍) : 이해관계자가 모여, DDD 식별 후 브레인  스토밍 하며 도출
3. Process Modeling (업무 기능 분해) : 경험적으로, 업무 단위로 분해

#### 마이크로 서비스 도출 절차

1. **유비쿼터스 언어 정의**
   1. 도메인 전문가, 사용자, 분석가, 개발자 등 참여자간의 공통된 언어 정의
   2. Wiki 형태로 용어 사전 작성
2. 비지니스 핵심이 되는 개념 식별, 분석 하여 **바운디드 컨텍스트 식별**
3. 컨텍스트간 관계를 통해 **컨텍스트 맵 작성**
4. 분할/분석 결과를 통해, 서비스 분할 검토
5. 마이크로 서비스 도출

### 아키텍처 설계

<figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

#### API Gateway

역할 :&#x20;

1. 인증 인가
2. 요청 라우팅
3. 프로토콜 변환
4. 로드 밸런싱
5. 오케스트레이션
6. 서비스 디스커버리

Spring Cloud Gateway vs Netflix Zuul :&#x20;

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Router (라우터) : URI 식별

Predicate (조건자) : HTTP 헤더/입력값 정의 기준 validate

Filter (필터) : HTTP 요청 수정

<table><thead><tr><th width="190">구분</th><th>Spring Cloud Gateway</th><th>Zuul (Netflix OSS)</th></tr></thead><tbody><tr><td>동작 방식</td><td><ul><li>Non-Blocking</li></ul></td><td><ul><li>Blocking</li></ul></td></tr><tr><td>동작 원리</td><td><ul><li>Filter</li></ul></td><td><ul><li>Predicates</li><li>Filter</li></ul></td></tr><tr><td>서버</td><td><ul><li>Tomcat</li></ul></td><td><ul><li>Netty</li></ul></td></tr></tbody></table>

그 외&#x20;

* Kong

#### Service Mesh

|     Mesh-Native Code    |  Mesh-Aware Code |   Mesh-Agnostic Code  |
| :---------------------: | :--------------: | :-------------------: |
|     3rd Party 서비스 이용    |      API 형태      | side car proxy 형태로 이용 |
| ex) Micro Azure Service | ex) Spring Cloud |       ex) istio       |

#### Gateway vs Service Mesh

<table><thead><tr><th width="148">구분</th><th>API Gateway</th><th>Service Mesah</th></tr></thead><tbody><tr><td>위치</td><td>외부망과 내부망 사이</td><td>내부망(쿠버네티스 클러스터)</td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>
