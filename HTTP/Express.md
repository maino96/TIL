## 01. 준비하기

[3_1_ExpressJS_2차_exported.mp4](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/efff82f4-ecce-4557-9b85-ac5b39ced9cc/3_1_ExpressJS_2%E1%84%8E%E1%85%A1_exported.mp4)

### Express.js의 이해

- 1) 웹서버란 무엇인가? Express는 무엇인가?
    
    <aside>
    👉 웹서버란 무엇일까요? 우리가 브라우저에 주소를 입력하면 그 내용은 어디서 가져오는 것일까요? 우리도 그런 서버를 만들려면 어떻게 해야할까요?
    
    </aside>
    
- 2) 일반적인 웹 서버와 Node.js로 만들게 될 웹 서버 비교
    
    **일반적인 웹 서버와 Node.js로 만든 웹 서버는 다르지 않습니다!**
    
    - 그저 어떤 도구를 사용해서 만들었나의 차이일 뿐, 동일한 기능을 수행하는 웹 서버를 만들수 있으며, 이것은 다른 언어나 도구를 이용해 만든 웹 서버도 마찬가지 입니다.
   
   - 기능이 다른 웹 서버는 존재할 수 있지만 기반이 되는 개념 자체가 다른 웹 서버는 존재하지 않습니다! 우리가 배운게 전부라고 볼 수 있어요!

- 3) Express.js란?
    
    - **Express.js**는 **Node.js로 서버를 빠르고 간편하게 만들 수 있게 도와주는 웹 프레임워크** 입니다.
    
    - **Express.js** 이외에 다양한 웹 프레임워크가 존재하지만 오늘날 가장 많은 Node.js 웹서버가 **Express.js** 프레임워크를 통해 개발되었습니다.

- 4) 웹 서버와 Express.js의 차이점
   
   - **다시 한번 복습!** Express.js와 웹서버는 동일하지 않습니다!
   
    - Express.js는 웹서버 자체가 아닌 **Node.js를 위한 웹 프레임워크**로 웹 서버를 구현하기 위해 사용 되는 것이 Express.js 프레임워크 입니다.

### Express.js로 웹 서버 구현

- 1) 새 프로젝트 설정
    
    1. `VS Code` 를 실행합니다.
    
    2. 상단 메뉴의 `File` → `Open` 을 합니다.
    
    3. 새로운 폴더 버튼을 누르고 새 폴더를 생성합니다. (`spa_mall`)
        
        ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8e7f3276-f9d7-4c6a-879b-31407e1c9a18/_2021-02-20__3.17.59.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8e7f3276-f9d7-4c6a-879b-31407e1c9a18/_2021-02-20__3.17.59.png)
        
    4. 새로 만들어진 폴더를 클릭하고 `열기`
        
        ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4d097dcc-7384-4e72-a227-5501caec0c58/_2021-02-20__3.19.09.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4d097dcc-7384-4e72-a227-5501caec0c58/_2021-02-20__3.19.09.png)
        
    5. 새 파일을 생성합니다. 이름은? `app.js` 
        
        ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/34339121-a4fe-4b40-9c6a-d970d4429cc2/_2021-02-20__3.19.53.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/34339121-a4fe-4b40-9c6a-d970d4429cc2/_2021-02-20__3.19.53.png)
        
    
    1. 그리고 위에 메뉴에서 `새 터미널`을 클릭합니다.
        
     
        
    2. 터미널이 열리면 터미널에 아래와 같이 명령어를 실행하여 package.json을 생성해줍시다.
    
    ```jsx
    $ npm init -y
    ```
    
    <aside>
    👉 뒤의 -y는 npm init 명령 실행시 원래는 프로젝트명이나 버전등을 물어보는데 그런 것들을 물어보지 않고 기본값으로 알아서 설정해주는 옵션입니다. npm init -y를 마치면 아래와 같은 폴더 구조로 `package.json`파일이 생성되었는지 확인해봅시다.
    
    👉 package.json 파일을 보시면 아래와 같이 자동생성된 json파일을 보실 수 있는데, 이에 대한 자세한 내용은 하나씩 차근차근 배워 나가볼게요!
    
    </aside>
    
    ```jsx
    {
      "name": "spa_mall",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "author": "",
      "license": "ISC"
    }
    ```
    
