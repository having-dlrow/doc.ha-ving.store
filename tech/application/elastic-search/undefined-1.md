# 구성요소

기본 용어&#x20;

1. 인덱스 : 데이터가 토큰화 되어 저장된 자료구조

<div align="left">

<figure><img src="../../../.gitbook/assets/image (42).png" alt="" width="286"><figcaption></figcaption></figure>

</div>

:white\_check\_mark: indices : 매핑 정보를 저장하는 논리적인 데이터 공간 ( index vs indices )

:white\_check\_mark: <mark style="color:red;">Term</mark> : 필드 내 데이터의 단위로, Elasticsearch에 색인되고 검색 할 단어 저장

<table><thead><tr><th width="136">RDS</th><th width="155">ElasticSearch</th><th>Description</th></tr></thead><tbody><tr><td>테이블</td><td>인덱스(index)</td><td>데이터가 토큰화 되어 저장된 자료구조</td></tr><tr><td>한행</td><td>문서</td><td>인덱스 내에 JSON 형식의 데이터 기본 단위</td></tr><tr><td>컬럼</td><td>필드</td><td>각 문서는 데이터 속성이나 특성을 나타내는 필드로 구성</td></tr><tr><td>물리파티션</td><td>샤드</td><td></td></tr><tr><td>스키마</td><td>매핑(mapping)</td><td></td></tr></tbody></table>

특징

1. Schemaless :&#x20;



노드 종류

1. 마스터 노드&#x20;
   1. 클러스터 인덱스 생성/삭제/샤드 분배 결정을 내림
2. 데이터 노드
   1. 색인, 검색, 집계 담당
   2. CPU, I/O, 메모리 소모가 많음
   3. 데이터노드종류
      1. data\_content : 지속적 유지 데이터
      2. data\_hot : 최근 데이터
      3. data\_warm : 빈도 낮은 데이터
      4. data\_cold : 오래된 데이터
      5. data\_frozen : 아카이브 데이터 ( s3 )
3. 코디네이팅 노드
   1. 클러스터의 요청을 라우팅
4. 인제스트 노드
   1. 데이터 수집, 가공 및 색인 전달 과정
   2. 데이터 전처리 ( 필터링, 변환 ) 가공
   3. 데이터 노드와 동일 구성 = 효율성, 데이터 노드와 별도 구성 = 처리과정이 높은(리소스) 많은 경우
5. 머신러닝 노드
   1. 머신러닝 기능을 제공, 데이터학습
6. 리모트 클러스터 클라이언트
   1. 여러 클러스터 간의 데이터 검색이 가능하게 담당
7. Transform 노드
   1. 인덱스 간 데이터를 자동으로 복사하거나 변환 하는 역할을 수행
