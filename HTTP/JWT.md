## 01. 쿠키와 세션

[2.3-1-1_exported.mp4](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d66d3063-905d-444b-a644-c7e108a7d19c/2.3-1-1_exported.mp4)

- 1) 쿠키와 세션이란?
    - **쿠키(Cookie)**: 브라우저가 서버로부터 응답으로 Set-Cookie 헤더를 받은 경우 해당 데이터를 저장한 뒤 모든 요청에 포함하여 보냅니다.
        - 데이터를 여러 사이트에 공유할 수 있기 때문에 보안에 취약할 수 있습니다.
        - 쿠키는 `userId=user-1321;userName=sparta` 와 같이 문자열 형식으로 존재하며 쿠키 간에는 세미콜론`(;)` 으로 구분됩니다.
    - **세션(Session):** 쿠키를 기반으로 구성된 기술입니다. 단, 클라이언트가 마음대로 데이터를 확인 할 수 있던 쿠키와는 다르게 세션은 데이터를 **서버**에만 저장하기 때문에 보안이 좋으나, 반대로 사용자가 많은 경우 서버에 저장해야 할 데이터가 많아져서 서버 컴퓨터가 감당하지 못하는 문제가 생기기 쉽습니다.
- 2) 쿠키(Cookie) 만들어보기
    
    서버가 클라이언트의 HTTP 요청(Request)을 **수신**할 때, 서버는 응답(Response)과 함께 `Set-Cookie` 라는 헤더를 함께 **전송**할 수 있습니다. 그 후 쿠키는 해당 서버에 의해 만들어진 요청과 Cookie HTTP 헤더안에 포함되어 전달받습니다.
    
    그렇다면 `‘/set-cookie’`API를 호출했을 때 `name=sparta` 라는 쿠키를 할당하는 API를 만들어 볼까요?
    
    - `Set-Cookie` 를 이용하여 쿠키 할당하기
        
        ```jsx
        app.get("/set-cookie", (req, res) => {
          const expire = new Date();
          expire.setMinutes(expire.getMinutes() + 60); // 만료 시간을 60분으로 설정합니다.
        
          res.writeHead(200, {
            'Set-Cookie': `name=sparta; Expires=${expire.toGMTString()}; HttpOnly; Path=/`,
          });
          return res.status(200).end();
        });
        ```
        
    - `res.cookie()`를 이용하여 쿠키 할당하기
        
        ```jsx
        app.get("/set-cookie", (req, res) => {
          const expires = new Date();
          expires.setMinutes(expires.getMinutes() + 60); // 만료 시간을 60분으로 설정합니다.
        
          res.cookie('name', 'sparta', {
            expires: expires
          });
          return res.status(200).end();
        });
        ```
        
    
    ![스크린샷 2022-07-05 오전 2.39.20.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a38da1d4-63ad-4c75-a035-1a8d25bf62f6/스크린샷_2022-07-05_오전_2.39.20.png)
    
- 3) req를 이용하여 쿠키 접근하기
    
    일반적으로 쿠키는 `req.headers.cookie`에 들어있습니다. `req.headers`는 클라이언트가 요청한 Request의 헤더를 의미합니다.
    
    `/get-cookie`에 접근했을 때, 설정된 쿠키를 출력하는 API를 만들어볼까요?
    
    ```jsx
    app.get("/get-cookie", (req, res) => {
      const cookie = req.headers.cookie;
      console.log(cookie); // name=sparta
      return res.status(200).json({ cookie });
    });
    ```
    
    - `req.headers`에서 전달된 쿠키를 출력하는 예제입니다.
