---
cover: https://seongjin.me/content/images/2022/08/wooden-raft.jpg
coverY: 0
---

# 🌵 ETCD

Key : value 형태의 데이터 저장 스토리지



## 기본 동작

Etcd 프로세스는 기본적으로 log entry를 메모리에 보관합니다. \
주기적으로 log entry를 파일시스템에 저장(snapshot) 하고, memory를 비우는 작업(truncate)을 합니다.





## RSM ( Replicated state machine )

* 똑같은 데이터를 여러 서버에 복제하는 것. 이 방법으로 사용하는 머신을 RSM이라 한다.
* command을 받은 순서대로 처리한다 -> 데이터 일치(consensus) 확보가 필요하다.
  * Raft 알고리즘을 사용한다. ( [raft.md](raft.md "mention") )



Kubernetes ETCD 데이터 조회

```
kubectl exec -it -n kube-system etcd-docker-desktop -- sh

etcdctl --endpoints=https://127.0.0.1:2379 \
        --cacert /run/config/pki/etcd/ca.crt \
        --cert /run/config/pki/etcd/server.crt \
        --key /run/config/pki/etcd/server.key \
        get "" --prefix --keys-only
        

```



Kubernetes ETCD 데이터 형태

{% code overflow="wrap" %}
```
etcdctl --endpoints=https://127.0.0.1:2379 \
        --cacert /run/config/pki/etcd/ca.crt \
        --cert /run/config/pki/etcd/server.crt \
        --key /run/config/pki/etcd/server.key \
        get "/registry/apiregistration.k8s.io/apiservices/v1.apps"

{"kind":"APIService","apiVersion":"apiregistration.k8s.io/v1","metadata":{"name":"v1.apps","uid":"cb5d885d-431b-4c07-8672-99eb6a36180a","creationTimestamp":"2024-07-25T14:58:57Z","labels":{"kube-aggregator.kubernetes.io/automanaged":"onstart"},"managedFields":[{"manager":"kube-apiserver","operation":"Update","apiVersion":"apiregistration.k8s.io/v1","time":"2024-07-25T14:58:57Z","fieldsType":"FieldsV1","fieldsV1":{"f:metadata":{"f:labels":{".":{},"f:kube-aggregator.kubernetes.io/automanaged":{}}},"f:spec":{"f:group":{},"f:groupPriorityMinimum":{},"f:version":{},"f:versionPriority":{}}}}]},"spec":{"group":"apps","version":"v1","groupPriorityMinimum":17800,"versionPriority":15},"status":{"conditions":[{"type":"Available","status":"True","lastTransitionTime":"2024-07-25T14:58:57Z","reason":"Local","message":"Local APIServices are always available"}]}}
```
{% endcode %}

* value 크기 제한 : 1.5MB (기본값)
  * `etcd --max-request-bytes=10485760`변경가능하지만, 메모리, 클러스터 노드 고려해야한다.

Ref&#x20;

* [https://tech.kakao.com/posts/484](https://tech.kakao.com/posts/484)







