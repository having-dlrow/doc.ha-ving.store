# 🕸️ Network

### 기본 네트워크 구성

```
node$ docker network ls
NETWORK ID          NAME                DRIVER      SCOPE
1befe23acd58        bridge              bridge      local
0ea6066635df        docker_gwbridge     bridge      local
726ead8f4e6b        host                host        local
8eqnahrmp9lv        ingress             overlay     swarm
ef4896538cc7        none                null        local
0cihm9yiolp0        overnet             overlay     swarm
```

### Driver 종류

<figure><img src="../../../.gitbook/assets/image (9) (1) (1).png" alt="" width="375"><figcaption><p>@copywrite docker official github</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption><p>@copywrite docker official github</p></figcaption></figure>

* [bridge](https://github.com/docker/labs/blob/master/networking/A2-bridge-networking.md) :  호스트 네트워크와 게스트 네트워크를 브릿지하여 두 개의 네트워크를 하나의 네트워크처럼 사용
* [overlay ](https://github.com/docker/labs/blob/master/networking/A3-overlay-networking.md): 여러 도커 호스트에 걸쳐 배포된 컨테이너 그룹을 같은 네트워크에 배치하기 위한  가상 네트워크&#x20;
