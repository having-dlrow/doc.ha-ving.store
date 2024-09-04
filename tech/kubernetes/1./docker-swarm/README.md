---
description: '#_클러스터_구축_및_관리'
---

# 🐛 Docker Swarm

* docker swarm _(classic)_  :  > 1.6&#x20;
* ✅ swarm mode : > <mark style="color:red;">1.12</mark>

### Concept&#x20;

자원이 부족하게 된다면 자원을 병렬로 확장한다.

### 장점

* 멀티 호스트 관리
* 암호화된 네트워크

### 구성

* 서비스
* 자동 확장
* 스케줄링  ( _Task(컨테이너)를 노드에 분배하는 작업을 의미 )_
* DNS
* 로드밸런서

### 설치

Master Node

<pre class="language-bash"><code class="lang-bash">docker swarm init --advertise-addr 192.168.0.100
<strong>Swarm initialized: current node (xpjgazyylrs1rakd397hl3cmv) is now a manager.
</strong>To add a worker to this swarm, run the following command:
    docker swarm join --token SWMTKN-1-3wwnt9pyw05mdfznlcurr9jt8lz8mo9e5re4ga7wn7ohie8uq1-aehvli6arxx6dj8v7t5u0isvg 192.168.0.100:2377
To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
</code></pre>

Worker Node

```
    docker swarm join --token SWMTKN-1-3wwnt9pyw05mdfznlcurr9jt8lz8mo9e5re4ga7wn7ohie8uq1-aehvli6arxx6dj8v7t5u0isvg 192.168.0.100:2377
```

노드 확인&#x20;

```
docker node ls
```



### 서비스 생성

```
Usage: docker service create [OPTIONS] IMAGE [COMMAND] [ARG...]
```

```
Usage: docker service ls
Usage: docker service ps [SERVICE]
```



### 자동 확장

```
Usage: docker service scale SERVICE=REPLICAS [SERVICE=REPLICAS...]
```

배포 전략 ( Rolling Update )

```
Usage: docker service update --update-parallelism 1 SERVICE
```

<pre><code><strong>Usage: docker service update --rollback SERVICE
</strong></code></pre>



### 스케줄링

노드별 설정 또는 라벨링(labeling)을 통해 스케줄링 가능한 노드의 범위를 제한

<pre><code><strong>Usage: docker node update --label-add foo --label-add type=redis SERVICE
</strong></code></pre>



### DNS

Ingress 네트워크는 docker swarm init/join 할 때 자동으로 생성된다.&#x20;

Ingress 네트워크는 서비스의 노드들 간에 로드 밸런싱을 수행하는 <mark style="color:blue;">Overlay 네트워크</mark>이다.



