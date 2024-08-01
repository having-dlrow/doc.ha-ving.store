# Application Load Balancer

CLB : Classic Load Balancer

NLB : L4 Network Load Balancer

ALB : L7 Application Load Balancer



Kubernetes의 Ingress Resource을 통해 ALB을 생성한다.

ALB 에서 TLS Termination을 사용하고,&#x20;

모든 Request 을 Istio Ingress Gateway Pod로 전송한다.

Istio Ingress Gateway가 Application Service로 Routing 하게 된다.



