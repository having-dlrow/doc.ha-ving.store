---
icon: face-icicles
---

# PART 1 - 발주자 안내서

1. 클라우드 네이티브 개요
   1. 클라우드 네이티브 정의
   2. <mark style="background-color:blue;">클라우드 어플리케이션 성숙도 단계</mark>
   3. 클라우드 네이티브 구성요소
   4. <mark style="background-color:blue;">클라우드 네이티브 특장점</mark>
2. 도입 필요성
3. 구성 요소 및 원칙
   1. 마이크로 서비스
   2. 컨테이너
   3. 데브옵스
   4. CI/CD
   5. 애자일
   6. 12 Factor
   7. <mark style="background-color:blue;">클라우드 네이티브 어플리케이션 아키텍처</mark>
4. 도입 적합성 검토
   1. 적합성검토 체크리스트
      1. 검토 항목 도출
   2. 적합성검토 수행
      1. 적합성 검토 후, 도입 여부 결정
      2. 도입 우선 순위 결정
5. 구축사업 추진시 고려사항
   1. 사업 관리 고려사항
      1. 관리 프로세스
      2. 발주자 업무&#x20;
   2. 사업 계획서 및 제안 요청서 작성
      1. 사업 범위 작성
      2. 상세 요구사항 작성
   3. 개발비 산정
      1. 개발비 구성 요소
      2. 기능식별방식
   4. 데브옵스 조직 고려 사항

***

## 클라우드 네이티브 정의

* <mark style="background-color:yellow;">클라우드 네이티브 환경에서 개발, 실행되는 애플리케이션</mark>
* 프라이빗, 퍼블릭 및 하이브리드 클라우드 환경 전체에 지속적인 개발과 자동화된 관리 환경을 제공하기 위해 설계된 애플리케이션이다.
* 클라우드 내에서 확장이 가능하고, 어떤 클라우드 환경에도 이식이 가능하다.

## 클라우드 어플리케이션 성숙도 단계

* Level 0 : 기존 환경
* Level 1 : 클라우드 준비
* Level 2 : 클라우드 친화 단계
* **Level 3 : 클라우드 네이티브 단계**

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

## 클라우드 네이티브 특장점

<table><thead><tr><th width="155" align="center"> 구성 요소</th><th align="center">주요 특징</th></tr></thead><tbody><tr><td align="center">Micro Service</td><td align="center"><ul><li>소규모 서비스</li><li>독립 서비스 운영</li><li>다양한 언어/기술 적용 (Polyglot)</li><li>유지보수 용이성</li></ul></td></tr><tr><td align="center">Container</td><td align="center"><ul><li>효율적 개발환경 구축</li><li>경량화</li><li>높은 이식성</li><li>확장성</li></ul></td></tr><tr><td align="center">DevOps</td><td align="center"><ul><li>서비스 단위 개발/운영 협업</li><li>신속한 서비스 개발 및 배포</li></ul></td></tr><tr><td align="center">CI/CD</td><td align="center"><ul><li>프로세스 자동화</li><li>소규모 배포</li></ul></td></tr></tbody></table>

## 클라우드 네이티브 어플리케이션 아키텍처
