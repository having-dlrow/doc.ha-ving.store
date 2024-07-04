---
description: client side Load balancer
---

# Service Discovery

## Feign Client

<details>

<summary>RestTemplate</summary>

```
RestTemplate restTemplate = new RestTmplate();
restTemplate.getForObject("http://localhost:8080/", User.class, 200);
```

</details>

* RESTful 웹 서비스 간의 통신을 간편하게 처리하고, 코드의 간결성 향상 목적
* Netflix OSS 프로젝트 일부

```
@FeignClient("stores")
public interface StoreClient {
    @RequestMapping(method=RequestMethod.GET, value="/store")
    List<Store> getStores();
```

* Microservice("Stores")의 주소 없이, `/store` 연결



