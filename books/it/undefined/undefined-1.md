# 식별 관계

## 개념

1. RDBMS 테이블간의 관계 설정
2. 외래키를 이용한 Join 방법

## 식별 관계

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 자식 테이블의 기본키 =   부모 테이블 기본키 +   기본키
2. 부모테이블의 데이터가 존재해야 입력 가능하다.



## 비식별 관계

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 자식 테이블의 기본키 = 기본키
2. 부모 기본키는 FK로 등록
3. 부모 데이터가 없어도 독립적 생성 가능
