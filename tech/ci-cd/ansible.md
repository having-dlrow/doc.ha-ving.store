# Ansible

## Ansible  특징

자동화 도구로, 구성 관리, 애플리케이션 배치, 작업 자동화에 사용 된다.&#x20;

동일한 명령을 여러 번 실행해도 결과는 한 번 실행했을 때와 동일하게 유지**(멱등성)**, 예측 가능한 상태 관리를 제공한다.

* YAML을 사용하여 구성 설정이 쉽다.
* SSH를 통해 관리, agent가 필요 없다.
* PUSH 기반 서비스
* **다양한 모듈 지원**

## Ansible  명령

{% hint style="info" %}
\-i (--inventory-file)              : 적용 될 호스트들에 대한 파일 정보 \
\-m (--module-name)          : 모듈 선택\
&#x20;\-k (--ask-pass)                    : 관리자 암호 요청\
&#x20;\-k (--ask-become-pass)    : 관리자 권한 상승 \
\--list-hosts                            : 적용되는 호스트 목록
{% endhint %}

### Basic Sample

```
$ ansible all -m ping
$ ansible all -m copy "src=./test.txt dest=/tmp"
```



## Ansible Configuration File

### ansible/hosts

: 연결 대상호스트 목록

```
[devops]
172.17.0.3
172.17.0.4
```

### ansible/ansible.cfg

: 환경 설정 파일