- 4) cookie-parser 미들웨어 적용하기
    
    쿠키를 사용하기 위해서는`req.headers.cookie`와 같이 여러 프로퍼티를 넘어서야 사용할 수 있었습니다.
    
    💡 여기서! cookie-parser 미들웨어는 요청에 추가된 쿠키를 `req.cookies` 객체로 만들어 줍니다. 더이상 `req.headers.cookie`와 같이 번거롭게 사용하지 않아도 되겠죠?
    
    **cookie-parser 미들웨어**를 전역으로 사용하기 위해서는 다음과 같이 사용합니다.
    
    ```jsx
    app.use(cookieParser());
    ```
    
    그렇다면 cookie-parser를 이용해 쿠키를 출력하는 API를 수정해볼까요?
    
    ```jsx
    const cookieParser = require('cookie-parser');
    app.use(cookieParser());
    
    app.get("/get-cookie", (req, res) => {
      const cookie = req.cookies;
      console.log(cookie); // { name: 'sparta' }
      return res.status(200).json({ cookie });
    });
    ```
    
    **cookie**를 불러오는 부분을 `req.cookies`로 변경되었고, **cookie**의 형식이 `name=sparta`가 아니라 **객체 형식**으로 바뀌었습니다. 좀 더 사용하기 쉬워졌죠?
    
    <aside>
    👉 cookie-parser는 단순히 쿠키를 `req.cookies`로 만들어 주기만 하는것이 아니라 더욱 쿠키를 손쉽게 사용할 수 있도록 도와주는 라이브러리 입니다. 더욱 자세한 내용을 확인하고 싶다면 [npm 문서](https://www.npmjs.com/package/cookie-parser)를 확인해보세요! 😎
    
    </aside>
    
- 5) 세션(Session) 만들어보기
    
    쿠키의 경우 서버를 재시작하거나 새로고침을 하더라도 로그인이 유지됩니다. 사용자의 입장에서는 편하게 사용할 수 있지만 서버의 입장에서는 상당히 위험한 상황입니다. 쿠키가 조작되거나 노출되어 보안적으로 문제가 발생할 수 있습니다.
    
    그렇다면 쿠키에는 어떠한 정보를 넣어줘야 할까요? 서버에서 해당하는 사용자가 누구인지 확실하게 구분할 수 있는 정보만 있다면 서버에서 해당 **사용자의 유니크한 정보**도 반환할 수 있겠죠?
    
    `/set-session` API를 호출했을 때 `name=sparta` 의 정보를 서버에 저장하고, 저장한 시점의 시간 정보를 쿠키로 반환받는 API와 
    
    `/get-session` API를 호출했을 때 쿠키의 시간 정보를 이용하여 서버에 저장된 name 정보를 출력하는 API를 만들어보겠습니다.
    
    - `/set-session` API 만들기
        
        ```jsx
        let session = {};
        app.get('/set-session', function (req, res, next) {
          const name = 'sparta';
          const uniqueInt = Date.now();
          session[uniqueInt] = { name };
        
          res.cookie('sessionKey', uniqueInt);
          return res.status(200).end();
        });
        ```
        
        - 서버에 해당하는 유저의 정보를 저장하기 위한 `session`객체를 만들었습니다.
        - `/set-session` API를 호출했을 때 `name=sparta`의 정보를 session에 삽입하고, 해당하는 데이터를 불러들이기 위한 시간 정보를 쿠키로 반환받습니다.
    - `/get-session` API 만들기
        
        ```jsx
        app.get('/get-session', function (req, res, next) {
          const { sessionKey } = req.cookies;
          const name = session[sessionKey];
          return res.status(200).json({ name });
        });
        ```
        
        - 쿠키에 저장된 `sessionKey`를 이용하여 `session`에 저장된 데이터를 불러옵니다.
    - API 전체 코드
        
        ```jsx
        const express = require('express');
        const cookieParser = require('cookie-parser');
        
        const app = express();
        app.use(cookieParser());
        
        let session = {};
        app.get('/set-session', function (req, res, next) {
          const name = 'sparta';
          const uniqueInt = Date.now();
          session[uniqueInt] = { name };
        
          res.cookie('sessionKey', uniqueInt);
          return res.status(200).end();
        });
        
        app.get('/get-session', function (req, res, next) {
          const { sessionKey } = req.cookies;
          const name = session[sessionKey];
          return res.status(200).json({ name });
        });
        
        app.listen(5002, () => {
          console.log("서버가 켜졌어요!");
        });
        ```
        
