# Kubernetes DNS

{% embed url="https://d2.naver.com/helloworld/2905424" %}

## A/AAAA Record 구성

* Service : \<service>.\<ns>.svc.\<zone>&#x20;
* Pod&#x20;
  * \<pod-ip>.\<ns>.pod.\<zone>
  * \<hostname>.\<service>.\<ns>.svc.\<zone>

## nodelocaldns

\*nodelocaldns : DNSCache 로 부터 생성된 임시 인터페이스

노드에서 DNS 참조 방식

```
/etc/resolv.conf
nameserver : 192.168.65.254
```

Pod 에서 DNS 참조 방식

```
/etc/resolv.conf
nameserver : 169.254.20.10
```

```
ip address

13: nodelocaldns <BROADCCAST,NOARP> mtu 1500
    inet 168.254.20.10
```



Calico





## CoreDns ( kube-dns <= 1.13 )

* Kubernetes 클러스터 내의 기본 DNS 서버
* 역할
  * Service, Pod 에 대한 DNS 레코드 생성 및 업데이트
  * Service DNS 쿼리 처리
  * 외부 도메인 쿼리 처리

```
root@DESKTOP-PTIJ6PV:~# kubectl get all -n kube-system
NAME                                         READY   STATUS    RESTARTS      AGE
pod/coredns-76f75df574-5jq2n                 1/1     Running   2 (14m ago)   6d12h
pod/coredns-76f75df574-rc7pk                 1/1     Running   2 (14m ago)   6d12h
pod/kube-proxy-ggfps                         1/1     Running   2 (14m ago)   6d12h

NAME               TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)                  AGE
service/kube-dns   ClusterIP   10.96.0.10   <none>        53/UDP,53/TCP,9153/TCP   6d12h

NAME                        DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR            AGE
daemonset.apps/kube-proxy   1         1         1       1            1           kubernetes.io/os=linux   6d12h

NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/coredns   2/2     2            2           6d12h

NAME                                 DESIRED   CURRENT   READY   AGE
replicaset.apps/coredns-76f75df574   2         2         2       6d12h
```



### CoreDNS 의 CoreFile 분석

```
root@DESKTOP-PTIJ6PV:~# kubectl describe cm coredns -n kube-system
Name:         coredns
Namespace:    kube-system
Labels:       <none>
Annotations:  <none>

Data
====
Corefile:
----
.:53 {
    errors
    health {
       lameduck 5s
    }
    ready
    kubernetes cluster.local in-addr.arpa ip6.arpa {
       pods insecure
       fallthrough in-addr.arpa ip6.arpa
       ttl 30
    }
    prometheus :9153
    forward . /etc/resolv.conf {
       max_concurrent 1000
    }
    cache 30
    loop
    reload
    loadbalance
}


BinaryData
====

Events:  <none>
```

* ready : 쿼리를 받을 준비가 되었음을 나타내틑 준비상태 정보
* kubernetes : Kubernetes 클러스터 내의 Pod 및 Service 에 대한 DNS 레코드를 자동으로 생성 및 관리&#x20;
* loadbalance : DNS 응답 내에서 A,AAAA, MX 레코드의 순서를 랜덤하게 재배치하여 부하 분산을 지원

### CoreDNS AutoScaler

* [https://kubernetes.io/docs/tasks/administer-cluster/dns-horizontal-autoscaling/](https://kubernetes.io/docs/tasks/administer-cluster/dns-horizontal-autoscaling/)&#x20;

&#x20;

