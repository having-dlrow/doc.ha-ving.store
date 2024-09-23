# 설계 단계

## 도메인 모델링을 통한 마이크로 서비스 설계

### 도메인 모델 패턴

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th width="170"></th><th></th><th></th></tr></thead><tbody><tr><td>Entity</td><td>식ㅂㅕㅈ=값 객체</td><td><img src="../../.gitbook/assets/image (5).png" alt="" data-size="original"></td></tr><tr><td>Aggregate</td><td>엔티티와 값 객체의 묶음</td><td><img src="../../.gitbook/assets/image (4).png" alt="" data-size="original"></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>



### 마이크로 서비스 프로젝트 설계

1. **마이크로 서비스 아키텍터 설계**
   1. 쿼리 패턴
   2. <mark style="background-color:blue;">API 조합 패턴</mark>
   3. <mark style="background-color:blue;">CQRS 패턴</mark>
   4. <mark style="background-color:blue;">트랜잭션 관리 설계</mark>
   5. 서비스 간 통신 설계
   6. 서비스 매시 설계
2. 12 Factor 기반 개발
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
