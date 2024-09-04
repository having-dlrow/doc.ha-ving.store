# Struct 구조

1. 중첩 불가

```
type ClusterSpec struct {
	Leader   RedisLeader   `json:"leader"`
	Follower RedisFollower `json:"follower,omitempty"`
}
```

Cluster 리소스 생성시, RedisLeader, RedisFollower 리소스가 생성되는 방법

\-> 독립적으로 RedisLeader, RedisFollower 리소스 생성이 되지 않고, Cluster 일부로 처리된다.



```
func CreateRedisCluster(c echo.Context, clientset versioned.Interface, req *model.ReplicasRequest) error {

	cluster := &v1.Cluster{
		TypeMeta: metav1.TypeMeta{
			Kind:       "Cluster",
			APIVersion: "redis.github.com/v1",
		},
		ObjectMeta: metav1.ObjectMeta{
			Name:      req.StatefulSetName,
			Namespace: req.Namespace,
		},
		Spec: v1.ClusterSpec{
			Leader: v1.RedisLeader{
				TypeMeta: metav1.TypeMeta{
					Kind:       "RedisLeader",
					APIVersion: "redis.github.com/v1",
				},
				ObjectMeta: metav1.ObjectMeta{
					Name:      req.StatefulSetName,
					Namespace: req.Namespace,
				},
				Spec: v1.RedisLeaderSpec{
					Foo: req.Image,
				},
			},
			Follower: v1.RedisFollower{
				TypeMeta: metav1.TypeMeta{
					Kind:       "RedisFollower",
					APIVersion: "redis.github.com/v1",
				},
				ObjectMeta: metav1.ObjectMeta{
					Name:      req.StatefulSetName,
					Namespace: req.Namespace,
				},
				Spec: v1.RedisFollowerSpec{
					Foo: req.Image,
				},
			},
		},
		Status: v1.ClusterStatus{},
	}

	// CreateOptions 설정
	createOptions := metav1.CreateOptions{}
	if os.Getenv("TEST_ENV") == "true" {
		createOptions.DryRun = []string{metav1.DryRunAll}
	}

	// StatefulSet 생성
	_, err := clientset.RedisV1().Clusters(req.Namespace).Create(c.Request().Context(), cluster, createOptions)
	_, err = clientset.RedisV1().RedisLeaders(req.Namespace).Create(c.Request().Context(), &cluster.Spec.Leader, createOptions)
	_, err = clientset.RedisV1().RedisFollowers(req.Namespace).Create(c.Request().Context(), &cluster.Spec.Follower, createOptions)
```

{% code overflow="wrap" %}
```
root@DESKTOP-PTIJ6PV:/home/workspace/api/kubernetes-api# kubectl get redisfollowers
NAME     AGE
redis5   7s
root@DESKTOP-PTIJ6PV:/home/workspace/api/kubernetes-api# kubectl get redisleaders
NAME     AGE
redis5   11s
root@DESKTOP-PTIJ6PV:/home/workspace/api/kubernetes-api# kubectl get cluster
NAME     AGE
redis5   12s

```
{% endcode %}

&#x20;생성시, TypeMeta을 넣어, 위와 같이 리소스가 생성되었다.

```
2024-08-20T21:45:15+09:00       INFO    Cluster Reconciliation started  {"controller": "cluster", "controllerGroup": "redis.github.com", "controllerKind": "Cluster", "Cluster": {"name":"redis5","namespace":"default"}, "namespace": "default", "name": "redis5", "reconcileID": "1849c94a-d22b-45b6-8df6-3181cda0b965", "Namespace": "default", "Name": "redis5"}
2024-08-20T21:47:10+09:00       INFO    Leader Reconciliation started   {"controller": "redisleader", "controllerGroup": "redis.github.com", "controllerKind": "RedisLeader", "RedisLeader": {"name":"redis5","namespace":"default"}, "namespace": "default", "name": "redis5", "reconcileID": "4a466697-6e11-4ae4-8868-3f5b90294f3a", "Namespace": "default", "Name": "redis5"}
2024-08-20T21:47:10+09:00       INFO    Follow Reconciliation started   {"controller": "redisfollower", "controllerGroup": "redis.github.com", "controllerKind": "RedisFollower", "RedisFollower": {"name":"redis5","namespace":"default"}, "namespace": "default", "name": "redis5", "reconcileID": "95822b1b-b6c6-49a7-813b-0aae506d2a05", "Namespace": "default", "Name": "redis5"}
```

Reconcile도 각자 실행되었다.
