# Spring Cloud Eureka

## 클라이언트 설정

<details>

<summary>호스트 명 </summary>

**`prefer-ip-address` :** 호스트 이름이 아닌 IP 주소를 Eureka Server 에 등록하도록 지정 (디폴트 false)

```
spring:
  cloud:
    inetutils:
      ignored-interfaces: eth1*
      preferred-networks: 192.168

eureka:
  instance:
    prefer-ip-address: true
```

</details>

<details>

<summary>등록</summary>

**`register-with-eureka` :  자신을 등록할지 여부 (default:true)**

**`fetch-registry`  :   정보를 가져옴 (default: true)**

<pre><code><strong> 
</strong><strong>eureka:
</strong>  client:
    register-with-eureka: true
    fetch-registry: true
</code></pre>

</details>

<details>

<summary>갱신</summary>

**`registry-fetch-interval-seconds` : 10초마다 서비스 캐싱 (default: 30초)**

**`disable-delta` : 캐싱시 변경사항 반영 (default:false)**

```
eureka:
  client:
    registry-fetch-interval-seconds: 10
    disable-delta: true
```

</details>

<details>

<summary>서비스 해제</summary>

2. 하트비트

**`lease-renewal-interval-in-seconds` : 서버에게 하트비트 전송 (default:30초)**

**`lease-expiration-duration-in-seconds` :** 하트비트 못받아서 장애로 판단하는  duration값 (default: 90초)

* 유레카 인스턴스가 정상적으로 종료된 경우는 레지스트리에서 바로 제거
* 이 값은 `lease-renewal-interval-in-seconds` 보다 커야 함

```
eureka:
  instance:
    lease-renewal-interval-in-seconds: 3
    lease-expiration-duration-in-seconds: 10
```

</details>

<details>

<summary>서버 상태 확인 Task</summary>

**`eviction-interval-timer-in-ms:`** 클라이언트로부터 하트비트가 계속 수신되는지 점검을 하는 주&#xAE30;**`(default: 60초)`**

```
eureka:
  instance:
    eviction-interval-timer-in-ms: 10000 // 10초
```

</details>

## 서버 설정

<details>

<summary>업데이트 주기</summary>

**`response-cache-update-interval-ms : 캐싱 업데이트 (default: 30초)`**

```
eureka:
  server:
    response-cache-update-interval-ms: 5000 // 5초
    // client.registry-fetch-interval-seconds 5초 보다 길게
```

</details>

설정 시간 내 하트비트가 일정 횟수 이상 들어오지 않아야 서비스 해제된다.

<details>

<summary>서비스해제</summary>

1. 일시적 네트워크 에러

**`enable-self-preservation` : 서비스 해제를 막기 위한 보호 모드 (default: true)**

```
eureka:
  server:
    enable-self-preservation: false
```

2. 하트 비트

보호 모드(false) 상황에서도, 서버 해제가 오래 걸린다.

`lease-renewal-interval-in-seconds` : 클라이언트 하트비트 전송 주기 (default: 30초)

`lease-expiration-duration-in-seconds` : 하트비트 못받아서 장애로 판단하는  duration값 (default: 90초)

</details>

하트 비트 설정을 조절하여도, 60초 마다 점검하므로, 60초 + 3초 \* 3 이상 소요된다.

<details>

<summary>클라이언트 상태 확인 Task</summary>

**`eviction-interval-timer-in-ms:`** 클라이언트로부터 하트비트가 계속 수신되는지 점검을 하는 주&#xAE30;**`(default: 60초)`**

```
eureka:
  server:
    eviction-interval-timer-in-ms: 10000 // 10초
```

</details>



***

### server&#x20;

```
server:
  port: 8761


eureka:
  server:
    enable-self-preservation: false
    response-cache-update-interval-ms: 5000
    eviction-interval-timer-in-ms: 10000

```

### client&#x20;

```
eureka:
  client:
    disable-delta: true
    fetch-registry: true
    register-with-eureka: true
    registry-fetch-interval-seconds: 10
    service-url:
      defaultZone: http://localhost:8761/eureka
  instance:
    prefer-ip-address: true
    instance-id: ${spring.application.name}:${spring.application.instance_id:${random.value}}
    lease-renewal-interval-in-seconds: 3
    lease-expiration-duration-in-seconds: 9
    eviction-interval-timer-in-ms: 10000
```

## N개 Server 구성

유레카는 등록된 서비스에서 10초 간격으로 연속 3회의 상태 정보(heartbeat)를 받아야 하므로 등록된 개별 서비스를 보여주는데 30초 소요

<details>

<summary>동기화</summary>

**`wait-time-in-ms-when-sync-empty` :** 노드로부터 Instance 들을 가져올 수 없을 때 기다릴 시간 ( default:3000ms)

**`registry-sync-retries :`** 노드로부터 registry 를 갱신할 수 없을 때 재시도 횟수 ( default:5)

```
eureka:
  server:
    wait-time-in-ms-when-sync-empty: 3000
    registry-sync-retries: 5
```

</details>
