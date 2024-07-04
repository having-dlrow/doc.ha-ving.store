# - SSL/TLS

## TLS

* <mark style="color:red;">SSL은 더이상 사용하지 않는다.</mark>
* TLS 은 SSL 3.0 기반에서 수정을 거쳤다.
* SSL  이름이 앞에 붙을 뿐, 실제 사용하는 것은 TLS 이다.
* <mark style="color:red;">SSL 인증서라고 하지만, 실제로는 TLS 인증서를 말하는 것이 맞다.</mark>
* 현재 TLS 1.2, TLS 1.3이 사용되고 있다.

## SSL

* Handshake , Change Cipher Spec Session 생성 3 단계로 이루어진다.

3 way Handshake

<table><thead><tr><th width="380">Client가 보냄</th><th>Server가 보냄</th></tr></thead><tbody><tr><td><ul><li>사용하는 TLS 버전</li><li>사용하는 암호화 목록</li><li>클라이언트_랜덤값</li></ul></td><td></td></tr><tr><td></td><td><ul><li>서버의 TLS 버전</li><li>선택된 암호화 목록</li><li>서버_랜덤값</li><li>서버 인증서 (서버_공개키 + CA_서명)</li></ul></td></tr><tr><td><p></p><p>CA 인증 기관 업데이트 중…</p><ul><li>인증서 확인 > OK > 서버_공개키 사용!</li><li>클라이언트_개인키 생성</li></ul></td><td></td></tr><tr><td><p></p><ul><li>서버_공개키(클라이언트_secret) 전송</li></ul><p></p></td><td></td></tr><tr><td><p></p><ul><li>세션 : Hash(클라이언트_secret ,<br>            (클라이언트_랜덤값+서버_랜덤값))</li></ul></td><td><p></p><p>서버_개인키(서버_공개키(클라이언트_secret))</p><ul><li>세션 : Hash(클라이언트_비밀키,<br>            (클라이언트_랜덤값+서버_랜덤값))</li></ul><p></p></td></tr><tr><td>change Cipher Spec<br>( 암호화 통신 시작!! )</td><td></td></tr><tr><td></td><td>finished ( handshake 끝!)</td></tr></tbody></table>



* 클라이언트와 서버는 세션을 유지합니다.&#x20;
* 동일한 세션 키를 사용하여 handshake 없이 통신 할 수 있습니다.&#x20;

## OCSP  프로토콜

Online Certificate Status Protocol ( 온라인 인증서 상태 프로토콜 )

* 브라우저에서인 CA에  인증서 유효성 확인 방법
* 실시간 확인
* `CRL` : 인증 기관이 주기적으로 취소된 인증서를 제공하는 방



### OCSP Stapling

브라우저에서 CA에 인증서를 확인함에 따라, 인증서 노출 위험이 증가하고, 트래픽 응답 지연등을 초래한다.

이를 해결하기 위해, 서버에서 OCSP을 진행하여, 함께 전달하는 방식

* 성능향상
* 신뢰성 향상



OCSP Stapling 과TLS

TLS 연결에 OCSP Stapling 이 사용된다.&#x20;

```apacheconf
#   nginx.conf

ssl_stapling on;
ssl_stapling_verify on;
```
