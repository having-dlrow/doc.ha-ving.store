# Pattern

## 12가지 디자인 패턴으로 알아보는 클라우드 네이티브 마이크로서비스 아키텍처

자료: [https://www.slideshare.net/awskorea/aws-summit-seoul-2023-12](https://www.slideshare.net/awskorea/aws-summit-seoul-2023-12)

API 관리&#x20;

* <mark style="color:blue;">API Gateway Pattern</mark>

Event Driven Architect Pattern

* <mark style="color:blue;">Publish - Subscribe Pattern ( 주문/결제/상품 )</mark>
* Producer-Consumer Pattern
* Event Sourcing Pattern

Migration Pattern

* <mark style="color:red;">Strangler Fig Pattern</mark>
* Anti-corruption Layer Pattern
* Parallel Run Pattern
* Change Data Capture Pattern

Service

* <mark style="color:blue;">Sidecar Pattern ( Monitoring )</mark>
* Service Mesh Pattern ( Envoy )
* Service Orchestration Pattern

Database

* Database Per Service Pattern
* <mark style="color:blue;">Data Locality Pattern</mark>
* CQRS Pattern ( 재고 이벤트 )
* Materialized View Pattern ( 좋아요 반영 )

Community&#x20;

* Request-Response Pattern
* Asynchronous Request Reply Pattern
* Single Receiver Pattern
* <mark style="color:blue;">Multiple Receiver Pattern</mark>