- 6) 연습문제
    
    `GET` Method로 `[http://localhost:5001/set](http://localhost:5001/set)`을 호출했을 때, **name**에 **nodejs**가 저장된 쿠키를 할당하고
    
    `GET` Method로`[http://localhost:5001/](http://localhost:5001/set)get`을 호출했을 때, 쿠키에 등록된 정보들이 반환되는 API를 만들어주세요!
    
    - 정답
        
        ```jsx
        const express = require("express");
        const cookieParser = require('cookie-parser');
        
        const app = express();
        app.use(cookieParser());
        
        app.get("/set", (req, res) => {
          res.cookie('name', 'nodejs');
          return res.status(200).end();
        });
        
        app.get("/get", (req, res) => {
          const cookie = req.cookies;
          return res.status(200).json({ cookie });
        });
        
        app.listen(5001, () => {
          console.log("서버가 켜졌어요!");
        });
        ```
        

## 02. JWT가 무엇인가요?

[심화2-2_JWT가 무엇인가요.mp4](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/043dd665-3d46-4b37-a944-5563032b9491/2-2_JWT_.mp4)

- 1) 간략한 정리!
    - JSON 형태의 데이터를 안전하게 교환하여 사용할 수 있게 해줍니다.
    - 인터넷 표준으로서 자리잡은 규격입니다.
    - 여러가지 암호화 알고리즘을 사용할 수 있습니다.
    - `header.payload.signature` 의 형식으로 3가지의 데이터를 포함합니다. (개미처럼 머리, 가슴, 배)
    때문에 JWT 형식으로 변환 된 데이터는 항상 2개의 `.` 이 포함된 데이터여야 합니다.
- 2) 어떻게 생긴건가요?
    
    ![jwt - Header, Payload, Signature](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4ade6645-2ee4-4233-98d9-c9f468eed8d4/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-09_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_5.55.01.png)
    
    jwt - Header, Payload, Signature
    
    [https://jwt.io/](https://jwt.io/) 에서 간단히 확인할 수 있는데요, 위에서 말했듯이 개미처럼 머리, 가슴, 배와 같은 3가지를 가졌습니다.
    
    - **header**(머리)는 signature(배)에서 어떤 암호화를 사용하여 생성된 데이터인지 표현합니다.
    - **payload**(가슴)는 개발자가 원하는 데이터를 저장합니다.
    - **signature**(배)는 이 토큰이 변조되지 않은 정상적인 토큰인지 확인할 수 있게 도와줍니다.
- 3) 더 알아두어야 할 특성
    - JWT는 암호 키를 몰라도 Decode가 가능합니다.
    변조만 불가능 할 뿐, **누구나 복호화**하여 보는것은 가능하다는 의미가 됩니다!
    - 때문에 민감한 정보(개인정보, 비밀번호 등)는 담지 않도록 해야합니다.
    - 특정 언어에서만 사용 가능한것은 아닙니다!
    단지 개념으로서 존재하고, 이 개념을 코드로 구현하여 공개된 코드를 우리가 사용하는게 일반적입니다.
- 4) 쿠키, 세션과 어떻게 다른가요?
    
    데이터를 교환하고 관리하는 방식인 쿠키/세션과 달리, **JWT는** 단순히 데이터를 표현하는 형식입니다.
    
    - JWT로 만든 데이터를 브라우저로 보내도 쿠키처럼 자동으로 저장되지는 않지만, 변조가 거의 불가능하고 서버에 데이터를 저장하지 않기 때문에 서버를 Stateless(무상태)로 관리할 수 있기 때문에 최근 많이 쓰이는 기술중 하나입니다.
    - Stateless(무상태)와 Stateful(상태 보존)의 차이를 간단히 설명하자면,
    Node.js 서버가 언제든 죽었다 살아나도 똑같은 동작을 하면 **Stateless**하다고 볼 수 있습니다.
    반대로 서버가 죽었다 살아났을때 조금이라도 동작이 다른 경우 **Stateful**하다고 볼 수 있겠죠.
    - 서버가 스스로 어떤 기억을 갖고 다른 결정을 하냐 마냐의 차이라고 보면 더 쉽습니다 😉
    - 로그인 정보를 서버에 저장하게 되면 무조건 **Stateful**(상태 보존)이라고 볼 수 있죠!

## 03. JWT는 어떻게 사용하면 되나요?

