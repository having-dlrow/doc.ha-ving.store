# 설계 단계

## 의존리파지토엔티에그리게도메인 모델링을 통한 마이크로 서비스 설계

### 도메인 모델 패턴

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th width="130" align="center">구성 요소</th><th width="336" align="center">설명</th><th align="center">그림</th></tr></thead><tbody><tr><td align="center">티</td><td align="center">값 객체</td><td align="center"><img src="../../.gitbook/assets/image (5).png" alt="" data-size="original"></td></tr><tr><td align="center">애그리게잇</td><td align="center">엔티티와 값 객체의 묶음</td><td align="center"><img src="../../.gitbook/assets/image (4).png" alt="" data-size="original"></td></tr><tr><td align="center">리파지토리</td><td align="center">생성된 애그리게잇에대한 영속성관리 <br>애그리게잇에엔티티저장, 애그리게잇 업데이트 및 삭제 수행</td><td align="center"><img src="../../.gitbook/assets/image (1).png" alt="" data-size="original"></td></tr><tr><td align="center">도메인 이벤트</td><td align="center">도메인 이벤트를사용하여도메인내 변경의 파생 작업을명시적으로구현</td><td align="center"><img src="../../.gitbook/assets/image (1) (1).png" alt="" data-size="original"></td></tr></tbody></table>



### 마이크로 서비스 아키텍처설계

<table><thead><tr><th width="197">패턴 이름</th><th></th></tr></thead><tbody><tr><td>쿼리 패턴</td><td></td></tr><tr><td><mark style="background-color:blue;">API 조합 패턴</mark></td><td>DB 조인을 대신하여,  API 조합기 처리</td></tr><tr><td><mark style="background-color:blue;">CQRS 패턴</mark></td><td>Command Query Responsibility Segregation : 명령 조회 책임 분리<br>- 데이터 시차 발생<br>- 복잡한 쿼리처리를 위한 별도 마이크로서비스 구현</td></tr><tr><td><mark style="background-color:blue;">트랜잭션 관리 설계</mark></td><td><a data-mention href="../../tech/microservice/pattern/transaction/saga-pattern.md">saga-pattern.md</a></td></tr><tr><td>서비스 간 통신 설계</td><td>동기식 통신, 비동기 통신</td></tr><tr><td>서비스 매시 설계</td><td></td></tr></tbody></table>

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

1. 12 Factor 기반 개발

<table><thead><tr><th width="187">원칙</th><th width="96">구분</th><th></th></tr></thead><tbody><tr><td>코드 베이스</td><td>CI/CD</td><td><img src="../../.gitbook/assets/image (58).png" alt="" data-size="original"></td></tr><tr><td>의존성</td><td>CI/CD</td><td><img src="../../.gitbook/assets/image (57).png" alt="" data-size="original"></td></tr><tr><td>설정</td><td>배포</td><td><img src="../../.gitbook/assets/image (56).png" alt="" data-size="original"></td></tr><tr><td>백엔드 서비스</td><td>배포</td><td>-</td></tr><tr><td>빌드/배포/실행</td><td>CI/CD</td><td>-</td></tr><tr><td>stateless</td><td>배포</td><td><img src="../../.gitbook/assets/image (59).png" alt="" data-size="original"></td></tr><tr><td>포트 바인딩</td><td>배포</td><td>-</td></tr><tr><td>동시성</td><td>운영</td><td><img src="../../.gitbook/assets/image (60).png" alt="" data-size="original"></td></tr><tr><td>폐기 가능</td><td>운영</td><td>graceful shutdown</td></tr><tr><td>개발/운영환경 일치</td><td>배포</td><td>개발 환경 = Production 환경</td></tr><tr><td>로그</td><td>운영</td><td>ELK</td></tr><tr><td>운영관리 프로세스</td><td>운영</td><td>DB  백업/복구, 스크립트 실행 분리</td></tr></tbody></table>
