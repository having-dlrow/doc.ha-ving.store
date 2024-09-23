# Architecture

**Hexagonal Architecture** : 외부 인터페이스를 통해서만 내부에 접근 가능, 경계간 이동 제한

* Adapter : 외부 시스템과의 직접적인 구현 및 상호작용을 처리
* Port : Adapter와 통신하기 위한 동작 정의

***

**Layered Architecture** ( 계층화 ) : 계층 간 접근

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

* Presentation  Layer
* Application  Layer
* Domain Layer
* Infra Layer