- 2) Express.js 설치
    - 다시 터미널로 돌아가 이번에는 Express.js 프레임워크를 설치해줍니다.
    
    <aside>
    👉 express를 사용하기 전에 아래와 같이 Terminal에서 설치를 진행해줍시다.
    
    `npm i express`
    
    </aside>
    
    - 설치가 완료되었다면 이제 웹서버를 작성할 준비가 완료되었습니다!
- 3) 기본적인 웹 서버 코드 작성
    
    <aside>
    👉 SPA_MALL 폴더 안에 app.js라는 파일을 아래와 같이 만들어봅시다. 폴더 구조는 아래와 같습니다.
    
    </aside>
      
    - `package.json` 파일을 다시 열어봤을때 express 관련된 내용이 들어있으면 정상적으로 설치가 된 것입니다.
    
    - `package-lock.json`은 어떤 패키지들이 어떤 버전으로 설치되었는지 기록해놓은 파일입니다. 나중에 이 파일이 있으면 다른 동료들과 협업할때 같은 환경으로 개발할 수 있게 도와줍니다.
    
    - `node_modules` 폴더는 npm을 통해 설치된 패키지들에 대한 파일이 있는 폴더입니다.
    앞으로 개발을 하면서 다양한 라이브러리를 사용하게 될텐데 이에 대한 모든 파일이 여기에 설치됩니다.
    
    
    - **app.js 예시**
        
        ```jsx
        const express = require('express');
        const app = express();
        const port = 3000;
        
        app.get('/', (req, res) => {
          res.send('Hello World!');
        });
        
        app.listen(port, () => {
          console.log(port, '포트로 서버가 열렸어요!');
        });
        ```
        
- 4) 내가 만든 웹 서버 실행
    
    <aside>
    👉 app.js를 실행하기 위해서는 SPA_MALL의 경로에서 아래와 같이 실행해줍시다.
    
    `node app.js`
    
    </aside>
        
    - “**3000 포트로 서버가 열렸어요!”** 라는 메세지가 출력되었다면 정상적으로 서버가 실행된것입니다!
    
    - 실행에 문제가 있어요 😢
        
        ```jsx
        Error: listen EADDRINUSE: address already in use :::3000
            at Server.setupListenHandle [as _listen2] (net.js:1318:16)
            at listenInCluster (net.js:1366:12)
            at Server.listen (net.js:1452:7)
        
        // 혹시 위와같은 에러가 나오나요? 이미 다른 프로그램이 해당 포트를 사용중일 수 있어요.
        // app.js 파일에서 3000 이라고 써져있는 port를 4000이나 다른 숫자로 변경해서 다시 해봅시다.
        ```
        
        - 🧩  **한발짝 더 나아가기**
            
            이미 사용 중인 포트를 찾아서 종료하고 싶다면 어떻게 해야할까요?
            
            - MAC
                
                맥의 경우에는 **lsof**라는 명령어를 사용하여 간편하게 특정 포트를 찾을 수 있습니다.
                **lsof**란 list open files를 의미하며, 현재 시스템에 열린 파일 목록에 대한 정보들을 알려 줍니다.
                
                1. 터미널을 열고 아래 명령어를 통해서, 우리가 원하는 포트 정보를 찾습니다.
                예를 들어서 3000포트를 점유하고 있는 프로세스에 대한 정보를 찾고 싶다면
                `lsof -i :3000` 이라고 입력하면 됩니다.
                    
                    ```bash
                    lsof -i :원하는포트
                    ```
                    
                2. 해당 포트를 점유하고 있는 PID를 찾아서 종료시킵니다.
                    
                    ```bash
                    kill -9 포트를 점유하고 있는 PID
                    ```
                                        
            - WINDOW
                
                윈도우의 경우 **netstat** 이라는 명령어를 통해서 현재 컴퓨터와 연결된 네트워크 정보를 확인할 수 있는대요, 이를 이용해서 원하는 포트 정보를 확인할 수 있습니다.
                
                * netstat 명령어에 대한 추가적인 설명등이 궁금하시다면 아래 글을 참고해주세요!
                
                1. cmd 창을 열어서 아래 명령어를 통해서, 우리가 원하는 포트 정보를 찾습니다.
                    
                    ```bash
                    netstat -ano | find "원하는포트"
                    ```
                    
                2. 해당 포트를 점유하고 있는 PID를 찾아서 종료시킵니다.
                    
                    ```bash
                    taskkill /f /pid 12952
                    ```
                    
