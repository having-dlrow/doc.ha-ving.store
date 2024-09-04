# 트랜잭션 격리 레벨

\[ 문제 ]

* MySQL을 주로 사용하셨다고 했는데, 트랜잭션의 격리 수준에 대해 설명해주세요.

\[ 정답 ]

참고자료에 언급된 블로그의 예시 설명과 함께보셔야 이해가 잘됩니다.

*   해설

    * 트랜잭션의 격리수준 (Isolation Level)
      * 동시에 여러 트랜잭션이 처리될 때, 트랜잭션끼리 얼마나 격리되어 있는지를 나타내는 것
    * 격리 레벨 종류
      * READ UNCOMMITTED (커밋되지 않은 읽기)
        * 커밋되지 않은 수정된 데이터를 다른 트랜잭션에서도 볼 수 있음
          * 모든 부정합 문제 발생 (DIRTY READ, NON-REPETABLE-READ, PHANTOM READ)
      * **READ COMMITTED** (커밋된 읽기)
        * 기본 설정인 DB : postgreSQL, oracleDB
        * COMMIT이 완료된 데이터만 조회 가능한 격리 수준
          * NON-REPETABLE-READ 발생
          * PHANTOM READ 발생
      * REPETABLE READ (반복 가능한 읽기)
        * 기본 설정인 DB : MySQL
        * 자신보다 낮은 트랜잭션 번호를 갖는 트랜잭션에서 커밋한 데이터만 읽을 수 있음
          * PHANTOM READ 발생 (MySQL의 InnoDB에서는 PHANTOM READ 발생X)
            * 언급했다시피 MySQL에서는 보통 발생하진 않고, OracleDB에서는 발생
      * SERIALIZABLE (직렬화 가능)
        * 데이터의 무결성과 정합성이 중요할때 사용 (ex : 금융)
        * 한 트랜잭션을 다른 트랜잭션으로부터 완전히 분리하는 격리 수준
        * 모든 부정합 문제 해결, BUT 트랜잭션이 순차적으로 처리되어야해서 동시 처리 불가능
    * 부정합의 종류
    *

        <figure><img src="../../../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

        * DIRTY READ : 한 트랜잭션에서 처리한 작업이 완료되지 않았음에도 불구하고 다른 트랜잭션에서 볼수있게 되는 현상
        * NON - REPETABLE READ : 하나의 트랜잭션 내에서 동일한 SELECT 쿼리를 실행했을 때 항상 같은 결과를 보장해야한다는 REPETABLE 정합성에 어긋남을 뜻함
          * 오늘 입금된 총 합을 계산하는 A 트랜잭션에서, 다른 트랜잭션이 계속 입금 내용을 커밋하는 상황이라면 SELECT 할때마다 값이 달라지는 현상 발생
        * PHANTOM READ : `SELECT … FOR UPDATE` 쿼리와 같은 베타적 잠금(비관적 잠금, 쓰기 잠금)을 거는 경우, 언두 로그가 아닌 테이블 레코드를 그대로 조회하게 되어, 다른 트랜잭션에서 수행한 변경 작업에 의해 레코드가 보였다가 안 보였다가 하는 현상이 발생

    #### SpringBoot에서 트랜잭션 격리레벨 적용

    ```java
    import org.springframework.transaction.annotation.Isolation;
    import org.springframework.transaction.annotation.Transactional;

    @Transactional(isolation = Isolation.READ_UNCOMMITTED)
    public void readUncommittedTransaction() {
        // Your code here
    }

    @Transactional(isolation = Isolation.READ_COMMITTED)
    public void readCommittedTransaction() {
        // Your code here
    }

    @Transactional(isolation = Isolation.REPEATABLE_READ)
    public void repeatableReadTransaction() {
        // Your code here
    }

    @Transactional(isolation = Isolation.SERIALIZABLE)
    public void serializableTransaction() {
        // Your code here
    }
    출처: <https://bangpurin.tistory.com/273> [기억 파편:티스토리]
    ```

    * 다만 위의 어노테이션은 연결된 DB의 종류에 따라 예외가 발생할 수 있음 (ex : READ\_UNCOMMITTED)

    Phantom Read : • 다른 트랜잭션에서 수행한 변경 작업에 의해 레코드가 보였다가 안 보였다가 하는 현상
*

    <figure><img src="../../../../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure>
