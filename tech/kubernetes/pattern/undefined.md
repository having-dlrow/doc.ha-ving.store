# 🏗️ 배치 전략

## 관심사의 분리

컨테이너 1개에 <mark style="color:blue;">하나의 관심사</mark>&#x20;

\| Best Practices for writing Dockerfiles :: Each Container should have only one concern



하지만,   <mark style="color:blue;">컨테이너 1개 ≠ 프로세스 1개</mark>

작업  수행 단위로 구성하자.   1개 프로세스 구성이 간결한 형태지만, 오히려 유지하기 어려울 수 있다.