- 5) 브라우저에서 웹 서버의 응답 확인
    
    - 위의 코드에서 **GET Method**로 작성된 코드를 통해 Hello World! 라는 문구를 확인 할 수 있습니다!
    
    <aside>
    🎉 **축하드려요!**
    드디어 Express.js를 활용한 첫번째 서버를 만들고 직접 확인해봤어요!
    
    </aside>
    

### API Client 학습

- 1) API Client란 뭘까?
    
    - **API Client**란 개발단계에서 우리가 작성한 **API의 요청을 확인**하거나 **테스팅** 할 때 도움을 주는 툴입니다. API Client를 사용함으로 개발 속도를 높이거나 치명적인 에러를 예방하는데 도움을 받을 수 있습니다.
    - `Postman`, `Insomnia` 등 여러 API Client가 있지만 이번에는 `Thunder Client`를 사용할 예정입니다.
        
        - `Thunder Client`는 VS Code 안에서 사용할 수 있으면서, 기능이 부족하지 않기 때문에 비교적 쉽게 사용 할 수 있습니다!

- 2) 어떤 상황에 필요할까?
    
    지금까지 우리는 HTTP Method 중 [**GET Method**](https://www.notion.so/03-Express-js-3304447e6e3b48fc90b2ebc114ff5a20)에 대응하는 API만 만들고 브라우저로 확인했습니다!
    
    아직까진 API Client가 필요 없어보였지만 **POST**, **PATCH**, **PUT**, **DELETE**, **HEAD** 등의 다양한 Method에 대한 API를 개발하고 테스트하기 위해서는 반드시 필요한 도구라고 볼 수 있습니다.
    
- 3) VS Code - Thunder Client 설치
   
    1. VS Code 내에 좌측 탭 맨아래 Extensions를 눌러줍니다.
        
        
    2. 검색창이 나오면 `Thunder Client`를 검색하고 제일 위에 나오는 아이콘을 눌러보면 아래와 같이 나옵니다.
        
        
    3. Install 버튼을 눌러 설치를 해주시고 아래와 같이 번개 모양 아이콘이 생기면 설치가 완료된것입니다!
        
        
- 4) Thunder Client로 웹 서버 응답 확인하기
    
    API Client인 Thunder Client를 설치했으니 이제 사용해봐야겠죠?
    이전에 만든 기본적인 웹 서버 API를 요청해봅시다. 우선 `node app.js`를 입력하여 서버를 켜줍니다.
    
    1. 먼저 Thunder Client 아이콘을 클릭하시고 아래와 같이 창이 나오면 New Request 버튼을 눌러줍니다.
          
    2. 이런 화면이 나오게 됩니다. 그럼 이제 맨위의 URI를 입력하는곳에 웹 서버 API의 HTTP Method인 GET으로 설정해 준뒤  [http://localhost:3000/](http://localhost:3000/api/goods) 를 입력하고 Send 버튼을 눌러줍니다.
            
    3. 이전에 브라우저에서 보았던 “Hello World!”가 나오게 되면 성공입니다!
                
- 5) Thunder Client 활용하기
    - Collections
                
        - 특별한 프로젝트마다 API 목록을 정리해서 사용할 수 있습니다.
        
        - Collections는 여러가지의 API를 그룹화 시킬 수 있습니다.
    
    - Env
                
        - 여러번 사용되는 값들을 환경변수로 설정할 때 사용합니다.
       
        - Token, URL, 개인 키 등 다양한 자격증명을 저장 및 사용할 수 있습니다.

---

## 02. 시작하기

### Routing 이해 및 Router 학습

- 1) Routing이란?
    
    **Routing**은 클라이언트의 요청 조건(메서드, 주소 등)에 대응해 응답하는 방식을 말합니다.
    
- 2) Router란?
    
    여기서 말하는 **Router**는 클라이언트의 요청을 쉽게 처리 할 수 있게 도와주는 `Express.js` 기본 기능중 하나입니다.
    
    - 일반적으로 **Router**는 아래와 같은 구조를 가집니다.
    
    ```jsx
    router.**METHOD**(**PATH**, **HANDLER**);
    ```
    
    - `router`: express의 라우터를 정의하기 위해 사용합니다.
    
    - `METHOD`: HTTP Method를 나타냅니다. (ex: get, post, put, delete …)
    
    - `PATH`: 실제 서버에서 API를 사용하기 위한 경로를 나타냅니다.
   
    - `HANDLER`: 라우트가 일치할 때 실행되는 함수힙니다.

