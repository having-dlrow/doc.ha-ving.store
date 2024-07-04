# - HTTP

## HTTP/0.9

```
GET /index.html

<html>
    Sample Page.
</html>
```

* TCP
* Body 가 본문인 심플한 상태
* (단점) 항상 새로운 연결을 맺어야 함

## HTTP/1.0

```
GET /index.html HTTP/1.0
User-Agent : Mozilla/5.0

200 OK
Date : Mon, 14 Dec 2000 00:00:00 GMT
Content-Type : text/html
<html>
    Sample Page.
</html>
```

* TCP
* `HEADER` 생김
* `CONTENT-TYPE` HTML 이외의 파일도 전송 가능.
* (단점 극복) hand-shaking
* (단점) 순차적 요청 처리
* (단점) HEADER 중복 발생



## HTTP/1.1 (1997)

*   (단점  극복) <mark style="color:red;">Persistent Connection</mark>

    * 전체 시간 ↓

    <figure><img src="../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>
*   (단점 극복) Pipelining

    * 응답을 기다리지 않고, 연속된 요청을 처리함

    <figure><img src="../../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>
* (새로운 단점)  Head Of Line Blocking
  * 연속된 요청 中 한 개의 요청이 길어지는 경우, 전체 요청이 지연

## HTTP/2

* Header&#x20;
*   (단점 극복) Binary Framing

    * Parsing, 전송 속도 ↑ , 오류 발생 가능성  ↓
      * `Frame`:  가장 작은 통신 단
      * `Message`  : 여러 Frame으로 구성된, HTTP 요청
      * `Stream` : Frame의 논리적 시퀀스를 의미

    <figure><img src="../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>
*   (단점 극복)  Multiplexing&#x20;

    * 메시지 단위의 처리가 아닌, 프레임 단위의 처리 순서로, 병렬 처리가 가능해짐
    * Stream 에 우선순위 가중치를 줄 수 있음

    <figure><img src="../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

## HTTP/3

* 2020
* UDP(QUIC)
  * 구글 YOUTUBE 등디미디어 파일을 겨냥한 방향
* 특징
  * 패킷 손실 회복
  * 재연결이 더 빠름
* 문제점&#x20;
  * CPU 사용이 큼



## NGINX

> Nginx 와 Backend 간은 HTTP/2가 지원이 안된다!

<figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

이유 :

* 내부 네트워크간 지연 시간이 짧다.
* keep-alive을 통해, connection을 재사용하므로, HTTP/2 지원이 필요하지 않다고 판단.

HTTP/3

* NGINX 1.25 (2023) 버전 부터 모듈 추가 하여 사용할 수 있게 되었다.
* `Alt-Svc`  헤더 값을 통해, 해당 서버가 HTTP/3 지원이 가능한지 확인 할  수 있으니, Nginx 설정에 add\_header 해줘야한다.
* Openssl  QUIC TLS 지원이 아직 안된다. ( BoringSSL  지원 가능 )
* UDP 방화벽을 열어야 한다.&#x20;
