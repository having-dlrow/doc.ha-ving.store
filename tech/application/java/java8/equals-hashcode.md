# equals() , hashcode()

\[ 질문 ]

* equals() 와 hashcode() 의 차이점에 대해 설명해주세요.
* equals() 는 왜 오버라이드 해서 사용하는 걸까요?
* equals() 를 오버라이드 할 때 왜 hashcode() 도 함께 오버라이드 해야할까요?

\[ 정답 ]

*   해설

    **equals() 와 hashcode()**

    * equals() 는 두 개의 객체가 동일한지 동일성을 비교하는 것입니다. 즉, 객체가 **같은 메모리 주소**인지 비교합니다.
    * hashcode() 는 **객체의 메모리 주소에 대한 해시 코드**를 반환하는 메소드입니다. 메모리 주소는 객체마다 고유한 값이기 때문에 해시 코드도 고유한 값을 가지게 됩니다.

    **equals() 를 오버라이딩해서 사용하는 이유**

    * 프로그래밍을 하다보면 메모리 주소는 다르지만 같은 값을 가지고 있어서 같은 객체로 인식해야 하는 경우가 있는데 이런 경우에 동등성을 가지도록 equals() 를 오버라이딩 해주어야합니다.

    **equals() 를 오버라이드할 때 hashcode() 도 같이 오버라이드 하는 이유**

    * 동일한 객체는 동일한 메모리 주소를 갖는다는 의미이므로 동일한 객체는 같은 해시코드를 가져야합니다. 그렇기 때문에 equals() 를 재정의 한다면 hashcode() 도 재정의되어야 합니다.
    * ex) hashMap 의 Key 값

Ref \
\- [https://mangkyu.tistory.com/101](https://mangkyu.tistory.com/101)\
\-[https://f-lab.kr/insight/java-object-class-equals-hashcode?gad\_source=1\&gclid=Cj0KCQjwudexBhDKARIsAI-GWYUqQXMQVnzKUdVa1oW2B-\_upTBwOVqfoXAToeQL6YRBfhW6rxniYYYaApewEALw\_wcB](https://f-lab.kr/insight/java-object-class-equals-hashcode?gad\_source=1\&gclid=Cj0KCQjwudexBhDKARIsAI-GWYUqQXMQVnzKUdVa1oW2B-\_upTBwOVqfoXAToeQL6YRBfhW6rxniYYYaApewEALw\_wcB)
