# Computing

## EC2

<mark style="color:orange;">"Region 간 AutoScaling은 불가, AZ 간은 가능"</mark>

* Auto Scaling Group (free)
* 예약 인스턴스 : 약정 요금제 개념&#x20;
  * 1년 또는 3년 단위 약정
* onDemand : AZ 단위, AZ에 필요한 양이 없을 수 있으니 예약하는 개념
* 절전 모드 : 인스턴트의 메모리에 저장된 내용을 EBS에 저장후, 다시 로드하는 개념
* secondary Elastic Network Interface
  * 다른 EC2인스턴스에 연결 가능
  * 장애 발생 시, 대기 EC2인스턴스로 연결하는 개념
* storage
  * EBS : 네트워크 연결되는 블록 스토리지 ( USB stick 같은 개념 )
  * EC2 인스턴스 스토어 : IO 성능이 좋은 임시 스토리지, 캐시/버퍼 같은 임시 저장용
  * EFS : 확장가능한  NFS , 동시액세스지원,   S3에비해비쌈&#x20;



## ELB (Elastic Load Balancer)

### ALB ( Application Load Balancer )&#x20;

* L7 로드밸런서 ( HTTP/HTTPS )   : IP주소 + 포트 번호 + 패킷 내용&#x20;
* URL (/users, /posts) 에 따라 routing
* URI (git.example.com, harbor.example.com)에 따라 routing
* container 기반 application 또는 MSA(Docker)에 적합

### NLB ( Network Load Balancer )

* &#x20;L4 로드밸런서 ( TCP/IP ) : IP 주소 + 포트번호
* 고정 IP 지원

### GWLB&#x20;

* 침입탐지 방지



## CloudFront ( CDN )

* ddos 보호 , cache
* 정적 파일인 경우 유리
* origin
  * s3 bucket
  * http: alb, ec2



<table data-header-hidden><thead><tr><th width="139"></th><th></th><th></th></tr></thead><tbody><tr><td><strong>항목</strong></td><td><strong>CloudFront</strong></td><td><strong>S3 Cross-Region Replication</strong></td></tr><tr><td><strong>기능</strong></td><td>콘텐츠를 전 세계의 엣지 로케이션으로 캐시하여 사용자가 가장 가까운 위치에서 빠르게 제공.</td><td>S3 버킷의 객체를 지정된 다른 AWS 리전의 S3 버킷으로 복제하여 데이터의 가용성 및 지리적 분산을 지원.</td></tr><tr><td><strong>주요 목적</strong></td><td>웹사이트, 애플리케이션, 동영상 스트리밍 등의 정적/동적 콘텐츠 전송 속도 향상 및 대기 시간 감소.</td><td>데이터의 고가용성, 재해 복구, 지리적 데이터 동기화 및 규정 준수를 위해 S3 버킷 간 복제.</td></tr><tr><td><strong>동작 방식</strong></td><td>- 요청에 따라 엣지 로케이션에서 캐시된 데이터 제공.<br>- 캐시 만료 시 원본 S3 또는 웹 서버에서 데이터 가져오기.</td><td>- S3 버킷 간 자동 복제.<br>- 이벤트 기반으로 새로운 객체나 업데이트된 객체를 대상으로 실행.</td></tr><tr><td><strong>대상 데이터</strong></td><td>정적 웹 콘텐츠, 이미지, 동영상, JavaScript, CSS 등.</td><td>모든 S3 객체 (단, 복제 규칙을 통해 특정 프리픽스나 태그로 필터링 가능).</td></tr><tr><td><strong>속도 및 대기 시간</strong></td><td>엣지 로케이션 캐싱으로 빠른 데이터 제공, 대기 시간 최소화.</td><td>복제는 백그라운드에서 수행되며, 복제 시간은 네트워크 상태와 객체 크기에 따라 다름.</td></tr><tr><td><strong>비용 구조</strong></td><td>데이터 전송 비용 및 요청 수에 따라 비용 발생.<br>- 엣지 로케이션에서의 데이터 전송 비용.</td><td>복제 대상 데이터의 데이터 전송 비용 및 요청 수에 따라 비용 발생.<br>- 복제된 데이터 저장 비용 추가.</td></tr><tr><td><strong>설정 난이도</strong></td><td>- 간단한 원본 설정 (S3, EC2, 또는 커스텀 HTTP 서버).<br>- 캐시 제어 정책 설정 필요.</td><td>- 복제 규칙 생성 필요.<br>- 원본 및 대상 버킷에서 복제 역할(권한) 설정 필요.</td></tr><tr><td><strong>주요 이점</strong></td><td>- 글로벌 사용자에 대한 콘텐츠 제공 속도 향상.<br>- DDoS 방어 (AWS Shield 통합).<br>- HTTPS 지원.</td><td>- 데이터의 가용성과 내구성 보장.<br>- 멀티 리전 복제 통해 재해 복구 기능 제공.<br>- 법적/규정 준수를 위한 데이터 위치 설정 가능.</td></tr><tr><td><strong>사용 사례</strong></td><td>- 전 세계적인 웹 콘텐츠 배포.<br>- 동영상 스트리밍.<br>- API 응답 캐싱.</td><td>- 재해 복구를 위한 데이터 복제.<br>- 규제 요구사항을 충족하기 위한 데이터 복제.<br>- <mark style="color:red;"><strong>지리적으로 분산된 애플리케이션의 데이터 동기화.</strong></mark></td></tr><tr><td><strong>제약 사항</strong></td><td>- 동적 콘텐츠는 캐싱 정책에 따라 성능이 제한될 수 있음.<br>- 캐시 적중률에 따라 성능 변화 가능.</td><td>- 복제는 리전 간에만 가능 (같은 리전 내 복제 불가).<br>- 버킷 버전 관리 활성화 필요.<br>- 이미 존재하는 데이터는 복제되지 않음.</td></tr></tbody></table>

동적 파일을 사용하며, low-latency가 보장되어야 하는 경우, s3의 Cross Region Replication을 사용한다



