# - SAGA Pattern

SAGA 패턴 개념&#x20;

* 트랜잭션 관리 주체 : Application 단위
* 작업이 실패하면 이전까지 작업된 마이크로 서비스에 보상 이벤트를 소싱하여, 원자성 보장
* 2PC ( 2 Phase Commit ) 같은 방식을 사용 할 수 없고, 이벤트 / 명령어 방식으로 한다.

<figure><img src="../../../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>