- 3) Router 사용해보기
    
    - `routes` 폴더를 생성해 `goods.js`라는 파일을 생성합니다.
   
    - express 에서 제공되는 Router 함수를 사용해 Router를 생성합니다.
        
        ```jsx
        // routes/goods.js
        const express = require('express');
        const router = express.Router();
        ```
        
    - 그리고 예시로 엔드포인트를 작성해보겠습니다.
        
        ```jsx
        // routes/goods.js
        router.get('/', (req, res) => {
        	res.send('this is home page');
        });
        
        router.get('/about', (req, res) => {
        	res.send('this is about page');
        });
        ```
        
    - 그리고 작성한 Router를 app.js에서 사용하기 위해서 하단에 내보내주는 코드를 추가합니다.
        
        ```jsx
        // routes/goods.js
        module.exports = router;
        ```
        
    - Router 미들웨어를 사용하겠다고 작성합니다.
        
        ```jsx
        // app.js
        const goodsRouter = require("./routes/goods");
        app.use("/api", [goodsRouter]);
        ```
        
    - 이제부터 [http://localhost:3000/](http://localhost:3000/) 뒤에 `/api` 로 시작되는 주소는 `routes/goods.js` 에 있는 Router 미들웨어를 통해 처리됩니다.
        - ❓ 미들웨어(Middle ware)란 뭘까요?
            
            <aside>
            💡 웹 서버에서 요청을 받을때 가끔 모든 요청에 대해 공통적인 처리를 하고싶은 경우가 생길 수 있습니다. 그럴때 미들웨어를 이용하여 웹 서버의 요청/응답에 대해 공통적으로 관리가 가능합니다.
            
            현재는 가볍게 설명하고 넘어가지만 다음 주차에는 확실하게 개념을 확인해봐요! 😇
            
            </aside>
            

### Module의 이해

[1.3-2-1_exported.mp4](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0fcc9b19-b2cc-4de4-b184-dcf7f14a2bfc/1.3-2-1_exported.mp4)

- 1) Module이란?
    - Module은 분리된 **자바스크립트 파일**이고 각 파일은 **특정한 기능**을 가진 여러 개의 함수와 변수들의 **집합**입니다!
    - Module을 만들면 다른 프로그램에서 해당 모듈을 **재사용**할 수 있습니다.
    - Module은 그 자체로도 하나의 **프로그램**이면서 다른 프로그램의 **부품**으로도 사용할 수 있습니다.
    - 보통 **1개의 파일**이 **1개의 모듈**이 됩니다.
- 2) Module은 어떻게 사용할까요?
    - `export` 명령어를 변수나 함수 앞에 붙이면 외부 모듈에서 해당 변수나 함수에 접근할 수 있습니다.
    - `import`, `require` 명령어를 사용하면 외부 모듈의 기능을 가져올 수 있습니다.
        - ❓ `import`, `require`는 어떻게 구분해서 사용할까요?
            - 자바스크립트는 대표적으로 **CommonJS**, **ES6(ES2015)** 방식으로 모듈 시스템을 관리할 수 있습니다.
            - `require`는 현재 학습하고 있는 **CommonJS**로 모듈 시스템을 관리할 때 사용합니다.
            - `import`는 **ES6(ES2015)**로 모듈 시스템을 관리할 때 사용합니다.
            
            [→ ES6로 사용해보고 싶다면 여기를 클릭해서 확인해보세요!](https://nodejs.org/api/packages.html#determining-module-system)
            
- 3) Module 사용해보기
    - `modules` 폴더를 생성해 `math.js`, `run.js` 라는 파일을 생성합니다.
    - 2가지의 인자를 입력받았을 때 값을 더해주는 함수를 생성합니다.
        
        ```jsx
        // modules/math.js
        function add(a, b) {
         return a + b;
        }
        ```
        
    - 그리고 작성한 함수를 다른 모듈로 내보내주기 위해 하단에 코드를 추가합니다.
        
        ```jsx
        // modules/math.js
        module.exports = add;
        ```
        
    - run.js에서 불러들인 add함수를 사용하도록 작성합니다.
        
        ```jsx
        // modules/run.js
        const add = require("./math");
        console.log(add(3, 4));
        // Print: 7
        ```
        