[심화2-3_JWT 사용 방법.mp4](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c214f531-ab52-43ec-acb5-f33323561909/2-3_JWT__.mp4)

- 1) 오픈소스 라이브러리를 이용합니다.
    
    우리는 제일 사용량이 많은 [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken) 라이브러리를 사용해볼게요!
    
    프로젝트로 이용할 폴더를 생성하고, 모듈을 설치해줍니다!
    
    ```bash
    npm init
    npm i jsonwebtoken -S
    ```
    
    프로젝트가 있는 경로에서 위 명령어로 우리가 필요한 모듈을 설치합니다!
    
- 2) 우리가 원하는 JSON 데이터를 암호화합니다.
    - 데이터를 암호화 해봅니다!
        
        ```jsx
        const jwt = require("jsonwebtoken");
        
        const token = jwt.sign({ myPayloadData: 1234 }, "mysecretkey");
        console.log(token);
        ```
        
        - 개발자인 우리가 담을 데이터는 Payload에 담긴다고 했죠? [jwt.io](http://jwt.io) 에서도 아래처럼 데이터를 입력하면 인코딩 된 데이터를 볼 수 있습니다!
    - 위처럼 코드를 작성하고 실행하면 어떤 화면이 보이나요?
    저와 같다면 `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJteVBheWxvYWREYXRhIjoxMjM0fQ.6XFgtNglH9hIzz5y8jAcI0g5kDnlAvnTTbxKIcL2CHY` 이와 똑같은 데이터가 출력되어야 합니다!
- 3) 복호화를 해봅니다!
    - 코드로 복호화해서 출력해봅시다!
        
        ```jsx
        const jwt = require("jsonwebtoken");
        
        const token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJteVBheWxvYWREYXRhIjoxMjM0fQ.6XFgtNglH9hIzz5y8jAcI0g5kDnlAvnTTbxKIcL2CHY";
        const decodedValue = jwt.decode(token);
        ```
        
        앞서 말했듯이 JWT는 누구나 복호화가 가능해요!
        그러나 검증을 통해 변조가 되지 않은 데이터인지 알 수 있죠!
        
    - 복호화가 아닌, 변조되지 않은 데이터인지 검증해봅시다
        
        ```jsx
        const jwt = require("jsonwebtoken");
        
        const token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJteVBheWxvYWREYXRhIjoxMjM0fQ.6XFgtNglH9hIzz5y8jAcI0g5kDnlAvnTTbxKIcL2CHY";
        const decodedValue = jwt.verify(token, "myesecretkey");
        ```
        
        만약 변조된 코드라면 위의 코드에서 에러가 발생할거예요!
        
    - [jwt.io](http://jwt.io) 에서 복호화하여 확인해봅니다!
- 4) 이 암호화 된 데이터는 어떻게 쓸 수 있나요?
    - 보통 암호화 된 데이터는 클라이언트(브라우저)가 전달받아 다양한 수단(쿠키, 로컬스토리지 등)을 통해 저장하여 API 서버에 요청을 할 때 서버가 요구하는 HTTP 인증 양식에 맞게 보내주어 인증을 시도합니다!
    - 비유하자면, 놀이공원의 자유이용권과 비슷한거죠!
        - **회원가입**: 회원권 구매
        - **로그인**: 회원권으로 놀이공원 입장
        - **로그인 확인**: 놀이기구 탑승 전마다 유효한 회원권인지 확인
        - **내 정보 조회**: 내 회원권이 목에 잘 걸려 있는지 확인하고, 내 이름과 사진, 바코드 확인

## 04. Access Token, Refresh Token

[2.3-4-1_exported.mp4](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cc31fa14-d8b2-4edd-9b3a-58c9f2ac9e61/2.3-4-1_exported.mp4)

