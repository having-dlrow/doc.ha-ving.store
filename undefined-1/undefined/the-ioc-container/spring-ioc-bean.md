---
description: https://docs.spring.io/spring-framework/reference/core/beans/introduction.html
---

# - Spring IoC 컨테이너 및 Bean 소개

### <mark style="color:blue;">요약 내용</mark>

ApplicationContext는 일종의 BeanFactory의 기업용 특화 버전.

스프링에서는 Ioc Container에 의해 인스턴스화 되며, 조립(assemble)되고, 관리되는 Object을 Bean이라고 한다.\
또는 일반적으로 작성되는 Application의 Object도 Bean이라고 한다.

Bean과 Bean간의 관계/종속성은 컨테이너가 사용하는 구성 메타데이터에 반영된다.\
컨테이너가 Bean이 생성 될때 의존성을 주입해주는 행위를 DI라고 한다.

***

### Inversion of Controls 원칙

DI(Dependency Injection)으로도 알려져 있다.

DI란?

* 생성자 인수
* 팩토리 함수의 인수
* 인스턴스의 속성(properties)

컨테이너가 Bean이 생성 될때 의존성을 주입해주는 행위.\
이 행위가 역으로 실행되므로, inverse of Control 이라고도 말함.

`org.springframework.beans`, `org.springframework.context` 패키지는 IOC의 근간, [`org.springframework.beans.factory.BeanFactory`](https://docs.spring.io/spring-framework/docs/6.1.3/javadoc-api/org/springframework/beans/factory/BeanFactory.html)\` 인터페이스는 모든 유형의 객체를 관리할 수 있는 구성 메커니즘을 제공.

`ApplicationContext`는 BeanFactory의 하위 인터페이스로, 아래의 특징이 더해진 것.

* AOP와 쉬운 통합
* 국제화 Message resource 처리
* 이벤트 발행
* WebApplicationContext (웹 특화용)
