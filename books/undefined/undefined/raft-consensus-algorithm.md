# 뗏목 합의 알고리즘 ( Raft Consensus Algorithm )

2014년에 Diego Ongaro와 John Ousterhout가 ["In Search of an Understandable Consensus Algorithm"](https://raft.github.io/raft.pdf?ref=seongjin.me)이라는 논문을 통해 최초로 발표하였다. 이후 현재는 쿠버네티스(Kubernetes)의 etcd 클러스터, MongoDB의 레플리카 셋(replica set) 등 다양한 영역에 접목되어 활용되고 있다.



### 동작 원리 <a href="#eb-8f-99-ec-9e-91-ec-9b-90-eb-a6-ac" id="eb-8f-99-ec-9e-91-ec-9b-90-eb-a6-ac"></a>

뗏목 합의 알고리즘(Raft Consensus Algorithm)이 적용된 분산 시스템에서 모든 노드는 아래의 세 가지 중 하나의 상태를 가진다.

1. 리더
2. 팔로워
3. 후보