- 1) **Access Token**이 무엇인가요?
    
    <aside>
    💡 **Access Token**은 사용자의 권한이 확인(ex: 로그인) 되었을 경우 해당 사용자를 인증하는 용도로 발급하게됩니다.
    
    </aside>
    
    이전에 저희가 구현하였던 **Cookie**로 **jwt**를 발급하고 설정한 Expire 기간이 지날 때 인증이 만료되게 하는것 또한 Access Token이라고 부를 수 있습니다.
    
    사용자가 Access Token을 가지고 인증을 요청할 경우 Token을 생성할 때 사용한 **비밀키(Secret Key)**를 가지고 인증하기 때문에, 복잡한 설계없이 코드를 구현할 수 있고, 여러 분기를 거치지 않아도 된다는 장점이 있습니다.
    
    Access Token의 경우 **Stateless(무상태)** 즉, Node.js 서버가 죽었다 살아나더라도 동일한 동작을하는 방식입니다. 즉, jwt를 이용해 사용자의 인증 여부는 확인할 수 있지만, 처음 발급한 사용자 본인인지 확인할 수는 없습니다. 🥲
    
    Access Token은 그 자체로도 사용자를 인증하는 **모든 정보를 가지고 있습니다.** 그렇기 때문에 토큰을 가지고 있는 시간이 늘어날 수록 탈취되었을 때는 피해가 더욱 커지게 됩니다.
    
    만약 토큰이 탈취되었다고 인지하더라도 저희들은 해당 토큰이 탈취된 토큰인지 알 수 없고, 고의적으로 만료를 시킬 수도 없을 것 입니다. 그러므로 저희들은 언제든지 사용자의 토큰이 탈취될 수 있다고 생각을 하고, 피해를 최소화 할 수 있는 방향으로 개발을 진행해야합니다.😊
    
- 2) **Refresh Token**이 무엇인가요?
    
    <aside>
    💡 **Refresh Token**은 Access Token 처럼 해당하는 사용자의 모든 인증 정보를 관리하는 것이 아닌, 특정한 사용자가 Access Token을 발급받을 수 있게 하기 위한 용도로만 사용됩니다.
    
    </aside>
    
    Refesh Token은 사용자의 인증정보를 **사용자**가 가지고 있는 것이 아닌, **서버**에서 해당 사용자의 정보를 **저장소** 또는 **별도의 DB**에 저장하여 관리합니다. 그렇기 때문에, 서버에서 특정 Token 만료가 필요할 경우 저장된 Token을 제거하여 **사용자의 인증 여부를 언제든지 제어가 가능**하다는 장점이 있습니다.
    
    그렇다면 어째서 바로 Access Token을 발급하지 않고, Refresh Token을 거쳐서 Access Token을 발급하는것일까요? 사용자에게 발급한 Token이 탈취당할 경우 피해를 최소화 하기 위해서 사용합니다.
    
    저희가 실제 세계에서 사용하는 **OTP**와 같이 짧은 시간 내에서만 인증 정보를 사용할 수 있게하고, 주기적으로 재발급하여, 토큰이 유출되더라도 오랜 기간동안 피해를 입는것이 아닌, 짧은 기간동안만 사용가능하도록 하여 피해를 최소화할 수 있게 됩니다.
    
    언제든지 토큰이 탈취될 수 있다는 것을 가정하고, 탈취를 막는것이 어렵다면, 우리는 탈취된 토큰자체를 사용할 수 있는 기간을 줄여서 피해를 막을 것 입니다. 😊
    
