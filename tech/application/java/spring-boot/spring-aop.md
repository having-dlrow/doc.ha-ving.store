---
description: 선언적 트랜잭션 관리, 보안, 로깅과 같은 공통 기능을 쉽게 구현
---

# Spring Aop

```
implementation 'org.springframework.boot:spring-boot-starter-aop'
```

* 횡단 관심사(Cross-Cutting Concerns)를 모듈화하는 프로그래밍 패러다임
* 프록시 패턴을 기반으로 런타임 위빙(Runtime Weaving)을 사용
* JDK 동적 프록시 또는 CGLIB 프록시

<figure><img src="../../../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

### AspectJ

* 컴파일 타임, 로드 타임, 런타임에 걸쳐 더 광범위한 AOP 지원을 제공하는 독립적인 프레임워크
* 컴파일 타임 위빙(Compile Time Weaving)과 로드 타임 위빙(Load Time Weaving)을 지원
* 바이트코드를 직접 조작하여 AOP를 구현
* ajc 컴파일러가 필요



#### JoinPoint

#### PointCut

* first wildcard matches any return value
* _(..)_ pattern matches any number of parameters (zero or more)

```
@Pointcut("execution(* com.baeldung.pointcutadvice.dao.FooDao.*(..))")
```

```
@Pointcut("within(com.baeldung..*)")
```

```
@Pointcut("this(com.baeldung.pointcutadvice.dao.FooDao)")
```

```
@Pointcut("target(com.baeldung.pointcutadvice.dao.BarDao)")
```

* **Pointcut 표현식은 &&** , **||** , **!** 연산자를 사용하여 결합할 수 있습니다 .

```
@Pointcut("@target(org.springframework.stereotype.Repository)")
public void repositoryMethods() {}

@Pointcut("execution(* *..create*(Long,..))")
public void firstLongParamMethods() {}

@Pointcut("repositoryMethods() && firstLongParamMethods()")
public void entityCreationMethods() {}
```

#### Advice