### Request와 Response

[1.3-2-3.mp4](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a529989e-3489-4908-8167-38f89003223a/1.3-2-3.mp4)

- 1) Request, Response란 뭘까?
    - **Request**란 **클라이언트가 서버에게 전달**하려는 정보나 메시지를 담는 객체를 의미합니다.
    - **Response**란 **서버에서 클라이언트로 응답** 메시지를 전송시켜주는 객체입니다.
- 2) 서버 모듈
    - Node.js의 서버 모듈에는 대표적으로 **http** 모듈과 **Express** 모듈이 존재합니다.
    - Express 모듈은 http 모듈을 **확장하여 제공**합니다.
    - Express 모듈은 기존 http 모듈의 메서드도 사용할 수 있지만, Express가 추가 제공하는 메서드나 속성들을 사용할 수 있습니다.
    - 최근에는 Express의 메서드가 더욱 편리하기에 기존 http 모듈의 메서드는 잘 사용되고 있지 않습니다.
    
    → [http 모듈이 궁금하시다면 여기를 클릭해주세요!](https://leejabba.gitbooks.io/node-js/content/http-baa8-b4c8.html)
    
- 3) Express 모듈의 req, res 객체
    
    <aside>
    💡 **볼드** 내용들만 우선적으로 확인 하면 좋아요!
    
    나머지 내용은 추가적으로 궁금할 때 별도로 학습하시면 좋아요! 😇
    
    </aside>
    
    **req 객체**
    
    - req.app : req 객체를 통해 app 객체에 접근할 수 있습니다.
    - req.ip: 요청한 Client의 ip 주소가 담겨 있습니다.
    - **req.body**: Request를 호출할 때 body로 전달된 정보가 담긴 객체입니다.
        - body-parser Middleware를 이용하여야 해당 객체를 사용할 수 있습니다.
    - **req.params**: 라우터 매개 변수에 대한 정보가 담긴 객체입니다.
    - **req.query**: Request를 호출할 때 쿼리 스트링으로 전달된 정보가 담긴 객체입니다.
    - req.cookies: Request를 호출할 때 Cookie 정보가 담긴 객체입니다.
        - cookie-parser Middleware를 이용하여야 해당 객체를 사용할 수 있습니다.
    - req.get(*Header*): 헤더에 저장된 값을 가져오고 싶을 때 사용합니다.
    
    **res 객체**
    
    - res.app : res 객체를 통해 app 객체에 접근할 수 있습니다.
    - **res.status(*코드*)** : Response에 HTTP 상태 코드를 지정합니다.
    - **res.send(*데이터*)** : 데이터를 포함하여 Response를 전달합니다.
    - **res.json(*JSON*)** : JSON 형식으로 Response를 전달합니다.
    - res.end() : 데이터 없이 Response를 전달합니다.
    - res.direct(*주소*) : 리다이렉트할 주소와 함께 Response를 전달합니다.
    - res.cookie(*Key, Value, Option*) : 쿠키를 설정할 때 사용합니다.
    - res.clearCookie(*Key, Value, Option*) : 쿠키를 제거할 때 사용합니다.

### API와 REST API의 개념

[1.3-2-4_exported.mp4](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/95020201-c4f7-473d-9dad-f7adb5f06994/1.3-2-4_exported.mp4)

- 1) API(Application Programming Interface)란?
    - **API**는 **애플리케이션끼리 연결**해주는 **매개체**이자 **약속**이라고 볼 수 있습니다.
- 2) 그럼 현실에서는 어떤것을 API로 비유할 수 있을까?
    - 키보드로 글자를 입력하면 키보드는 우리가 작성한 글자를 컴퓨터에 전달해주는 역할을 합니다.
    우리가 키보드의 키를 누르는것이 API를 호출하는것으로 볼 수 있습니다.
    - 어떤 연인은 서로 기분이 상할것 같으면 미리 “윙크”를 하기로 약속했습니다.
    대화하다 갑자기 “윙크”를 본 상대방은 기분이 나쁜것을 알아채고 은근히 기분을 풀어주려 노력합니다.
    이러한 약속 또한 API라고 볼 수 있습니다.