- 3) Refresh Token Project의 템플릿을 만들어봅니다!
    
    Refresh Token은 최초로 발급받고, 짧은 만료시간을 가지는 Access Token을 발급받기 위한 수단인데요. 이번 프로젝트에서는 하나의 파일에서 Refesh Token과 Access Token이 어떤식으로 동작하는지 확인해볼 예정입니다.
    
    저희는 이번 프로젝트에서 아래와 같은 API를 만들거에요! 
    
    - **Refresh Token Project의 API 목록**
    
    코드 스니펫을 복사해 프로젝트 구현을 시작해보겠습니다! 😆
    
    - **[코드스니펫] npm Package 설치**
        
        ```bash
        npm init -y
        npm install express jsonwebtoken cookie-parser -S
        ```
        
    - **[코드스니펫] Refresh Token Project - app.js**
        
        ```jsx
        // app.js
        
        const jwt = require("jsonwebtoken");
        const cookieParser = require("cookie-parser");
        const express = require("express");
        const app = express();
        const port = 3002;
        const SECRET_KEY = `HangHae99`;
        
        app.use(cookieParser());
        
        app.get("/", (req, res) => {
          res.status(200).send("Hello Token!");
        })
        
        app.listen(port, () => {
          console.log(port, '포트로 서버가 열렸어요!');
        })
        ```
        
    
    이제 `node app.js` 라는 명령어로 API 서버를 켠 뒤, [`http://localhost:3002/`](http://localhost:3002/) 주소로 들어가 “Hello Token!” 이라는 문구가 잘 보이는지 확인해보세요!
    
- 4) Refresh Token과 Access Token을 **발급**하는 API를 만들어봅니다!
    
    Express 서버가 잘 동작하는것을 확인했다면, 이번에는 사용자가 API를 호출할 때, Refresh Token과 Access Token을 발급하는 API를 만들어 보겠습니다.
    
    - **[코드스니펫] `GET` `/set-token/:id` - app.js**
        
        ```jsx
        // app.js
        
        ...
        
        let tokenObject = {}; // Refresh Token을 저장할 Object
        
        app.get("/set-token/:id", (req, res) => {
          const id = req.params.id;
          const accessToken = createAccessToken(id);
          const refreshToken = createRefreshToken();
        
          tokenObject[refreshToken] = id; // Refresh Token을 가지고 해당 유저의 정보를 서버에 저장합니다.
          res.cookie('accessToken', accessToken); // Access Token을 Cookie에 전달한다.
          res.cookie('refreshToken', refreshToken); // Refresh Token을 Cookie에 전달한다.
        
          return res.status(200).send({ "message": "Token이 정상적으로 발급되었습니다." });
        })
        
        // Access Token을 생성합니다.
        function createAccessToken(id) {
          const accessToken = jwt.sign(
            { id: id }, // JWT 데이터
            SECRET_KEY, // 비밀키
            { expiresIn: '10s' }) // Access Token이 10초 뒤에 만료되도록 설정합니다.
        
          return accessToken;
        }
        
        // Refresh Token을 생성합니다.
        function createRefreshToken() {
          const refreshToken = jwt.sign(
            {}, // JWT 데이터
            SECRET_KEY, // 비밀키
            { expiresIn: '7d' }) // Refresh Token이 7일 뒤에 만료되도록 설정합니다.
        
          return refreshToken;
        }
        ```
        
    - ✅  `createAccessToken`, `createRefreshToken` 코드 추가 설명
        
        `createAccessToken`는 **Access Token**을 생성하는 함수에요!
        jwt 안에는 `set-token` API를 호출할 때 받은 `id` 변수를 삽입하는데요, 해당 사용자의 id가 무엇인지 확인할 때에는 Access Token에 있는 데이터를 바탕으로 인증을 진행합니다!
        
        `createRefreshToken`는 **Refresh Token**을 생성하는 함수에요!
        jwt 안에는 아무런 데이터가 존재하지 않는데요, 해당하는 Refresh Token에 대한 정보는 서버에서 `tokenObject`라는 변수안에 할당하게 됩니다. 
        만약 서버에서 해당하는 Refresh Token에 대한 정보를 가지고 있지 않으면, Token의 인증은 실패하게 되겠죠?
        
    
    사용자가 `GET` `/set-token/:id` API를 호출했을때 Access Token과 Refresh Token을 2개 발급하게 되고, Refresh Token을 Key 값으로 입력된 id를 찾을 수 있게 구현하였습니다.
    
    그리고 `accessToken`, `refreshToken`이라는 **Key**로 Cookie를 2개 발급하게 됩니다. 😊
    
