# JWT

\[ 문제 ]

* JWT의 특징
* 쿠키, 세션 대비 JWT의 장점

\[ 정답 ]

*   JWT의 특징

    #### JWT 정의

    * 웹에서 사용되는 JSON 포맷의 토큰에 대한 표준 규격으로 주로 사용자의 인증, 인가 정보를 서버와 클라이언트 간에 안전하게 주고 받기 위해서 사용됨
    * JSON Web Token은 웹 표준(RFC 7519)로서 두 개체에서 JSON 객체를 사용하고 가벼우면서 자가 수용적(Self-contained) 방식으로 정보를 안정성 있게 전달
      * 자가 수용적 : JWT 안에 인증에 필요한 모든 정보를 자체적으로 지니고 있음

    #### 동작 프로세스



    #### JWT 구조

    * 각각 구분을 위해 .(컴마) 구분자가 들어감

    <figure><img src="../../../../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

    ![](<../../../../../.gitbook/assets/image (43).png>)

    * 헤더 (Header)
      * 두 가지 정보를 가짐
        * typ - 토큰의 타입 (JWT)
        * alg - 해싱 알고리즘
          * Signature를 해싱하기 위한 알고리즘 지정
    *   내용 (Payload)

        * 토큰에 담을 정보들이 존재하고 여기에 담는 정보의 한 조각을 `Claim`이라고 함
        * 클레임은 키값 형태로 존재
          * 클레임의 종류는 등록된(registered) 클레임, 공개(public) 클레임, 비공개 클레임 등이 있음

        ```json
            {
                "iss": "jh.com", // 등록된 클레임
                "exp": "1485270000000", // 등록된 클레임
                "<https://xxx.com/jwt_claims/is_admin>": true, // 공개 클레임
                "userId": "11028373727102", // 비공개 클레임
                "username": "jh" // 비공개 클레임
            }
        ```

    #### JWT 등장 배경

    * 인증에 필요한 정보가 토큰에 들어있었어서 별도의 저장소가 필요 없음
      * 하지만 보안성을 높이기 위해 `Refresh Token`을 사용하는 경우, 별도의 저장소에 저장하면서 사용하는 경우에 해당하지 않음
        *   Refresh Token 개념

            ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6b84eb4f-62e8-4f22-ac63-d5825ebb88e5/a4e68faa-5e3a-4dc7-b44c-66c1a1a39925/Untitled.png)
    * Cookie와 Session 사용시 문제점이었던 Stateful 특성을 JWT 사용시 Stateless하게 가져갈 수 있음
    * 다양한 언어에서 지원
    * HTTP 헤더에 넣어서 쉽게 전달 가능
    * MSA 환경에서 유용
*   쿠키, 세션 대비 JWT의 장점

    **쿠키**

    * 적은 용량과 보안 문제점 존재

    **쿠키 + 세션**

    * 쿠키의 문제점 해결
    * 문제점
      * 상태를 저장해야 하므로, 즉, 세션 정보를 저장하기 위한 추가 저장소가 필요
      * `Http Stateless` 특성을 위반
        * 즉, 로그인 할때마다 세션 스토리지(추가 저장소)에 접근해서 확인해야 함
      * 스케일 아웃시 여러 서버에 세션 정보를 복사해줘야하는 작업이 필요
      * 이를 해결하기 위한 개념인 스티키 세션, 세션 클러스터링이 등장했지만 여전히 `stateful`하다는 문제점은 해결 못함

    **JWT**

    * 클라이언트가 상태를 들고있을 필요 없이 토큰만으로 인증처리 가능. 즉, `Stateless`를 보장
    * MSA에서 중앙화된 인증방식에 비해 유리
    * 그러나 보안 문제로 `Refresh Token`을 도입하면 결국 이를 저장하기 위한 별도의 저장소가 필요한 것은 마찬가지
      * `Stateless`를 완벽하게 보장하지 못함
    * 하지만 세션은 로그인을 할때마다 저장소에 접근하고, JWT는 토큰이 만료되었을때만 저장소에 접근하므로 접근하는 횟수 자체는 상대적으로 적다는 장점이 있음
    * `Access Token`을 사용하는 기간 동안은 `Stateless`하지만, 만료되었을때는 `Stateless`가 깨지게 됨
    * MSA 환경에서 유용
