---
description: 시스템 커널 기능
---

# cgroup

배경 지식

* 컨테이너 런타임은 cgroup을 사용하여, 컨테이너에 자원을 할당한다.
* cgroup을 관리하기 위한 기술 cgroupfs, systemd가 있다.
* \`/sysm/fs/cgroup\` 디렉토리에 파일 시스템 형태로 관리된다.
* cgroupfs는 정보를 파일 시스템 형태로 변환해주는 매니저이다.



Kubernetes(Docker) cgroup 확인 하는 방법

<pre><code><strong>kubelet --version
</strong>docker info | grep Cgroup -F2
</code></pre>

## systemd vs cgroupfs

* cgroupfs
  * 디렉터리 하위에 리소스를 직접 매핑하는 구조
* systemd
  * 프로세스가 사용하는 자원을 관리
  * slice > scope > service  단위로 계층 구조를 만들어 각 단위에 자원을 할당

```
systemd-cglsasdg
```