- 3) 우리가 API를 작성한다는 의미는?
    - 웹 어플리케이션(프론트엔드)에서 원하는 기능을 수행하는 **URL**과 **인터페이스**를 **제공**한다는 의미입니다.
    - 우리가 작성 할 API에서 **원하는 데이터를 받아** **데이터베이스에 데이터를 저장**하고, **저장되어 있는 데이터를 읽어서** **웹 어플리케이션(프론트엔드)에 데이터를 제공**하는 행위를 통해 사용자가 원하는 목적을 이룰 수 있게 해야 합니다.
- 4) 그럼 REST API는 어떤 의미를 갖는 API인가?
    - REST API, RESTful API 라고 들어보셨나요? 여기서 REST란 무슨 의미일까요?
    - REST는 “**Representational State Transfer**”의 줄임 말로, [위키](https://ko.wikipedia.org/wiki/REST)를 따르면 다음과 같습니다.
        
        > **REST**(Representational State Transfer)는 [월드 와이드 웹](https://ko.wikipedia.org/wiki/%EC%9B%94%EB%93%9C_%EC%99%80%EC%9D%B4%EB%93%9C_%EC%9B%B9)과 같은 분산 [하이퍼미디어](https://ko.wikipedia.org/wiki/%ED%95%98%EC%9D%B4%ED%8D%BC%EB%AF%B8%EB%94%94%EC%96%B4) 시스템을 위한 [소프트웨어 아키텍처](https://ko.wikipedia.org/wiki/%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4_%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98)의 한 형식이다.
        > 
    - 최대한 간단하게 설명하자면 **URL**, **Headers, Method** 등 네트워크 표현 수단을 사람이 봐도 이해하기 쉬운 표현으로 정의한다고 이해하면 됩니다.
    또한 이 “REST 아키텍쳐”는 사람이 봐도 쉽게 이해할 수 있도록 “자원”을 정의하고 이 “자원”을 중심으로 표현을 구성하는 원칙을 제시합니다.
        
        ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d68f3618-6b1d-4650-827e-ff661c45d69e/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d68f3618-6b1d-4650-827e-ff661c45d69e/Untitled.png)
        
    - REST API는 “REST 아키텍쳐”라는 규칙을 따르는 API라고 생각하시면 됩니다.
    - REST API의 구성은 크게 세 가지로 이루어 집니다
        
        ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6268a0c7-7694-4770-8454-aa68fbe7508f/_2021-02-24__9.07.34.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6268a0c7-7694-4770-8454-aa68fbe7508f/_2021-02-24__9.07.34.png)
        
        [RESTful API](https://velog.io/@meekukin/RESTful-API-4uk5rtheqv)
        
    1. **자원(Resource) - URL**
        - 우리가 만들 소프트웨어가 관리하는 모든 것을 자원으로 표현할 수 있습니다. 쇼핑몰이라면 상품(Goods)에 대해서 정보를 관리할것이고 또는 장바구니(Carts)에 담긴 상품들도 관리해야겠죠.
    2. **행위 - HTTP method**
        - 이전에 배웠던 HTTP method 기억나시나요? `GET`, `POST` 등등이 있다고 했었는데요. 이것으로 해당 자원에 대한 행위를 표현할 수 있습니다. 예를 들어 GET 메소드는 해당 자원의 조회, POST 메소드는 해당 자원의 생성 이런 식으로요.
        - 이렇게 나누어진 것을 보통 CRUD 라고 합니다. 자원에 대한 생성/조회/수정/삭제를 각각의 method 로 나누어놓은 것이지요.
            
            ```jsx
            Create : 생성(POST)
            Read : 조회(GET)
            Update : 수정(PUT),(PATCH)
            Delete : 삭제(DELETE)
            ```
            
        - 위 이미지의 예시처럼 쓰이는 것이 일반적인 method 사용방식입니다. 하지만 이것은 필수인 부분이 아니고 모든 곳에서 다 이렇게 지켜서 사용하지는 않습니다. 상황에 따라 저것을 완벽하게 지키기 어려운 부분들도 있으니 이 부분 참고 해주세요.
    3. **표현**
        - 해당 자원을 어떻게 표현할지에 대한 설명입니다. 보통 **JSON**, **XML** 같은 형식을 이용해서 자원을 표현합니다.
        - HTTP에서는 `Content-Type` 이라는 헤더를 통해 표현 방법을 서술합니다.
- 5) REST API 예시
    
    ```jsx
    router.get('/books', (req, res) => {
    	res.json({ success: true, data: getAllBooks() });
    });
    ```
    
    - 위의 예시 코드는 `/books` 라는 URL을 통해 전체 책 목록을 불러와 응답해 주는 역할을 하는 API입니다.
    - 위의 API는 REST API의 관점에서 보았을때 URL로 리소스를 구분할 수 있고 다른 표현이 없으므로 **전체 리스트를 불러오는것**을 짐작 할 수 있습니다.
    또한 CRUD 중 Read를 담당하는 HTTP 메소드로 표현하여 REST한 API라고 볼 수 있습니다.

