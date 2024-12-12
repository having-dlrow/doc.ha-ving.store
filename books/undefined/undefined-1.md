---
description: >-
  https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART003067161
---

# 쿠버네티스 환경에서 컨테이너 워크플로의실행 시간 개선을 위한 컨테이너 재시작 감소 기법

논문 게시일:  2023.10

\[ 요약 ]&#x20;

***

## 1. 서론

<details>

<summary>VM 기술은 리소스 활용도가 낮고, 탄력적 확장 및 클러스터 확장 에 많은 시간이 소요된다<br><mark style="background-color:blue;">컨테이너 애플리케이션을 오버프로비저닝하는 경향(리소스 부족 재시작 방지를 위해)</mark></summary>

* 오버프로비저닝은 시스템 리소스의( CPU, 메모리) 활용률을 낮아지게 만든다.

- 지나친 메모리 리소스 초과 사용은 노드의 메모리 부족으로 인해\
  연쇄적인 컨테이너 재시작을 유발할 수 있다

* 메모리 변동성이 높은 컨테이너(상태저장 애플리케이션) 큰 오버헤드를 유발할 수 있다

</details>

<details>

<summary>쿠버네티스, 메모리 초과 사용 시 <mark style="background-color:blue;">컨테이너 재시작을 완화하는 기법</mark>을 제안</summary>

1. 메모리 사용량이 많은 노드에서 메모리 할당을 요청할 가능성이 큰 컨테이너를 식별하고 이러한 컨테이너를 일시정지한다

2) 컨테이너의 CPU 사용량을 크게 줄이면 컨테이너가 일시정지하는 상태와 유사한 효과를 얻을 수 있다

3. 해당 노드의 메모리 사용량이 개선된 것으로 판단되면 컨테이너의 일시정지를 해제한다.

</details>

컨테이너의 재시작 횟수가 평균 40%, 최대 58% 감소하였다.



## 2. 쿠버네티스의 자원관리 방식 및 한계점

<div align="left"><figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure></div>

* kubelet은 containerd를 목적지로 하는 CRI-API를 호출하여 \
  컨테이너의 생성 및 삭제와 같은 관리 작업을 수행
* kubescheduler는 파드의 request 값이 아닌,\
  노드에 배포된 파드들의 request 값의 합을 기준으로 스케줄링
* 파드 request 값  (= 최소필요값)

<div align="left"><figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure></div>

* <mark style="background-color:orange;">모든 컨테이너는 정의된 limit 값에 근접하는 리소스를 요구하지 않을 것이라고 가정한다 (한계점1)</mark>
* 물리적인 메모리보다 초과하여 메모리 할당을 요구하는 컨테이너가 있으면 \
  우선순위에 따라 컨테이 너를 강제 종료한다.
* <mark style="background-color:orange;">리소스 초과 사용은 노드의 메모리 가용량 부족 시 해당 노드에 있는 일부 파드는 노드의 메모리 대역폭 확보를 위해 반드시 재시작되어야 한다.(한계점2)</mark>
* <mark style="background-color:orange;">기계학습, 빅데이터 등을 활용하 는 데이터 집약적이고 메모리 변동성이 큰 상태저장 애플리케 이션은 재시작 발생 시 처음부터 작업을 다시 시작해야 하므 로 재시작으로 인한 오버헤드가 매우 크다 (한계점3)</mark>

### 파드 재시작을 위한 CrashLoopBackOff 루틴

컨테이너 재시작은 최대 300초로 제한된 지수 백오프(exponential back-off) 지연(10초, 20초, 40초, 80 초...) 시간을 순차적으로 가지며 재시작을 수행한다.

<mark style="background-color:orange;">만약 10 분 동안 이상 없이 동작하면 지수 백오프 지연시간은 초기화 된다.</mark>&#x20;



### 메모리 관리 한계점 해결 방안

1. swap 사용
2. ELASTICDOCKER (Dhuraibi)
3. RUBAS (Rattihalli)
4. 해당 연구



## 3. 연구 내용

3.1&#x20;