- 5) Refresh Token과 Access Token을 **검증**하는 API를 만들어봅니다!
    
    서버에서 발급받은 Refresh Token과 Access Token을 검증하기 위해 `GET` `/get-token` API를 만들어보겠습니다!
    
    - **[코드스니펫] `GET` `/get-token` - app.js**
        
        ```jsx
        // app. js
        
        ...
        
        app.get("/get-token", (req, res) => {
          const accessToken = req.cookies.accessToken;
          const refreshToken = req.cookies.refreshToken;
        
          if (!refreshToken) return res.status(400).json({ "message": "Refresh Token이 존재하지 않습니다." });
          if (!accessToken) return res.status(400).json({ "message": "Access Token이 존재하지 않습니다." });
        
          const isAccessTokenValidate = validateAccessToken(accessToken);
          const isRefreshTokenValidate = validateRefreshToken(refreshToken);
        
          if (!isRefreshTokenValidate) return res.status(419).json({ "message": "Refresh Token이 만료되었습니다." });
        
          if (!isAccessTokenValidate) {
            const accessTokenId = tokenObject[refreshToken];
            if (!accessTokenId) return res.status(419).json({ "message": "Refresh Token의 정보가 서버에 존재하지 않습니다." });
        
            const newAccessToken = createAccessToken(accessTokenId);
            res.cookie('accessToken', newAccessToken);
            return res.json({ "message": "Access Token을 새롭게 발급하였습니다." });
          }
        
          const { id } = getAccessTokenPayload(accessToken);
        	return res.json({ "message": `${id}의 Payload를 가진 Token이 성공적으로 인증되었습니다.` });
        })
        
        // Access Token을 검증합니다.
        function validateAccessToken(accessToken) {
          try {
            jwt.verify(accessToken, SECRET_KEY); // JWT를 검증합니다.
            return true;
          } catch (error) {
            return false;
          }
        }
        
        // Refresh Token을 검증합니다.
        function validateRefreshToken(refreshToken) {
          try {
            jwt.verify(refreshToken, SECRET_KEY); // JWT를 검증합니다.
            return true;
          } catch (error) {
            return false;
          }
        }
        
        // Access Token의 Payload를 가져옵니다.
        function getAccessTokenPayload(accessToken) {
          try {
            const payload = jwt.verify(accessToken, SECRET_KEY); // JWT에서 Payload를 가져옵니다.
            return payload;
          } catch (error) {
            return null;
          }
        }
        ```
        
    
    - ✅  `validateAccessToken`, `validateRefreshToken` 코드 추가 설명
        
        `validateAccessToken`과 `validateRefreshToken`은 사용자가 전달한 Token이 정상적인 토큰인지 확인하는 함수에요!
        
        - Access Token 또는 Refresh Token이 저희가 발급한 토큰이 맞는지 검증합니다.
        - Access Token 또는 Refresh Token의 만료 여부를 검증합니다.
        
    
    - ✅  `GET` `/get-token` API 에서는 어떤 에러들이 발생하나요 ?
        1. 사용자가 Cookie를 전달할 때, Access Token이 없다면 에러가 발생합니다.
            - `{ "message": "Access Token이 존재하지 않습니다." }`
        2. 사용자가 Cookie를 전달할 때, Refresh Token이 없다면 에러가 발생합니다.
            - `{ "message": "Refresh Token이 존재하지 않습니다." }`
        3. 사용자가 전달한 Refresh Token이 인증되지 않았다면 에러가 발생합니다.
            - `{ "message": "Refresh Token이 만료되었습니다." }`
        4. Refresh Token이 인증되었지만, 서버에 존재하지 않을 때 에러가 발생합니다.
            - `{ "message": "Refresh Token의 정보가 서버에 존재하지 않습니다." }`
        
    
    사용자가 발급받은 Access Token과 Refresh Token을 가지고 API를 호출할 때, 가지고 있는 토큰에 상태에 맞게 Response가 반환되는것을 확인할 수 있습니다.
    
    Access Token이 정상적으로 인증되었을 경우 Payload의 값을 Response에서 확인할 수 있게 되었습니다! 😊
    
