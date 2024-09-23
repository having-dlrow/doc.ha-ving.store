# OAuth2.0

OAuth2.0 은 애플리케이션 인증 및 권한 부여를 위한 개방형 표준 프로토콜로 간단하게 설명하면 사용자가 자신의 아이디와 비밀번호를 직접 공유하지 않고 제 3자 애플리케이션에 서비스 접근 권한을 부여할 수 있습니다.

* 대표적으로 네이버, 카카오, 구글 로그인과 같은 소셜 미디어 간편 로그인이 있습니다.

## **Authorization Code Grant**

<div align="left">

<figure><img src="../../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

</div>

####

1. Authorization **Code, 클라이언트에게** 전달 ( 진짜 유효한 Client인지 확인 목적(해킹 방지) )
2. code 가지고 Authorization Server에 Access Token 받음
3. Access Token = ( 기존 ID + Password )



## 구현 단계 별

#### 코드 발급 ( 인증 )

1.  “카카오로 로그인” 버튼 클릭

    1. 카카오의 페이지

    <div align="left">

    <figure><img src="../../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="188"><figcaption></figcaption></figure>

    </div>


2. 카카오 개발자 센터에 등록한 /social/login/kakao?code=xxxxx 호출 해줌\
   ![](<../../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1).png>)
3.  social/login/kakao controller 에서 Access Token 요청 호출

    1. **{kakao.url/oauth/token}?client\_id=xxx\&response\_type=code\&redirect\_url={액세스토큰받는URL}**
    2. 응답 값

    ```java
    {  "access_token":"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
       "token_type":"bearer",
       "refresh_token":"yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
       "expires_in":43199,
       "scope":"Basic_Profile"
    }
    ```

#### 로그인을 진행하는 경우 ( 인가 )

1. Access Token으로 카카오에 Profile 호출
2. 카카오 정보 기반으로 나의 DB에서 User가 있는지 확인
   1. 없다 → 로그인 실패
   2. 있다 → **JWT 발급**

#### 회원 가입을 진행하는 경우 ( 인가 )

1. Access Token으로 카카오에 Profile 호출
2. 카카오 정보 기반으로 나의 DB에서 User가 있는지 확인 (가입 여부)
   1. 없다 → **신규 가입 (DB저장)**
   2. 있다 → 회원가입 실패

\[ 카카오로 다시 확인 ]

<figure><img src="../../../../../.gitbook/assets/image (5) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### JWT 토큰 방식 비교

| 로그인 행위   | UsernamePasswordAuthenticationFilter | 인증 필터 | 성공 → Access Token & Refresh Token 발급                                         |
| -------- | ------------------------------------ | ----- | ---------------------------------------------------------------------------- |
|          |                                      |       |                                                                              |
| 권한 체크 행위 | oncePerRequestFilter                 | 인가 필터 | 머리 달고 온 Access Token → 읽고\&DB조회 → SecurityContext Authentication 저장 → 페이지 접근 |

Refresh Token의 역할

* 액세스 토큰 보다 더 길게 유효한 정보 값
* 액세스 토큰 만료 후, 일정 기간 이내 재 토큰을 만드는 장치 ( 로그인 유지 )



#### 이외 Oauth2.0 방식

\<aside> 💡 Application = 내가 만든 Server Resource Server = 카카오 회원 Server

\</aside>

**Authorization Code Grant**

<figure><img src="../../../../../.gitbook/assets/image (6) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Implicit**

* 이렇게 카카오가 안해주니까, 이런 방식은 안쓴다.

<figure><img src="../../../../../.gitbook/assets/image (7) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Resource Owner Password**

* ID + PWD → Access Token 발급 형태
* Application (내가 만든 서버) , Resource Server 가 **같은 회사일 때**
*

    <figure><img src="../../../../../.gitbook/assets/image (8) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Client Credentials Flow

* 클라이언트가 직접 카카오 회원에 정보 요청 할 때
* 제휴사 API , 서버간 통신

<figure><img src="../../../../../.gitbook/assets/image (9) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Ref

* [https://developers.kakao.com/docs/latest/ko/kakaologin/common](https://developers.kakao.com/docs/latest/ko/kakaologin/common)
* [https://hoestory.tistory.com/32](https://hoestory.tistory.com/32)
* [https://jangjjolkit.tistory.com/26](https://jangjjolkit.tistory.com/26)
* [https://blog.naver.com/mds\_datasecurity/222182943542](https://blog.naver.com/mds\_datasecurity/222182943542)
