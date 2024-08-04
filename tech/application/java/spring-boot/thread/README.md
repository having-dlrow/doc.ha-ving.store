# Thread

\[ 문제 ]

* Spring Bean 은 Thread Safe 할까요?

\[ 정답 ]

* 해설
  * 스프링 빈은 기본적으로 **싱글톤 빈**으로 등록됩니다. 지역변수는 쓰레드마다 각각의 다른 메모리 영역이 할당되기 때문에 동시성 문제가 발생하지 않지만, 싱글톤으로 등록된 인스턴스의 필드를 여러 쓰레드가 동시에 접근하는 경우 문제가 발생하는데 이를 위해 ThreadLocal 을 사용하여 해결할 수 있습니다.
  * **ThreadLocal** : 여러 개의 쓰레드가 존재할 때 해당 쓰레드에만 접근할 수 있는 특별한 저장소로 멀티 쓰레드 환경에서 공유 자원의 동시성 문제를 해결하기 위해 사용

**Concurrent 클래스를** 통해서 보장할 수 있다.

* Concurrent Queue
* Concurrent

Spring Bean은 Thread safe할까? 관련 설명 자료 : [https://alwayspr.tistory.com/11](https://alwayspr.tistory.com/11) 해결법 : [https://velog.io/@on5949/JAVA-쓰레드-6.Thread-safe](https://velog.io/@on5949/JAVA-%EC%93%B0%EB%A0%88%EB%93%9C-6.Thread-safe)



ThreadLocal 참고 자료 : [https://velog.io/@dbsrud11/SpringBoot-핵심-원리-쓰레드-로컬-ThreadLocal-2](https://velog.io/@dbsrud11/SpringBoot-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EC%93%B0%EB%A0%88%EB%93%9C-%EB%A1%9C%EC%BB%AC-ThreadLocal-2)