- 6) Thuner Client로 API 테스트하기
    - **Refresh Token Project의 API 목록**
    
    - 1) Thunder Client에서 New Reqest를 생성하고, `GET` `/set-token/:id` API를 호출하겠습니다.
        
        ![84의 id를 가지도록 토큰을 발행합니다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2965ea29-da6d-4100-b889-77e4ba911847/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.50.56.png)
        
        84의 id를 가지도록 토큰을 발행합니다.
        
        ![정상적으로 토큰이 발급되었다는 API Response를 응답 받았습니다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/414a0c85-a7e3-48cf-9539-ad6142921fac/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.51.01.png)
        
        정상적으로 토큰이 발급되었다는 API Response를 응답 받았습니다.
        
        ![accesstoken, refreshtoken의 Key를 가지는 Cookie를 전달 받았습니다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e0c0d3fc-3a4f-46a2-a577-c52ae91f6d5e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.49.52.png)
        
        accesstoken, refreshtoken의 Key를 가지는 Cookie를 전달 받았습니다.
        
        - `GET` `/set-token/:id` API를 호출했을 때, “정상적으로 Token이 발급되었다”는 Response를 확인할 수 있습니다.
        - Thunder Client의 Cookies에서 `accesstoken`, `refreshtoken`의 Key를 가지는 2개의 Cookie를 전달받은것을 확인할 수 있습니다.
        
        저희는 전달받은 2개의 Token을 이용해서 다음 `GET` `/get-token` API를 호출해보도록 하겠습니다!
        
    - 2) Thunder Client에서 New Reqest를 생성하고, `GET` `/get-token` API를 호출하겠습니다.
        
        ![GET /get-token API를 호출합니다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/66270c12-d6cf-4aa1-afbf-7bdb38e82c47/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.56.18.png)
        
        GET /get-token API를 호출합니다.
        
        ![스크린샷 2022-09-09 오후 9.56.23.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/99c4016d-4fec-4da9-b17a-e66f374259b0/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.56.23.png)
        
        ![Access Token이 재발행되었다는 Response와 함께, accesstoken 쿠키를 전달받았습니다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/60f0c5b5-5f6a-4fd8-88cf-bc9a3c2f6530/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.56.33.png)
        
        Access Token이 재발행되었다는 Response와 함께, accesstoken 쿠키를 전달받았습니다.
        
        처음으로 `GET` `/get-token` API를 호출하였을때, Access Token을 갱신한다는 메시지와 함께 새로운 Access Token이 전달되는것을 확인할 수 있습니다.
        
        어째서 인증되었다는 메시지가 아니라 “Access Token이 새롭게 발급되었다”는 메시지를 응답받은걸까요?  🤔
        저희는 Access Token을 생성할 때, **10초**의 만료기간을 설정하였고, 토큰을 확인하기까지 **10초**이상의 시간이 소모되었기 때문에, 새로운 Access Token이 발급된것입니다.
        
        그렇다면 Access Token의 만료 기간을 더욱 늘리거나, 만료 기간이 되기 전에 `GET` `/get-token` API를 호출하여 정상적으로 메시지가 출력되는 것을 확인해보도록 하겠습니다.
        
    - 3) `GET` `/get-token` API의 정상적인 Response 확인하기!
        
        ![GET /get-token API를 호출합니다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/66270c12-d6cf-4aa1-afbf-7bdb38e82c47/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.56.18.png)
        
        GET /get-token API를 호출합니다.
        
        ![처음 생성한 84의 payload를 가진 Token 정보가 정상적으로 출력되었습니다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0c45bf76-ceac-4af5-9fe6-6db6baa79889/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_10.04.52.png)
        
        처음 생성한 84의 payload를 가진 Token 정보가 정상적으로 출력되었습니다.
        
        - `GET` `/set-token/:id` API에서 84의 Payload를 가진 Token을 만들었던 정보를 확인할 수 있게 되었습니다.
    
- 7) 그래서 우리는 어떤 인증 방식을 사용해야하나요?
    
    개발을 진행하다보면 모든 것에서 강점을 가지는 기술은 존재하지 않는다는것을 느낄 수 있습니다. 그렇기 때문에 새로운 기술을 도입할 때는 **현재 상황에 가장 알맞는 최선의 선택**을 하는것이 중요합니다.
    
    Access Token과 Refresh Token을 비교했을 때, 프로젝트를 빠르게 구현해야하거나 사용자의 요청에 대한 인증을 최소화 하기 위해서는 Access Token을 사용할 것이고, 보안성을 중요시 여기고, 서버를 좀더 탄탄하게 구성해야 할 경우에는 Refesh Token을 사용할 것입니다. 😊