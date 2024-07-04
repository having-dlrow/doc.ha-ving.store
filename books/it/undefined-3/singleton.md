# - Singleton

## 설명&#x20;

단 하나의 인스턴스 사용법

## 1. Basic Code (Eager Initialization)

```
class A {
    private static final A instance = new A();
    
    public static A getInstance() {
        return instance;
    }
    
    private A() {}
}
```

<table><thead><tr><th width="321">장점</th><th>단점</th></tr></thead><tbody><tr><td> 기본 형태</td><td>getInstance() 호출과 별개로,<br>A class가 항상 로딩됨</td></tr></tbody></table>

<details>

<summary>Static Block</summary>

Eager Initialization 과 유사 방식, 메모리(Heap) 사용

* 장점 :  try-catch 사용

```
class A {
    private static A instance;
    
    static {
        try { instance = new A(); } catch(Exception e) {}
    }
    
    public static A getInstance() {
        return instance;
    }
    
    private A() {}
}
```

</details>

<details>

<summary>Lazy Initialization</summary>

Eager Initialization 단점 보완

* 장점 :  getInstance()을 통해, 필요한 시점에 인스턴스 생성

```
class A {
    private static final A instance
    
    public static A getInstance() {
        if(Object.isNull(instance)) {
            instance = new A();
        }
        return instance;
    }
    
    private A() {}
}
```



</details>

## 2. Thread

### Synchronized

: 함수를 Thread 내에서 한번 실행되도록 함

<pre><code><strong>class A {
</strong>    private static final A instance;
    
    public static synchronized A getInstance() {
        if(Object.isNull(instance)) instance = new A();
        return instance;
    }
    
    private A() {}
}
</code></pre>

```
class A {
    private static final A instance;
    
    public static synchronized A getInstance() {
        if(Object.isNull(instance)) {
             synchronized (A.class) {
                 instance = new A();
             }
         }
        return instance;
    }
    
    private A() {}
}
```

### Synchronized + Null Check

```
class A {
    private static final A instance;
    
    public static synchronized A getInstance() {
        if(Object.isNull(instance)) {    # instance가 있으면, 빠른 인스턴스 리턴
             synchronized (A.class) {
                 if(Object.isNull(instance)){    # synchronized 안에서, instance 한번 생성
                     instance = new A();
                 }
             }
         }
        return instance;
    }
    
    private A() {}
}
```

<details>

<summary>Synchronized 변수에서 발생 가능 이슈</summary>

\[ simulation ]&#x20;

1. A Thread : instance 생성, synchronized 벗어남
2. B Thread : synchronized 입성, null 체크
3. 메모리 간 동기화 中
   1. A Thread Working Memory (존재), Main Memory (동기 직전 혹은 진행 중)
   2. A Thread Working Memory (존재), B Thread Working Memory (동기 직전 혹은 진행 중)
4. (오류 발생) 별도 instance,  B Thread가 생성

</details>

## 3. static 내부 클래스

static inner 클래스는  Memory에 바로 로딩 되지 않고,  instance화 과정에서 로딩하는 점을 이용한 방식.

```
class A {
    
    private static class Helper() {
        private static final A instance = new A();
    }
    
    public static A getInstance() {
        return Helper.instance;
    }    
    
    private A() {}
}
```

## 4. Enum

Enum이 전역적 접근이 가능하며,  한번만 instance화 하는 태생을 이용한 방식.&#x20;

단점 : 바로 로딩 됨 ( Lazy initialization 안됨 )

<pre><code><strong>public enum A {
</strong>    INSTANCE;
    
    public void someMethod(String param) {
        
    }
}
</code></pre>

## 5. :thumbsup: Volatile + Synchronized + Null Check

<details>

<summary>Volatile 이해하기</summary>

* Thread Local이 아닌, Main Memory에 생성하여 일관성 유지
* 스레드가 직접 메인 메모리에서 읽어온다.
* volatile 변수에 대한 write는 즉시 메모리에 반영된다.
* 다른 스레드가 volatile 변수를 캐시하면, read/write시 즉시 동기화 한다

<pre><code><strong>volatile boolean flag = true;
</strong><strong>public void run() {
</strong><strong>    while(flag) {
</strong><strong>        ...
</strong><strong>    }
</strong><strong>}
</strong><strong>
</strong><strong>public void stop() {
</strong><strong>    flag = false;
</strong><strong>}
</strong></code></pre>

</details>

* Synchronized ( Thread Safe) 하게 생성 하여, Main Memory 에 하나의 인스턴스를 저장한 형태

<pre><code><strong>public class A {
</strong>    private volatile static A;
    
    public static A getInstance() {
        if(Object.isNull(instance)) {
             synchronized (A.class) {
                 if(Object.isNull(instance)){
                     instance = new A();
                 }
             }
         }
        return instance;
    }
    
    private A() {}
}
</code></pre>

*
