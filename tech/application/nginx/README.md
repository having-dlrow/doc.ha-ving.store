# 🆗 Nginx

## Nginx

* master process , worker process, cache manager process 3개의 프로세스를 기동한다.

<details>

<summary>master process 이외를 기동하는 유저를 지정하는 부분이다. </summary>

* &#x20;master process는 root 유저로 기동하게 된다

```
# nginx.conf
user nginx;
```

</details>

<details>

<summary>nginx가 싱글스레드로 동작하기에, core 수를 맞춰 설정해놓는다.</summary>

```
# nginx.conf
worker_processes auto;     # core수 보다 높은 숫자를 저정해도 문제는 없다.
```

### CPU 코어 개수 확인

```
grep -c processor /proc/cpuinfo ll -d /sys/devices/system/cpu/cpu? | wc -l 
----------------
[root@zetawiki ~]# grep -c processor /proc/cpuinfo 48
```

### 물리 CPU 수

```
grep ^processor /proc/cpuinfo | wc -l
------------------
[root@zetawiki ~]# dmidecode -t processor | grep 'Socket Designation' 	Socket Designation: CPU 0 	Socket Designation: CPU 1 
```

### CPU당 물리 코어 수

```
grep 'cpu cores' /proc/cpuinfo | tail -1
-----------------
[root@zetawiki ~]# grep 'cpu cores' /proc/cpuinfo | tail -1 cpu cores	: 6 
```

</details>



## 용어

* `API` : HTTP를 통한 비 공개용 내/외부 호출 체계
* `OpenAPI` : HTTP를 통한 외부 공개용 호출 체계
* `모듈(Module)` : Server Side Script(PHP 등) 기반의 기능성 단위 프로그램(예, 게시판, 팝업관리 등)
* `브릿지(Bridge)` : 외부 서비스와의 Server Side Script(PHP 등) 연결 체계(예, 빌더와 제로보드 연동)
* `플러그인(Plugin)`  : JavaScript 기반의 외부 서비스 비동기 연결 체계(예, Google Map 등)

### CGI

<details>

<summary>웹서버와 외부 프로그램을 연결해주는 표준화된 프로토콜</summary>

웹서버로 요청이 들어왔을 때 그것이 웹서버가 처리 할 수 없는 정보일 때 그 정보를 처리 할 수 있는 외부 프로그램을 호출해서 외부 프로그램이 처리한 결과를 웹서버가 받아서 브라우저로 전송하는 것이다.

</details>

<figure><img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/384/1398.gif" alt=""><figcaption></figcaption></figure>

### FastCGI

<details>

<summary>FastCGI는 요청이 있을 때마다 프로세스가 만들어지는 것이 아니라 만들어진 프로세스가 계속해서 새로운 요청들을 처리한다.</summary>

CGI 는 하나의 요청(Request)에 하나의 프로세스를 생성한다. 이것은 프로세스를 생성하고 삭제하는 과정에서 많은 부하가 발생한다.

PHP-FPM : PHP를 FastCGI 모드로 동작하도록 해준다.

</details>

<figure><img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/384/1397.gif" alt=""><figcaption></figcaption></figure>
