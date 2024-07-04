---
description: https://docs.spring.io/spring-framework/reference/core/beans/basics.html
---

# - 컨테이너 개요

개요

`org.springframework.context.ApplicationContext` 인터페이스가 IoC 컨테이너를 대표하며, 이를 통해 인스턴스화, 설정초기화, 구성을 한다.

컨테이너는 Configuration metadata을 읽고 오브젝트에 필요한 인스턴스화할 대상과 configuration을 목록화 한다. configuration metadata는 xml, java annotation, javacode 등으로 만들 수 있다. 이를 통해, bean의 상호 관계를 나타낼 수 있다.

`ApplicationContext`을 implement한 다양한 인터페이스가 제공된다. 표준적인 application에서는 `classPathXmlApplicationContext`, `FileSystemXmlApplicationContext`가 사용된다.

대부분의 Application 에서 사용자 코드를 인스턴스화 하기 위해 작성할 필요가 없습니다. 상용구 적으로 사용되는 8줄 정도의 xml이 제공됩니다.

### Metadata 설정하기

IoC Container는 Configuration Metadata를 읽는다고 언급했듯이, 개발자가 작성한 코드의 Object가 인스턴스화, 구성, 조립 하는 과정을 한다.

초기에는 Configuration Metadata는 단순하고, 직관적인 XML 형태였다. (현재는 java-based 형태가 가장 많이 사용되고 있다.)

