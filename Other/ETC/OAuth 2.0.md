# OAuth 2.0

OAuth 는 access token을 얻는 것

## 역할

3개의 주체

* Resource Server: 인증 서버 (+Authorization Server)
* Resource Owner: 사용자
* Client: 클라이언트
  

## 등록

공통 요소

* Client ID
  * 애플리케이션 식별 ID
* Client Secret
  * 애플리케이션 식별 비밀번호
* Authorized redirect URIs
  * 리소스 서버가 권한 부여 과정에서 Authorization code 주는데 그거 받을 주소



## Resource Owner의 승인

리소스 서버가 A, B, C, D 기능 가질 때, 전부 인증 받을 필요 없고 유저는 이 중 선택할 수 있다.

페이스북에 글을 작성하거나, 구글 캘린더를 작성하려 할 때

페이스북 로그인, 구글 로그인 등의 버튼을 볼 수 있다.

사용자가 동의를 해야 다음으로 진행할 수 있다.

![image-20231101142802246](/Users/nocturne9no1/Library/Application Support/typora-user-images/image-20231101142802246.png)

scope는 사용하려는 기능

리소스 오너가 리소스 서버에 요청 보낸다.

로그인 안되어있으면 로그인 창 보여줌

리다이렉트 주소 다르면 진행 멈춤

![image-20231101142915727](/Users/nocturne9no1/Library/Application Support/typora-user-images/image-20231101142915727.png)

이후 클라이언트가 요청하는 정보 허용할 것인지 물어봄

허용했다는 정보 리소스 서버로 보냄

![image-20231101142940439](/Users/nocturne9no1/Library/Application Support/typora-user-images/image-20231101142940439.png)

동의 했다는 정보를 리소스 서버가 얻게 됨



## Resource Server의 승인

access token 발급 전 하나 더 해야함

authorization code 를 리소스 오너에게 보낸다

![image-20231101143032533](/Users/nocturne9no1/Library/Application Support/typora-user-images/image-20231101143032533.png)

`?code=3` 이 authorization code

여기서 코드가 클라이언트로 전달됨

![image-20231101143121501](/Users/nocturne9no1/Library/Application Support/typora-user-images/image-20231101143121501.png)

authorization code와 client secret을 통해 자신임을 알림

리소스 서버는 클라이언트가 전송한 authorization code, client secret, redirect URL 일치하면 access token 발급



## 액세스 토큰 발급

![image-20231101143340535](/Users/nocturne9no1/Library/Application Support/typora-user-images/image-20231101143340535.png)

액세스 토큰을 클라이언트에 응답해줌

액세스 토큰은 클라이언트가 4라는 액세스 토큰으로 접근하면 유효한 기능을 제공한다.



## API 호출

해당 영상은 인증 서버 쪽 리소스를 요청하는 API에 대해 서술하고 있기에 생략



## refresh token

액세스 토큰은 수명이 있음

수명이 되면 api가 데이터를 주지 않음

이때 refresh token을 사용하여 액세스 토큰 갱신