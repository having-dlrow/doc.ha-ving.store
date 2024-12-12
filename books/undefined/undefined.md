---
description: >-
  https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART002796829
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 마이크로서비스 아키텍처 기반 애플리케이션 프레임워크 구현 및 평가



논문 게시일 : 2024.12

***

\[ 요약 ]

### 1 모놀리틱 방식의 아키텍처 한계

* 기존 단일구조, 대규모 & 복잡한 구조 구현이 힘듦

### 2.1 마이크로서비스 아키텍처

* 분산 환경
  * <mark style="background-color:blue;">신뢰적 통신</mark>
  * <mark style="background-color:blue;">가용성</mark>
* 효율적 개발 패턴 및 빌드/배포

### 2.2 마이크로서비스 아키텍처 특성

1. 서비스 중심 :  도메인기반(기능단위) 분할
2. 경량화&#x20;
3. Polyglot (다국어) : 다양한 언어 사용 가능 ( eg. A서비스-Spring, B서비스-PHP )
4. 자동화

2.3 연구 필요성 및 방법

1. ATAM 활용, RISK 도출
2. RISK와 Tradeoff point를 고려하여 대안

### 3. 마이크로 아키텍트 평가

<div align="left"><figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure></div>

#### 3.1 마이크로 아키텍트 구성 정의

1. Config Server
2. Eureka
3. API Gateway

3.2 서비스 요구사항 정의

<div align="left"><figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure></div>

1. 사원 정보를 생성/수정/삭제 API
2. JSON 응답
3. 객체 기반 Dao 생성
4. 모듈별 Docker 빌드, 하나의 서버에 배포

3.3 ATAM 평가 방법

<div align="left"><figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>ATAM Evaluation Procedure</p></figcaption></figure></div>

ATAM은 품질 속성 요구사항과 비지니스 목표달성을 위한 Architecture 결정 사항을 평가

ATAM은 시나리오 중심으로 <mark style="background-color:orange;">품질 속성 요구사항(Quality Attributes Utility Tree) 도출</mark>

Architecture가 특정 품질 속성을 만족하는지 분석

다양한 이해관계자와 Risk, Sensitivity, TradeOff 분석



### 4. 마이크로 서비스 아키텍처 프레임워크

4.1 프레임워크 품질 속성 요구사항

1. <mark style="background-color:blue;">데이터 통신 기반, 신뢰성 확보 필요</mark>
2. <mark style="background-color:blue;">인프라 가용성 확보 필요</mark>

위험에 대응하기 위한 프레임워크의 기능 평가

<table><thead><tr><th width="128">속성</th><th width="395">설명</th><th width="90">중요성</th><th>어려움</th></tr></thead><tbody><tr><td>신뢰성</td><td>오류처리, 재처리, 동기/비동기 통신</td><td>높음</td><td>높음</td></tr><tr><td>재사용성</td><td>재사용</td><td>높음</td><td>높음</td></tr><tr><td>가용성</td><td>시스템 가용성 보장</td><td>높음</td><td>중간</td></tr><tr><td>수정가능성</td><td>업무 프로세스 및 룰 변경에 따른 유연성</td><td>높음</td><td>중간</td></tr><tr><td>성능</td><td>목표 동시 접속자 대응 성</td><td>중간</td><td>중간</td></tr><tr><td>유지성</td><td>운영관리 용이성</td><td>중간</td><td>중간</td></tr></tbody></table>



ATAM 평가 결과

<table><thead><tr><th width="102">분석</th><th width="76">구분</th><th width="278">Risk 설명</th><th>Framework Function</th></tr></thead><tbody><tr><td>위험</td><td>MSA</td><td>마이크로 서비스 간 <mark style="background-color:blue;"><strong>통신 실패</strong></mark>, 전체 서비스 장애 발생 가능</td><td>MQ 이벤트 기반 통신</td></tr><tr><td>위험</td><td>MSA</td><td>마이크로 서비스 실패, 전체 서비스 장애 발생 가능</td><td>Eureka 기반 health 모니터링<br>서비스 이중화</td></tr><tr><td>위험</td><td>MSA</td><td>다수의 인프라 관리의 어려움 (eg.  서비스/배포인프라/개발도구 )</td><td>Kubernetes Orchestration 활용</td></tr><tr><td>Sensitivity Point</td><td>MSA</td><td>마이크로 서비스의 수가 증가함에 따라, 전반적 성능 저하</td><td></td></tr></tbody></table>