---

## 03. REST API 개발

[3_3_2차_exported.mp4](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8dfa0654-f0a8-4199-83a2-15f6356b7c62/3_3_2%E1%84%8E%E1%85%A1_exported.mp4)

- 1) 상품 목록 조회 API 구현하기
    - 구현하려면 어떻게 해야 할까요?
        - 상품 목록 조회 API에서는 모든 상품이 한번에 다 나올수 있어야 합니다.
        - 예를들어 get 메소드를 이용해서 `/goods` 라는 주소로 들어갔을때 모든 상품 목록이 response로 응답해서 json 포맷으로 상품 목록이 보여야 합니다.
        - 이번 주차에서는 데이터베이스를 사용하지 않기때문에 routes 폴더에 goods.js 파일에 아래의 json 데이터를 저장해주도록 합니다.
        - 예시 데이터를 활용해 응답할 수 있도록 만들어보세요!
    - **[코드스니펫] 예시 데이터**
        
        ```jsx
        // /routes/good.js
        const goods = [
          {
            goodsId: 4,
            name: "상품 4",
            thumbnailUrl:
              "https://cdn.pixabay.com/photo/2016/09/07/02/11/frogs-1650657_1280.jpg",
            category: "drink",
            price: 0.1,
          },
          {
            goodsId: 3,
            name: "상품 3",
            thumbnailUrl:
              "https://cdn.pixabay.com/photo/2016/09/07/02/12/frogs-1650658_1280.jpg",
            category: "drink",
            price: 2.2,
          },
          {
            goodsId: 2,
            name: "상품 2",
            thumbnailUrl:
              "https://cdn.pixabay.com/photo/2014/08/26/19/19/wine-428316_1280.jpg",
            category: "drink",
            price: 0.11,
          },
          {
            goodsId: 1,
            name: "상품 1",
            thumbnailUrl:
              "https://cdn.pixabay.com/photo/2016/09/07/19/54/wines-1652455_1280.jpg",
            category: "drink",
            price: 6.2,
          },
        ];
        ```
        
    - 응답 값 예시
        - [http://localhost:3000/api/goods](http://localhost:3000/api/goods) 에 접속했을때 아래와 같이 보이면 제대로 작동한것입니다.
        
        ```jsx
        {
          "goods": [
            {
              "goodsId": 4,
              "name": "상품 4",
              "thumbnailUrl": "https://cdn.pixabay.com/photo/2016/09/07/02/11/frogs-1650657_1280.jpg",
              "category": "drink",
              "price": 0.1
            },
            {
              "goodsId": 3,
              "name": "상품 3",
              "thumbnailUrl": "https://cdn.pixabay.com/photo/2016/09/07/02/12/frogs-1650658_1280.jpg",
              "category": "drink",
              "price": 2.2
            },
            {
              "goodsId": 2,
              "name": "상품 2",
              "thumbnailUrl": "https://cdn.pixabay.com/photo/2014/08/26/19/19/wine-428316_1280.jpg",
              "category": "drink",
              "price": 0.11
            },
            {
              "goodsId": 1,
              "name": "상품 1",
              "thumbnailUrl": "https://cdn.pixabay.com/photo/2016/09/07/19/54/wines-1652455_1280.jpg",
              "category": "drink",
              "price": 6.2
            }
          ]
        }
        ```
        
    - goods.js 예시
        
        ```jsx
        // /routes/goods.js
        const express = require("express");
        
        const router = express.Router();
        
        const goods = [
          {
            goodsId: 4,
            name: "상품 4",
            thumbnailUrl:
              "https://cdn.pixabay.com/photo/2016/09/07/02/11/frogs-1650657_1280.jpg",
            category: "drink",
            price: 0.1,
          },
          {
            goodsId: 3,
            name: "상품 3",
            thumbnailUrl:
              "https://cdn.pixabay.com/photo/2016/09/07/02/12/frogs-1650658_1280.jpg",
            category: "drink",
            price: 2.2,
          },
          {
            goodsId: 2,
            name: "상품 2",
            thumbnailUrl:
              "https://cdn.pixabay.com/photo/2014/08/26/19/19/wine-428316_1280.jpg",
            category: "drink",
            price: 0.11,
          },
          {
            goodsId: 1,
            name: "상품 1",
            thumbnailUrl:
              "https://cdn.pixabay.com/photo/2016/09/07/19/54/wines-1652455_1280.jpg",
            category: "drink",
            price: 6.2,
          },
        ];
        
        //상품 목록 조회 API
        router.get("/goods", (req, res) => {
        	res.json({ goods: goods });
        });
        ```
        
- 2) 상품 상세 조회 API 구현하기
    - 구현하려면 어떻게 해야 할까요?
        - 이번 API에서는 특정 상품의 상세 조회를 위해서 기존 상품 목록 주소 이후에 **URL Parameters**로 **상품 id**로 특정 **상품 상세 조회**를 해야합니다.
        - URL Parameters?
            - router 주소에 쓰이는 특수한 패턴중 하나인데 예를 들어 상품 목록 조회 API의 주소가 `/goods` 였다면 그뒤에 `/:goodsId` 라는 값을 추가해서 요청시 id값을 받아올 수 있습니다.
            - 이 값은 API 내에서 req.params 객체 안에 들어있는것을 확인할 수 있습니다.
    - 응답 값 예시 (`http://localhost:3000/api/goods/1` 요청 예시)
        
        ```jsx
        {
          "detail": {
            "goodsId": 1,
            "name": "상품 4",
            "thumbnailUrl": "https://cdn.pixabay.com/photo/2016/09/07/02/11/frogs-1650657_1280.jpg",
            "category": "drink",
            "price": 0.1
          }
        }
        ```
        
    - goods.js 예시
        
        ```jsx
        // /routes/goods.js
        //상품 상세 조회 API
        router.get("/goods/:goodsId", (req, res) => {
        	const { goodsId } = req.params;
        	const [detail] = goods.filter((goods) => goods.goodsId === Number(goodsId));
        	res.json({ detail });
        });
        ```
        

