# 쿠버네티스는 systemd를 선호하고, docker는 cgroup을 선호한다

## 배경 지식

* 컨테이너 런타임은 cgroup을 사용하여, 컨테이너에 자원을 할당한다.
* cgroup을 관리하기 위한 기술 cgroupfs, systemd가 있다.
* \`/sysm/fs/cgroup\` 디렉토리에 파일 시스템 형태로 관리된다.
* cgroupfs는 정보를 파일 시스템 형태로 변환해주는 매니저이다.



### Kubernetes(Docker) cgroup 확인 하는 방법

<pre><code><strong>kubelet --version
</strong>docker info | grep Cgroup -F2
</code></pre>

### systemd vs cgroupfs

* cgroupfs
  * 디렉터리 하위에 리소스를 직접 매핑하는 구조
* systemd
  * 프로세스가 사용하는 자원을 관리
  * slice > scope > service  단위로 계층 구조를 만들어 각 단위에 자원을 할당

```
systemd-cgls

Control group /:
-.slice
├─kubepods
│ └─kubepods
│   ├─burstable
│   │ ├─pod91838c84176e55a239acd0e97bb0c8cf
│   │ │ ├─617333f8b19dfad902d685805859c17343b79f2226d88ff0136e1793f5046e4e
│   │ │ └─d783887e26b15bc54747655d187ad4cee2b1531af84de52a63b5737bd6b30b62
├─01-docker
├─init.scope
│ └─1 /sbin/init
├─system.slice
│ ├─snap-core22-1380.mount
│ │ └─272 snapfuse /var/lib/snapd/snaps/core22_1380.snap /snap/core22/1380 -o ro,nodev,allow_other,suid
│ ├─snap-snapd-19122.mount
│ │ └─304 snapfuse /var/lib/snapd/snaps/snapd_19122.snap /snap/snapd/19122 -o ro,nodev,allow_other,suid
│ ├─snap-go-10657.mount
│ │ └─287 snapfuse /var/lib/snapd/snaps/go_10657.snap /snap/go/10657 -o ro,nodev,allow_other,suid
│ ├─snap-helm-418.mount
│ │ └─294 snapfuse /var/lib/snapd/snaps/helm_418.snap /snap/helm/418 -o ro,nodev,allow_other,suid
│ ├─systemd-networkd.service
│ │ └─107 /lib/systemd/systemd-networkd
...skipping...
│ ├─snap-core20-1891.mount
│ └─1 /sbin/init
│ ├─systemd-networkd.service
│ │ └─107 /lib/systemd/systemd-networkd
│ ├─systemd-udevd.service
│ │ ├─   81 /lib/systemd/systemd-udevd
│ │ ├─43926 /lib/systemd/systemd-udevd
...skipping
│ ├─cron.service
│ │ └─384 /usr/sbi
```



## 쿠버네티스는 systemd를 선호하고, docker는 cgroup을 선호한다!?

{% hint style="danger" %}
쿠버네티스 v1.22 에서 부터 기본값은 systemd로 설정되었다.
{% endhint %}

{% hint style="success" %}
쿠버네티스 공식 문서에서 도커 18.03 + 커널 4.17.17 이하의 RHEL 에서는 cgroupfs에서 메모리 leaking issue가 발생하여 systemd로 변경하라고 권고한다.
{% endhint %}

{% hint style="success" %}
도커에서 cgroupfs를 cgroup v1에서만 사용, cgroup v2에서는 systemd로 변경할 계획이 있음을 밝혔다.
{% endhint %}

