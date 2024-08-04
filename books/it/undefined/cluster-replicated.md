# Cluster , Replicated

#### 레플리케이션

* 특징
  * 클러스터링을 보완하기 위해 나타난 개념
  * 유저가 마스터 DB 서버에 DML(Select, Insert, Update, Delete) 작업을 진행하면 Master DB는 그 데이터를 Slave DB에 복제
  * 일반적으로 Select는 Slave DB에서, Insert, Update, Delete는 Master DB에서 진행
* 장점
  * 양쪽 DB에 역할을 분산하기 때문에, READ의 성능을 향상시킬 수 있음
* 단점
  * 만약 테이블 자체에 데이터가 엄청나서 Slave DB 서버를 N대 늘려도 원하는 데이터를 테이블에서 찾는데 많은 시간이 걸릴 수 있음

#### 클러스터링

* 특징
  * 동일한 DB 서버 2개를 묶고, 두 DB 서버를 active - active 상태로 운영하면 하나의 DB 서버가 죽더라도 나머지 DB 서버는 살아있기 때문에 정상적으로 서비스가 가능
* 장점
  * 하나의 DB 서버가 부담하던 부하를 두 개의 DB에 나눠서 감당하므로 CPU, Memory 관리에 효율적
* 단점
  * DB 스토리지를 두 DB서버가 공유하기 때문에 병목현상이 발생할 수 있음
    * 이를 해결하기 위해 두 DB중 한 대는 Stand-by, 즉, 대기 상태로 두고, Active DB에 이슈가 발생할 경우 Fail Over(시스템 대체 작동)를 통해 두 서버가 Active ↔ Stand-by 상태를 상호 전홤하에 따라 장애를 대응
    * 단, Fail Over 역시 수초 \~ 수분 간의 시간동안 영업 손실이 발생할 수 있음
  * DB를 1개만 사용하는 것 보다는 2대 이상 운용에 더 많은 비용이 발생

