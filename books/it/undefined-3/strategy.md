# - Strategy

### 전략 패턴

#### 개요

* 전략을 선택하여, 객체가 동작하도록 한다.
* 전략이 바뀌어도, 객체의 동작에는 영향이 없다.
* 객체의 동작 ( 행위 디자인 패턴 ) 이다.
* 클라이언트가 다양한 전략 중 하나를 선택해 생성한 후에 전략을 실행할 컨텍스트에 주입하여 사용하는 패턴이다.
* 변경되는 부분을 인터페이스로 분리하고 변경되지 않는 부분은 컨텍스트에 존재한다.

#### 주로 사용 목적

* **여러 버전이 필요할 때 사용.**
* Redis, Memecache (캐시)
* MySQL, Postgresql (DB)
* **알고리즘의 동작이 런타임에서 교체되어야 할 때**

구조도

<figure><img src="../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Code Example

```
interface InterfaceStrategy {
    void doSomething();
}

// Redis 구현용
class RedisImpl implements InterfaceStrategy {
    public void doSomething() {}
}

// Memcache 구현용
class MemcacheImpl implements InterfaceStrategy {
    public void doSomething() {}
}

-----------------------

class Something {

   InterfaceStrategy strategy;
   
   void setStrategy(InterfaceStrategy strategy) {
	   this.strategy = strategy;
   }
   
   void doSomething() {
	   this.strategy.doSomething();
   }
}

------------------------

public static void main(String[] args) {

  Something s = new Something();
  
  s.setStrategy(new MemcacheImpl()); // Memcache 실행
  s.doSomething();
  
  s.setStrategy(new RedisImpl());    // Redis 실행
  s.doSomething();
}
```

#### 고려 사항

1. 전략이 많아 지면, 인터페이스 및 객체 수가 늘어난다.
2. 알고리즘이 복잡하지 않다면, 관리 클래스 수를 고려하여 전략 패턴을 적용할 이유가 없다.
3. 복잡도가 올라간다
4. 공통의 프로세스를 (인터페이스) 구체화 해야 한다.