* [Annotation-based configuration](https://docs.spring.io/spring-framework/reference/core/beans/annotation-config.html)
* [java-based configuration](https://docs.spring.io/spring-framework/reference/core/beans/java.html)

Spring Configuration은 한개 이상의 bean 구성이며, 컨테이너가 관리한다. XML 기반에서는 상위 `<beans>` 안에 `<bean>` 요소로 구성한다. (java 기반에서는 class에 @Configuration을 사용하고, @Bean Annotation 방식을 사용한다.)

이 bean 정의는 실제 객체에 해당한다. 일반적으로 Dao 객체와 같은 service layer 객체, persistent layer 객체, infrastructure object (JPA의 EntityManagerFactory, JMS queues 같은) 등이 선언된다.

일반적으로 세분화된 도메인 객체는 정의 되지 않는다. 왜냐하면, 로드하거나 생성하는 책임은 repositories 또는 비지니스 로직에게 있기 떄문이다.

```web.xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
		https://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="..." class="...">  
		<!-- collaborators and configuration for this bean go here -->
	</bean>

	<bean id="..." class="...">
		<!-- collaborators and configuration for this bean go here -->
	</bean>

	<!-- more bean definitions go here -->

</beans>
```

### Container 인스턴스화

다양한 외부 리소스(예, 로컬 파일 시스템, 자바 classPath)에 있는 설정을 ApplicationContext에 전달 할 수 있다.

```
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");
```

:::note 스프링의 리소스 추상화 매커니즘은 [#Application Context and Resource Paths](https://docs.spring.io/spring-framework/reference/core/resources.html#resources-app-ctx)를 참고 바란다 :::

service layer의 구성파일 예

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
		https://www.springframework.org/schema/beans/spring-beans.xsd">

	<!-- services -->

	<bean id="petStore" class="org.springframework.samples.jpetstore.services.PetStoreServiceImpl">
		<property name="accountDao" ref="accountDao"/>
		<property name="itemDao" ref="itemDao"/>
		<!-- additional collaborators and configuration for this bean go here -->
	</bean>

	<!-- more bean definitions for services go here -->

</beans>
```

data(repository) layer의 구성파일 예

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
		https://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="accountDao"
		class="org.springframework.samples.jpetstore.dao.jpa.JpaAccountDao">
		<!-- additional collaborators and configuration for this bean go here -->
	</bean>

	<bean id="itemDao" class="org.springframework.samples.jpetstore.dao.jpa.JpaItemDao">
		<!-- additional collaborators and configuration for this bean go here -->
	</bean>

	<!-- more bean definitions for data access objects go here -->

</beans>
```

`name`속성은 JavaBean의 이름을,`ref`속성은 bean정의에서 Id 값을 가르킨다. :::note `id`와 `ref` 요소간의 의존성은 [의존성](https://docs.spring.io/spring-framework/reference/core/beans/dependencies.html)를 참고 바란다. :::

#### XML 기반 Configuration Metadata 작성

여러개의 XML 파일로 구성하는 것이 유용하다. 그러면, 각각의 XML이 논리적으로 레이어 또는 모듈을 표현 하도록 한다.

이전에 설명했듯이 Application Context는 여러 Resource로 부터 읽어 올 수 있다. 따라서, 한 개 이상의 `<import/>` 요소를 사용하여, 다른 파일들을 읽는다. 예:

```
<beans>
	<import resource="services.xml"/>
	<import resource="resources/messageSource.xml"/>
	<import resource="/resources/themeSource.xml"/>

	<bean id="bean1" class="..."/>
	<bean id="bean2" class="..."/>
</beans>
```

위 예제에서 외부 Bean 정의를 3개의 다른 파일들 `service.xml`, `messageSource.xml`,`themeSource.xml`에서 불러 온다. 모든 path 정보는 `importing이 수행되는 정의 파일`로 부터 상대 경로다. 따라서, `service.xml`은 `importing이 수행되는 정의 파일`과 동일한 directory 또는 classPath에 위치한다. 반면에, `message.xml`과 `themeSource.xml`은 반드시 `importing이 수행되는 정의 파일`의 위치 하단 resources 경로 아래에 있어야 한다. 첫 머리말의 '/'는 무시된다. path 정보는 상대적으로 주어지기 때문에 '/'을 첫 글자에 사용하지 않는것이 좋다.

각 파일들로 부터 `<beans>` 요소를 포함한 모든 요소들이 import 된다. 이때, 스프링 스키마에 따른 유효한 XML Bean 정의 형태여야 한다.

:::note `../`을 사용하여 상단 디렉토리를 나타내는 것은 권장되지 않습니다. 현재 어플리케이션 외부에 있는 파일과 의존성을 갖을 우려가 있습니다. 특히, `classpath` (런타임 프로세스는 가장 근접한 classPath root 을 선택하고, 그것의 상위 디렉토리를 살피기 때문에) 에 사용하는 것을 추천 하지 않습니다. classpath 구성 변경에 의해, 다른, 잘못된 디렉토리 선택 될수 있습니다. :::

또한, 네임스페이스가 import 기능의 역할을 수행합니다. 일반적이지 않은 bean을 정의 할 때, 스프링에서 제공하는 XML namespace 선택자를 사용할 수 있습니다. (예, `context`, `util` 네임스페이스)

#### The Groovy Bean Definition DSL

더 나아가, 외부에서 설정가능한 configuration metadata, bean 정의는 스프링의 Groovy Bean Definition DSL 이다. Grails Framework로 알려져 있다. 특히, 아래와 같은 구조로 `.groovy`파일을 통해 설정한다.

```
beans {
	dataSource(BasicDataSource) {
		driverClassName = "org.hsqldb.jdbcDriver"
		url = "jdbc:hsqldb:mem:grailsDB"
		username = "sa"
		password = ""
		settings = [mynew:"setting"]
	}
	sessionFactory(SessionFactory) {
		dataSource = dataSource
	}
	myService(MyService) {
		nestedBean = { AnotherBean bean ->
			dataSource = dataSource
		}
	}
}
```

이런 설정 스타일은 매우 XML 형태와 동일하며 스프링의 XML configuration namespace도 지원된다. `importBeans` 지시자를 통해 XML bean을 import 할수 있다.

### Container 사용하기

`ApplicationContext`은 각기 다른 bean들과 bean들의 관계를 저장하기위한 고급화된 인터페이스이다. `T getBean(String name, class<T> requiredType)` method 을 통해, bean들의 인스턴스를 얻는다.

`ApplicationContext`는 bean을 정의하며, bean에 접근할 수 있게 한다. 예:

```
// create and configure beans
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");

// retrieve configured instance
PetStoreService service = context.getBean("petStore", PetStoreService.class);

// use configured instance
List<String> userList = service.getUsernameList();
```

Groovy 설정의 bootstrapping 방식도 유사하다.

```
ApplicationContext context = new GenericGroovyApplicationContext("services.groovy", "daos.groovy");
```

좀더 flexible한 방식은 `GenericApplicationContext`을 사용하는 것이다. XML일 때는 `XmlBeanDefinitionReader`를 reader로 위임하는 방식이다.

```
GenericApplicationContext context = new GenericApplicationContext();
new XmlBeanDefinitionReader(context).loadBeanDefinitions("services.xml", "daos.xml");
context.refresh();
```

또, Groovy 일때는 `GroovyBeanDefinitionReader`를 reader로 위임하는 방식이다.

```
GenericApplicationContext context = new GenericApplicationContext();
new XmlBeanDefinitionReader(context).loadBeanDefinitions("services.xml", "daos.xml");
context.refresh();
```

위와 같이 reader을 위임하고, `getBean()`을 통해 bean 인스턴스를 가져온다. `ApplicationContext`로 부터 bean을 가져오는 다른 방법도 있지만, 이상적으로 사용하면 안된다. 스프링 API을 직접 호출하거나, 의존성을 가지면 안된다.

스프링이 통합한 web framework에서는 DI(dependency Injection)을 제공한다. 다양한 web component (controllers, jsf-managed beans)은 DI로 제공되며, metadata(autowired annotation)을 통해 의존성을 정의하도록 한다.
