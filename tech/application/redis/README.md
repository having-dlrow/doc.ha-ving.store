# ⛵ Redis

## Concept

* Redis는 <mark style="color:red;">RE</mark>mote <mark style="color:red;">DI</mark>ctionary <mark style="color:red;">S</mark>erver 의 약자입니다 .
* The open source, <mark style="color:red;">in-memory data store</mark> used by millions of developers as a <mark style="color:red;">database</mark>, <mark style="color:red;">cache</mark>, streaming engine, and message broker.

## 등장 배경

* RDBMS는 데이터의 양이 많을 수록 성능이 저하된다. (B트리의 한계)
* 단일 서버 구성에서,  결국 하드웨어가 중요해지는 한계를 해결하고자 한다.

## Redis 장점

* 다양한 자료 구조
* 영속성 지원
* Replication 지원
* client- Sharding 지원

## Redis 사용 전략 <a href="#redis-20-ec-a3-bc-ec-9a-94-20-ec-82-ac-ec-9a-a9-1" id="redis-20-ec-a3-bc-ec-9a-94-20-ec-82-ac-ec-9a-a9-1"></a>

* Cache 용도
  * look-aside : php -> cache -> db
  * write-back : cache -> 일정시간 batch -> db
* Cache 용도 외
  * 데이터  백업 전략 :  aof , rdb&#x20;

## Redis Engine

* [thread](thread/ "mention")
* [undefined.md](undefined.md "mention")

## Redis 백업 전략 <a href="#redis-eb-8a-94-20-ec-8b-b1-ea-b8-80-20-ec-8a-a4-eb-a0-88-eb-93-9c-ec-9d-b4-eb-8b-a4.-1" id="redis-eb-8a-94-20-ec-8b-b1-ea-b8-80-20-ec-8a-a4-eb-a0-88-eb-93-9c-ec-9d-b4-eb-8b-a4.-1"></a>







## Ref

* [\[우아한테크 세미나\] 우아한 레디스](https://www.youtube.com/watch?v=mPB2CZiAkKM)
