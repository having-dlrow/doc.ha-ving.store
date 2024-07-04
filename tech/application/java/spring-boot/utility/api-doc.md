# API Doc

## Swagger API

`Spring doc`, `Spring fox` 두 라이브러리 모두 Spring framework 사용하여, Swagger API 문서를 쉽게 사용하도록 하는 라이브러리 이다.



### Spring Doc ✅

* API Grouping 가능하다.
* OpenAPI 3.0 스펙에 맞는 JSON을 만들어준다.

#### **구성요소**

* `swagger-ui` : 핵심 로직
* `springdoc-openapi` : swagger-ui 추상화하여 활용성을 넓히는 라이브러리

```
// build.gradle
implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.3.0'
```

```
## docs
springdoc:
    default-produces-media-type: application/json;charset=UTF-8
    default-consumes-media-type: application/json;charset=UTF-8
    swagger-ui:
        path: /api-docs.html
        operations-sorter: method
        display-request-duration: true

    api-docs:
        path: /api-docs
```



### Spring Fox ✅

```
// build.gradle
implementation 'io.springfox:springfox-swagger-ui:3.0.0'
implementation 'io.springfox:springfox-swagger2:3.0.0'
```

```
@Configuration
@EnableSwagger2
public class SwaggerConfig {
    ...
}
```