---

## 04. Quiz

<aside>
❓ 1. Express.js는 무엇때문에 사용하는 것일까요?

</aside>

<aside>
❓ 2. 대표적인 REST API의 HTTP Method 5가지는 무엇일까요?

</aside>

<aside>
❓ 3. 미들웨어 동작 방식 그려보기

- 상세보기
    
    이번 주차에서는 미들웨어가 어떻게 동작하는지 배워보았죠?
    
    그러면 5개의 미들웨어가 존재한다고 가정하고, 요청이 들어올 경우 어떻게 동작하는지 한번 그려보세요!
    아래의 구성요소가 반드시 포함되어야 합니다!
    
    - Request
    - Response
    - Node.js server
    
    머릿속으로 상상하며 간단하게 그려보세요! 😄
    
</aside>

## 05. Quiz 답안

- Express.js는 무엇때문에 사용하는 것일까요?
    - Express.js는 Node.js로 서버를 빠르고 간편하게 만들 수 있게 도와주는 웹 프레임워크 입니다.
- 대표적인 REST API의 HTTP Method 5가지는 무엇일까요?
    - 대표적인 HTTP Method에는 [`GET`, `POST`, `PUT`, `PATCH`, `DELETE`]가 있습니다.
- `미들웨어 동작 방식 그려보기` 답안
    
    ![Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fe0b8d9f-b036-4053-a682-d28e88bd32f1/Untitled.png)
    

---

## etc) 키워드

<aside>
💡 더 찾아보면 좋을 키워드들에 대한 힌트에요!

1. 프레임 워크란 무엇일까요?
2. 프레임 워크와 라이브러리는 어떠한 차이점이 있을까요?
3. 웹 서버와 Express.js의 차이점은 어떤것들이 있을까요?
</aside>