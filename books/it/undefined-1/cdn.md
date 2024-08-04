# - CDN

## CDN

* AWS / CloudFront
* Akamai / CDN
* Cloudflare / CDN
* Azure / CDN

### 특징

* 정적 파일 및 이미지, 동영상 전송
* 콘텐츠 캐싱을 제공한다.
* 분산된 서버 중 가장 근접한 서버를 통해 콘텐츠를 전달 받는다.
* DDos, 고가용성, SSL/TLS 제공

### 전략

#### cache-control

* `public` : CDN Caching 가능, 브라우저 Caching 가능
* `private` : CDN Caching 불가, 브라우저 Caching 가능
* `max-age=<seconds>` : 브라우저가 N초후 호출시, 재검증 요청

```jsx
HTTP/1.1 200 OK 
Date: Fri, 12 Mar 2021 03:52:32 GMT 
Server: WSGIServer/0.2 CPython/3.8.0 
Content-Type: application/json 
Cache-Control: max-age=15 

{"firstName": "\\uad11\\ubbfc", "lastName": "\\uae40"} 
```

ex) 토스 \
&#x20;      `s-maxage=31536000, max-age=0`  : CDN 1년 저장, 브라우저 매번 재검증 요청

## Edge Computing

* AWS Lambda
* Google IOT Edge
* Azure IOT Edge

### 특징

* 주로 IOT 기기에 실시간 응답/분석 결과 등을 전달 한다.
* 지연 시간을 감소한다.
* 중앙의 서버에서 데이터를 처리 하지 않고, 로컬에서 처리하는 목적이다.

Ref&#x20;

* [https://www.akamai.com/ko/glossary/what-is-a-cloud-cdn](https://www.akamai.com/ko/glossary/what-is-a-cloud-cdn)
* [https://toss.tech/article/smart-web-service-cache](https://toss.tech/article/smart-web-service-cache)
