# 🧊 Test 환경 구축

Docker in Docker 환경에서 진행합니다.

### Install

docker-compose.yml

```bash
version : "3"
services : 
    registry : 
        container_name: registry
        image : registry:2.6
        ports :
            - 5000:5000
        volumes:
            - ".registry-data:/var/lib/registry"

    manager:
        container_name: manager
        image : docker:18.05.0-ce-dind
        privileged: true
        tty : true
        ports : 
            - 8000:80
            - 9000:9000
        depends_on : 
            - registry
        expose :
            - 3375
        command : "--insecure-registry registry:5000"
        volumes : 
            - "./stack:/stack"

    worker01:
        container_name: worker01
        image : docker:18.05.0-ce-dind
        privileged: true
        tty : true
        depends_on:
            - manager
            - registry
        expose: 
            - 7946
            - 7946/udp
            - 4789/udp
        command: "--secure-registry registry:5000"

    worker02: 
        container_name: worker02
        image : docker:18.05.0-ce-dind
        privileged: true
        tty : true
        depends_on:
            - manager
            - registry
        expose: 
            - 7946
            - 7946/udp
            - 4789/udp
        command: "--secure-registry registry:5000"

    worker03: 
        container_name: worker03
        image : docker:18.05.0-ce-dind
        privileged: true
        tty : true
        depends_on:
            - manager
            - registry
        expose: 
            - 7946
            - 7946/udp
            - 4789/udp
        command: "--secure-registry registry:5000"
```

```bash
docker-compose up -d
779ddcf362b3: Pull complete
Digest: sha256:b813c414ee36b8a2c44b45295698df6bdc3bdee4a435481dbb892e1b44e09d3b
Status: Downloaded newer image for docker:18.05.0-ce-dind
Creating registry ... done
Creating manager  ... done
Creating worker03 ... done
Creating worker01 ... done
Creating worker02 ... done
```

Docker Compose 사용하면  Stack이 생성된다.

Stack을 사용하면 Overlay 네트워크에 속하게 된다.



### Docker Registry Image

worker 컨테이너가 registry 컨테이너로 부터 도커 이미지 내려받을 수 있는지 확인

```bash
$ docker container exec -it worker01 docker image pull registry:5000/example/echo:latest
latest: Pulling from example/echo
3386e6af03b0: Pull complete
49ac0bbe6c8e: Pull complete
d1983a67e104: Pull complete
1a0f3a523f04: Pull complete
0aa12b6901d5: Pull complete
Digest: sha256:b218dbeecec09cfd1092d2caf08028468615bc079ae5ebb1f8df44bf4f765915
Status: Downloaded newer image for registry:5000/example/echo:latest

$ docker container exec -it worker01 docker image ls
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
registry:5000/example/echo   latest              60261e17016d        12 minutes ago      123MB
```



### Docker Swarm Init

1. manager 컨테이너 docker swarm init 명령어 실행하여, swarm manager 역활 부여

```bash
$ docker container exec -it manager docker swarm init
Swarm initialized: current node (6i3kjs56109gtt0ryog57fryr) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-17js6ztkccq0zznv9er9qh73wcc65ypdr78bpy3nuqehyzgfmf-31cq29t33ibj4sx7fo0l83qiu 172.18.0.3:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```

2. join 토큰을 사용해서 3대의 노드를 스웜 클러스터에 worker로 등록한다.&#x20;
3. manager 및 모든 worker 컨테이너는 Docker Compose 생성한 기본 네트워크 위에서 실행 된다.&#x20;

```bash
$ docker container exec -it worker01 docker swarm join \\
--token SWMTKN-1-099z1pgun3vbse5ljlny5gxejapxwp1y7iuikagkynyibrk50w-2vqeg5xoj1ariufbwxvpvifaw 172.18.0.3:2377
This node joined a swarm as a worker.

$ docker container exec -it worker02 docker swarm join \\
--token SWMTKN-1-099z1pgun3vbse5ljlny5gxejapxwp1y7iuikagkynyibrk50w-2vqeg5xoj1ariufbwxvpvifaw 172.18.0.3:2377
This node joined a swarm as a worker.

$ docker container exec -it worker03 docker swarm join \\
--token SWMTKN-1-099z1pgun3vbse5ljlny5gxejapxwp1y7iuikagkynyibrk50w-2vqeg5xoj1ariufbwxvpvifaw 172.18.0.3:2377
This node joined a swarm as a worker.
```



### 서비스 실행

```bash
$ docker container exec -it manager docker service create --replicas 1 --publish 8000:8080 --name echo registry:5000/example/echo:latest
rspmbrx9o0y0juddcgnyoda28
overall progress: 1 out of 1 tasks
1/1: running   [==================================================>]
verify: Service converged
```

```bash
$ docker container exec -it manager docker service scale echo=6
echo scaled to 6
overall progress: 2 out of 6 tasks
1/6: preparing [=================================>                 ]
2/6: preparing [=================================>                 ]
3/6: preparing [=================================>                 ]
4/6: running   [==================================================>]
5/6: preparing [=================================>                 ]
6/6: running   [==================================================>]

$ docker container exec -it manager docker service ls
ID                  NAME                MODE                REPLICAS            IMAGE                               PORTS
rspmbrx9o0y0        echo                replicated          6/6                 registry:5000/example/echo:latest   *:8000->8080/tcp
```



### 네트워크 생성

```bash
// network "ch03" is declared as external, but could not be found. You need to create a swarm-scoped network before the stack is deployed
$ docker container exec -it manager docker network create --driver=overlay --attachable ch03
ozdpwofpvmcb5ux9gsi321ad3
```



### 스택 배포하기

```bash
$ docker container exec -it manager docker stack deploy -c ./stack/webapi.yml echo
Creating service echo_api
Creating service echo_nginx
```

replicas : 3  배포 확인

```bash
$ docker container exec -it manager docker stack services echo
ID                  NAME                MODE                REPLICAS            IMAGE                               PORTS
re2d5jh039i4        echo_nginx          replicated          3/3                 gihyodocker/ngix-proxy:latest
v7kwryhfhbc2        echo_api            replicated          3/3                 registry:5000/example/echo:latest
```

:white\_check\_mark: 컨테이너에 1개만 배치 된 경우

&#x20;호스트 → manager → visualizer   ( _포트 포워드 방식_ )&#x20;

:white\_check\_mark: 컨테이너에 여러개가 배치된 경우

호스트 → manager -> haproxy -> visualizer  ( _proxy_ )

외부에서 오는 트래픽을 목적하는 서비스로 보내주는 프록시 서버 (HAPROXY) 설치
