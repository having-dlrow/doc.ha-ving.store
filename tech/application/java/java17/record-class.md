# Record Class

이해하기

* Enum과 같은 특별한 형태의 class 이다.
* 간단하게 데이터를 저장하고 옮기는 역할
* getter, hashcode, equals, toString이 기본제공된다.



문법

* 생성자 처럼 쓴다.

```
public record User(Long id, 
        String Name,
        String email, 
        int age) { }        
```



단점&#x20;

* java.lang.Record 를 상속하고 있어, 다른 class 상속이 안된다.
* f inal class로 상속이 안된다.
