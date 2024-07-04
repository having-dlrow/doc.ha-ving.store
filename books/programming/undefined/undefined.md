---
cover: >-
  https://images.unsplash.com/photo-1503614472-8c93d56e92ce?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwyfHxjYW5hZGF8ZW58MHx8fHwxNzEwOTU2OTIyfDA&ixlib=rb-4.0.3&q=85
coverY: 187.86176470588236
---

# 관심사의 분리

1. 중복 코드 Method 추출
2. 관심사 분리
   * DAO 분리
     * <mark style="color:red;">템플릿 메소드 패턴</mark>
       * <mark style="background-color:yellow;">단점: 클래스가 많다 >>>> 템플릿 메서드 패턴 with 익명 클래스</mark>
     * <mark style="color:red;">팩토리 메소드 패턴</mark>
       * **인터페이스 타입으로 리턴**되므로, 정확히 어떤 클래스 관심  X

```
// 템플릿 메소드 패턴
public abstract class AbstractTemplate {
    public exec();                      // hook method
    public void ActuallyDoMethod() {    // template Method
        startlog();
        exec();
        endlog();    
    }
}

public class SubClass extends AbstractTemplate {
    exec() {
        // custom code
    }
}
```

<details>

<summary><mark style="background-color:yellow;">템플릿 메소드 패턴 with 익명 클래스</mark></summary>

```
AbstractTemplate template1 = new AbstractTemplate() {
    @Override
    protected void exec() {
        // custom code
    }
}
```

</details>

3. 인터페이스의 도입

```
// 팩토리 메소드 패턴

Connection redis = new ConnectionFactory('redis');
Connection memcache = new ConnectionFactory('memcache');
```

4.  관계 설정 책임의 분리

    " A 클래스는 Redis를 사용하고, B 클래스는 Memcache를 사용하면, \
    &#x20; DB 타입을 지정하는 코드가 남아 로직분리가 되지 않는다!  "

    1. 오브젝트 사이의 관계 : 런타임 시 한쪽이 다른 오브젝트의 레퍼런스를 갖고 있는 방식

```
Main {
 Connection redis = ConnectionFactory('redis');
 Connection memcache = ConnectionFactory('memcache');
 
 AUserDao(redis);
 BUserDao(memcache);
}

```

5.  개방 폐쇄 원칙 ( OCP )

    <mark style="color:orange;">#solid #Single Responsibility Principle #Open Closed Principle #Liskov Subsitution Principle</mark>\ <mark style="color:orange;">#Interface Segregation Principle #Dependency Inversion Principle</mark>

* 높응
* 낮결
* 전략 패턴
