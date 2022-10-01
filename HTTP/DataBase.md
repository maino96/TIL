## 01. 준비하기

[5-1_2차_exported.mp4](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9c3e750d-5c1a-407e-baec-24fb00ecfcf5/5-1_2%E1%84%8E%E1%85%A1_exported.mp4)

### 데이터베이스와 MongoDB의 개념

- 1) 데이터베이스란 뭘까?
   
    - 단순히 데이터를 잘 저장하고 잘 찾기 위해 만들어진 소프트웨어를 **Database Management System(DBMS)** 이라 부릅니다.
    
    - DBMS가 설치된 서버 컴퓨터를 데이터베이스 **서버(DB 서버**)라고 부를 수 있습니다.
    
    - 흔히 "데이터베이스에 저장한다" 라고 말하면 이 **DBMS가 설치된 서버에 데이터를 저장**한다고 말하는것입니다.
   
    즉, **DB 서버의 모든 데이터는 DBMS가 관리**하게 됩니다.
    
    - 데이터베이스의 종류는 크게 다음과 같습니다.
        
        - 🕸 **관계형 데이터베이스 - Relational Database (RDB)**:
        데이터 형식이 정해져 있고, 데이터 끼리 **관계**를 맺어 **모순이 없는 데이터**를 유지할 수 있도록 도와주는것에 집중한 데이터베이스를 **관계형 데이터베이스**라고 부릅니다.
        *모순이 없는 데이터: 무결성과 정합성이 높은 데이터*
        
        - 🗽 **비관계형 데이터베이스 - Non-relational Database (NoSQL)**:
        관계형 데이터베이스에 속하지 않는 모든 데이터베이스를 **비관계형 데이터베이스**라고 부릅니다.
        비관계형 데이터베이스는 **데이터의 형태가 고정되어 있지 않고 유연하게 확장**할 수 있지만, 유연한 만큼 저장되는 데이터를 제대로 관리하지 않으면 데이터베이스에 저장된 데이터를 신뢰할 수 없게 되기도 합니다.
        최근 많은 스타트업에서 **유연한 설계를 위해 많이 채택**되는 데이터베이스 유형입니다.

- 2) MongoDB는 뭘까?
    
    - 국내, 외 수많은 개발자들에게서 사용되고있는 가장 인기있는 **비관계형 데이터베이스 (NoSQL)** 중 하나입니다.
    
    - **모든 데이터가 JSON** 형태로 저장됩니다.
    
    - 복잡한 구조를 쉽게 저장할 수 있는 장점이 있습니다.
    
    - 무료로 사용할 수 있습니다.
   
    - 스케일을 쉽게 줄이고 늘일 수 있습니다.

- 3) 웹 서버와 DB 서버는 어떤 관계일까?
    
    - 두 개념 다시 정리
        
        - **웹 서버**는 **웹 클라이언트**가 원하는 데이터와 기능을 제공합니다.
        
        - **DB 서버**는 데이터를 최대한 성능 좋게 저장하고 **DB 클라이언트**가 원하는 데이터를 제공합니다.
    
    - 결국 두가지 서버는 어떤것을 제공하냐만 다를 뿐, 기본 원칙은 비슷합니다.
    그럼 웹 서버는 DB 서버와 어떤 관계일까요?
    
    - **웹 서버**는 DB 서버를 이용하는 **DB 클라이언트**가 될 수 있습니다.
        

        💡 **정리하면?**  `브라우저 ↔ 웹 서버 ↔ DB 서버`
        
      
        

### MongoDB 설치하기

- 1) MongoDB 설치
    
    - 윈도우
        - **[코드스니펫] mongoDB 다운로드**
            
            ```jsx
            [https://www.mongodb.com/try/download/community](https://www.mongodb.com/try/download/community)
            ```
            
        1. C드라이브에, 그림과 같이 data 라는 폴더를 만들고, 그 안에 db 라는 폴더를 만듭니다.
            
            
        2. [링크](https://www.mongodb.com/download-center/community)로 가셔서, MongoDB Community Server 탭에서 다음 사항을 선택한 뒤 다운로드합니다. (캡처 이미지를 클릭하면 크게 보실 수 있어요!)
            - Version : 5.0.9 (current)
            - Platfrom : Windows
            - Package : MSI
            
            
        3. Next 를 클릭합니다.
            
            
        4. 약관에 동의한 뒤 Next를 클릭합니다. 
            
            
        5. Custom을 클릭합니다. 
            
            
        6. Browse를 클릭합니다. 
            
            
        7. C:\data\db\ 를 찾아 선택하고 OK를 클릭합니다.
            
            
        8. Location 항목이 C:\data\db\ 로 변경된 것을 확인하고 Next 를 클릭합니다.
            
            
        9. Next 를 클릭합니다.
            
            
        10. Install MongoDB Compass 선택을 해제하고 Next를 클릭합니다.
            
            
        11. Install을 선택합니다.
            
            
        12. 아래와 같은 알림창이 뜨면, 'ignore'를 클릭해주세요.
            
            
        13. 제어판 > 시스템 및 보안 > 시스템 에서 [고급 시스템 설정]을 클릭합니다.
            
            
        14. 환경 변수 > [시스템 변수] 목록 > Path 선택 > 편집을 클릭한 뒤 다음 내용을 추가합니다.
            
            ```jsx
            C:\data\db\bin
            ```
                                   
        15. 윈도우 키 + R 을 누른 후 cmd 를 입력하고 엔터를 누릅니다. 명령 프롬포트에 다음 명령어를 입력합니다.
            
            (입력하면 아무일도 일어나지 않는 것이 정상입니다. 🤓)
            
            ```bash
            mongod --install --serviceName MongoDB --serviceDisplayName MongoDB --dbpath C:\data\db --logpath C:\data\db\log\mongoservice.log --logappend
            ```
            
            그 후에, 다음 명령어를 입력합니다.
            
            ```jsx
            mongo
            ```
            
            아래와 같은 화면이 보이면 정상 작동 하는 것입니다. cmd 창을 닫으면 끝!🔥
            
            
        
    - 맥
        - 터미널을 실행합니다. 혹은 vscode의 터미널 창을 이용해도 괜찮아요.
       
        - Homebrew 설치하기
            
            <aside>
            👉 **Homebrew**는 무엇인가요?
            
            ****새로운 것이 참 많죠? 지금부터 맥의 편리함에 빠져드신 겁니다.
            Homebrew는 '다운로드 패키지'를 관리할 수 있는 툴이에요.
            
            *brew install 프로그램이름*
            
            을 입력하면, 프로그램을 자동으로 다운로드 받아 설치해준답니다. 엄청나죠?
            
            </aside>
            
            터미널 창에 아래 코드를 복사, 붙여넣기 하고 엔터!
            
            ```bash
            /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
            ```
            
            그러면 아래와 같은 화면이 나옵니다. 이 화면에서 다시 엔터!
                        
            그러면 아래와 같이 패스워드 입력칸이 나옵니다. 내 맥북 패스워드를 입력하고 엔터!
            (패스워스를 입력하더라도 화면에 나타나진 않아요. 사실 잘 입력되고 있으니 걱정 마세요! 😜)
                        
            엔터 누른 후에 만약 맥 소프트웨어(Xcode) 업데이트 알림이 뜨면 업데이트를 해주세요.
                        
            모든 설치가 완료되면 아래와 같은 화면이 나옵니다. Homebrew 설치 끝!
                        
        - mongoDB 설치하기
            
            터미널 창에 아래 코드 입력 후 엔터 (한줄씩 복사-붙여넣기 하세요)
            
            ```html
            brew tap mongodb/brew
            ```
            
            ```html
            brew install mongodb-community
            ```
            
        - mongoDB 실행해보기
            
            ```bash
            brew services start mongodb-community
            ```
            
        - 마지막으로, mongoDB 실행이 잘 되었는지 확인하기
            
            <aside>
            아래와 같은 화면을 만나면 잘 된 것입니다!
            
            </aside>
                        
            이제 mongoDB 설치가 모두 완료되었습니다!
            
- 2) Studio 3T
    - **[코드스니펫] Studio 3T 다운로드**
        
        ```jsx
        [**https://robomongo.org/download**](https://robomongo.org/download)
        ```
        
    - Download Studio 3T Free Today를 눌러주세요!
                
        <aside>
        👉 본인의 OS에 맞는 것을 선택 후에 다운로드 받으세요. 🙂
        
        </aside>
                
        설치가 완료된 후에 실행 시키면 
        
        <aside>
        👉 1. 정책 동의(agree) 창이 뜨면,  agree를 클릭해주시고요!
        2. 아래에선 아무것도 입력하지 않고 Next를 클릭해주시구요!
        3. 마지막에 이메일, 이름, 전화번호를 입력하라는 창이 뜹니다. 입력하시면 FINISH!😎
        
        </aside>        

---

## 02. 시작하기

[5-2_2차_exported.mp4](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1e181a24-e749-4550-8a19-012fb7d419fa/5-2_2%E1%84%8E%E1%85%A1_exported.mp4)

### MongoDB Client: Studio 3T 학습

- 1) Studio 3T란?
   
    - **Studio 3T**는 API의 사용을 도와주는 API Client처럼 MongoDB를 위해서 만들어진 **MongoDB Client**입니다.
   
    - **Studio 3T**의 GUI를 통해 MongoDB에 저장된 데이터를 관리하기 쉽게 보여주는 프로그램입니다.

- 2) DB Client와 API Client의 다른점은?
    
    서버에 연결해 데이터를 보내는것 까지는 같은 개념이지만 DBMS는 웹처럼 단순하지 않아 프로그램 사용법이 조금 더 복잡하고 DB의 데이터를 조회하거나, 관리할 수 있는 기능을 제공합니다.
    
    오늘 배우게 될 **Studio 3T**는 **DB Client** 종류 중 하나이며, **MongoDB**를 관리하기 위한 **DB Client**입니다.
    
- 3) Studio 3T로 내 컴퓨터에 설치한 MongoDB에 연결하기
   
    - 다운받으신 **Studio 3T**를 실행시켜주면 아래와 같은 화면이 나오게 됩니다.
                
    - 우측 상단의 `Connect` 버튼을 클릭하고, 뜨는 창에서  `New Connection` 버튼을 눌러줍니다.
    그 후에 나오는 창에서 하단 옵션을 선택하고 Next 버튼을 눌러 다음 단계로 넘어갑니다.
                
    - 아래와 같은 창이 나오면 db 이름을 입력해주고 주소 `localhost` 와 `27017`을 입력 해주고 Save버튼을 눌러 저장해줍니다.
                
    - 저장이 완료되면 MongoDB Connections 창으로 돌아오게 되는데 방금 만든 connection을 클릭해준뒤 Connect버튼을 눌러서 연결해줍니다.
    - 화면과 같이 왼쪽에 db 이름이 나오면 연결 완료입니다!
                
- 4) 간단하게 데이터 제어해보기
    
    [CRUD](https://docs.mongodb.com/manual/crud/) 명령어도 간단하게 체험해봅니다!
    이 수업은 MongoDB가 아닌 Node.js를 배우는것이 목적이기 때문에 개념 잡는 정도만 짚고 넘어갈 예정이에요! 😉
    
    - `db.collectionName.find({})`
   
    - `db.collectionName.insertOne({ key: "value", key2: "값" })`
   
    - `db.collectionName.deleteOne({ _id: ObjectId("...")})`
    
    그러면 위의 명령어를 직접 테스트 해볼 **데이터 베이스**를 생성해보겠습니다!
    
    - 위에서 생성한 sparta_db에서 마우스 오른쪽 버튼을 클릭하고 `Add Database`를 클릭합니다.
        
    - 아래와 같은 창이 나오면 Database 이름을 입력해주고, ok 버튼을 눌러 생성해줍니다.
     이름은 자유롭게 지어도 되나, 편의상 mongodb_prac으로 지었습니다.
    이제 데이터베이스가 생성되었어요!
        
    - 생성된 Database에서 다시 오른쪽 버튼을 클릭하여, **Open IntelliShell**을 선택합니다.
                
    - 우리는 Shell을 통해서 앞에 명령어들을 실행하고, 데이터를 조회 삽입 삭제 할 수 있습니다!
        
        - 먼저 데이터를 넣어볼까요?
        하단의 명령어를 Shell에 복사 붙여넣기하고, 바로 위에 → 버튼을 클릭하여 실행시켜줍니다.
        `db.mongodb_prac.insertOne({ key: "value", key2: "값" })`
                        
        - 데이터 넣었다면, 잘 들어갔는지 명령어로 확인해보겠습니다.
        앞선 명령어를 주석 처리한 후에 하단 명령어를 입력하고 실행시켜보세요!
        `db.mongodb_prac.find({})`
        아래 결과 창에 위에서 넣은 데이터가 잘 들어간 것을 확인할 수 있습니다.😎
                        
        - 이제 들어간 데이터를 한 번 삭제도 해보겠습니다.
        삭제할때는 앞에 삽입한 데이터를 ObjectId 값이 필요하여, 하단과 같이 결과창에서 데이터를 클릭한 후에 F3버튼 또는 오른쪽 마우스를 누르고 Document → View Document를 클릭해서 복사해주면 됩니다!
                        
            앞선 명령어를 주석 처리한 후에 하단 명령어를 입력하고 실행시켜보세요!
            `db.mongodb_prac.deleteOne({ _id: ObjectId("...")})`
                        
        

### 코드에서 MongoDB 이용

- 1) 내 코드에서 MongoDB에 연결하려면 뭘 해야 할까요?
    
    - 이제부터 우리는 API에 MongoDB를 연결해서 데이터를 주고 받아볼 예정입니다!
    
    - 이를 위해 코드에서도 DB Client 역할을 하는 무언가가 있어야 데이터베이스에 연결을 할 수 있는데요,
    우리는 `mongoose` 라는 도구를 이용해 데이터베이스에 연결할 예정입니다.
- 2) `mongoose` 설치
    
    - 우리가 작업하던 `spa_mall` 프로젝트를 열어줍니다!
    
    - npm 으로 기존 프로젝트에서 터미널을 열어 아래와 같이 입력해 `mongoose`를 설치 할 수 있습니다.
        
        ```bash
        npm install mongoose
        ```
        
        [mongoose](https://www.npmjs.com/package/mongoose)
        
- 3) `mongoose`의 문서(Document)란?
   
    - MongoDB에서 가지고 있는 각 데이터 하나하나를 **문서(Document)**라고 정의합니다.
   
    - 1개 이상의 **Key**-**Value**의 쌍으로 이루어져있습니다.
    
    ```jsx
    {
        "_id": ObjectId("6682192a1c155bd2f27881"),
        "name": "lyw",
    }
    ```
    
- 4) `mongoose`의 컬렉션(Collection)이란?
    
    - **JSON** 형식의 여러가지 **문서(Document)**를 보유할 수 있습니다.
    
    - 이후에 설명할 **관계형 데이터베이스(RDB)**의 **Table**과 동일한 역할을 합니다.

- 5) `mongoose`의 스키마(Schema)란?
    
    - 스키마는 **컬렉션(Collection)**에 들어가는 **문서(Document)**에 어떤 종류의 **값**이 들어가는지를 정의합니다.
   
   - 데이터를 모델링할 때 사용합니다.
   
    - ❓ 대표적인 스키마의 타입은 어떤것들이 있을까요?
        - null : null 값과 존재하지 않는 필드
            - ex: `null`
        
        - String : 문자열
            - ex: `“mongoDB”`
       
        - Number : 숫자
            - ex: `3.14`
       
        - Date : 날짜
            - ex: `new Date()`
       
        - Buffer : 파일을 담을 수 있는 버퍼, UTF-8이 아닌 문자열을 저장
            - ex: `0x65`
       
        - Boolean : `true` or `false`
            - ex: `true`
       
        - ObjectId(Schema.Types.ObjectId) : 객체 ID, 주로 다른 객체를 참조할 때 넣음
            - ex: `ObjectId()`
        
        - Array : 배열 형태의 값
            - ex: `["a", "b", "c"]`
        
- 6) `mongoose`의 모델(Model)이란?
   
    - 데이터베이스에 데이터를 **저장**해줄때 데이터의 구조를 담당합니다.
   
    - 스키마를 사용하여 만들고, MongoDB에서 실제 작업을 처리할 수 있는 함수들을 지니고 있습니다.
    
    - **문서(Document)**를 생성할 때 사용합니다.

- 7) 웹 서버에서 MongoDB에 연결
    
    <aside>
    ✅ 우리가 만들 Directory Structure는 아래와 같아요!
    
    </aside>
    
    ```
    .
    ├── app.js
    ├── routes
    │   ├── carts.js
    │   └── goods.js
    └── schemas
        ├── index.js
        ├── cart.js
        └── goods.js
    ```
    
    이제 mongoose를 이용해 데이터베이스에 연결합니다.
    
    - /**schemas/index.js 예시**
        
        ```jsx
        const mongoose = require("mongoose");
        
        const connect = () => {
          mongoose
            .connect("mongodb://localhost:27017/spa_mall")
            .catch(err => console.log(err));
        };
        
        mongoose.connection.on("error", err => {
          console.error("몽고디비 연결 에러", err);
        });
        
        module.exports = connect;
        ```
        
    - /**app.js 예시**
        
        ```jsx
        const connect = require("./schemas");
        connect();
        ```
        
- 8) 상품 모델 작성
    
     mongoose를 더 편하게 사용하기 위한 방법!
    Schema를 생성하여 데이터를 관리하기 위해 모델을 작성합니다.
    
    - /**schemas/goods.js 예시**
        
        ```jsx
        const mongoose = require("mongoose");
        
        const goodsSchema = new mongoose.Schema({
          goodsId: {
            type: Number,
            required: true,
            unique: true
          },
          name: {
            type: String,
            required: true,
            unique: true
          },
          thumbnailUrl: {
            type: String
          },
          category: {
            type: String
          },
          price: {
            type: Number
          }
        });
        
        module.exports = mongoose.model("Goods", goodsSchema);
        ```
        
- 9) 상품 생성 API 작성
   
    - 이제 상품 데이터를 코드에 넣어두는게 아닌, 데이터베이스에 추가할 수 있게 할 예정이에요!
    
    - 지금까지 만든 API는 `상품 목록 조회`, `개별 상품 조회` 로 모두 `조회`하는 API 였어요!
    이제는 **GET** 메서드 뿐만 아니라 **POST**와 같은 메서드에 대응하는 API도 개발해봅니다.
   
    - **REST API** 에 따르면 새로운 데이터를 추가하는 `method`는 `POST` 를 쓰는 것을 권장합니다.
    
    - **POST** 메소드의 특징은 **GET** 메소드와는 다르게 **body** 라는 추가적인 정보를 담아 서버에 전달 할 수 있기 때문에  `정보값`을 `body`라는 이름으로 넘겨줄 예정입니다.
   
    - **/app.js 예시**
        
        **body**로 전달 받은 **JSON** 데이터를 바로 사용할 수 없어요!
        
        **Express.js**에서 제공하는 **JSON middleware**를 사용해 **body**로 전달된 데이터를 사용할 수 있도록 해봅니다!
        📌 **이때 주의할 점이 있어요!** 
        하단의 **middleware**가 `app.use("/api", [goodsRouter])` 보다 위에 작성되어야 합니다.
        미들웨어는 순차적으로 거쳐가기 때문이예요! Express 페이지에서 배운 부분을 리마인드 시켜봅시다🔥
        
        ```jsx
        app.use(express.json());
        ```
        
    - **/routes/goods.js 예시**
        
        ```jsx
        const Goods = require("../schemas/goods");
        router.post("/goods", async (req, res) => {
        	const { goodsId, name, thumbnailUrl, category, price } = req.body;
        
          const goods = await Goods.find({ goodsId });
          if (goods.length) {
            return res.status(400).json({ success: false, errorMessage: "이미 있는 데이터입니다." });
          }
        
          const createdGoods = await Goods.create({ goodsId, name, thumbnailUrl, category, price });
        
          res.json({ goods: createdGoods });
        });
        ```
        
    - API 작성이 완료되면 **Thunder Client**로 상품 생성 API를 호출해보세요.
    
    - 먼저 저번과 같이 **Thunder Client** 아이콘을 클릭해 준뒤 **New Request**를 클릭해줍니다.
   
    - 그리고 아래와 같이 이번엔 **HTTP method**를 `POST`, URL은 [http://localhost:3000/api/goods](http://localhost:3000/api/goods) 를 입력해줍니다.
                
    - 이번에는 **Body**에 추가할 정보값을 입력해 줄건데요, 아래의 예시를 넣어서 `Json Content` 안에 넣어준뒤 Send 버튼을 눌러서 호출을 해봅시다.
    - **[코드스니펫] 콜라 정보**
        
        ```jsx
        {
           "goodsId": 2,
           "name": "시원한 콜라",
           "thumbnailUrl": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRk7JqMw7ZYZP4ZW136wcoMTmLzbrMIJzUWb1Dhu9cHwCPp0gA&usqp=CAc",
           "category": "drink",
           "price": 3000
        }
        ```
        
- 10) 저장된 데이터 Studio 3T로 확인하기
    - Success 메시지를 확인한 후 Studio 3T를 열어 `spa_mall` 데이터베이스를 새로고침 해보면 방금 입력한 데이터가 MongoDB에 들어간것을 확인할 수 있습니다!        

---

## 03. 장바구니 구현 (1)

- 1) 장바구니를 구현하기 위해서는 어떤 기능들이 필요할까요?
    
    처음에는 잘 감이 안올 수 있겠지만 연습하다보면 어떤 기능이 필요할지 알 수 있습니다!
    오늘은 그 첫걸음!
    
    장바구니 기능을 구현하려면 보통 아래의 기능이 필요합니다.
    
    1. 장바구니 목록 조회
    
    2. 장바구니에 상품 추가
    
    3. 장바구니의 상품 제거
   
    4. 장바구니의 상품 수량 수정
    
    생각보다 많죠? 오늘 전부 구현해야 하니 마음 단단히 먹고 시작해봅시다!
    
- 2) 장바구니 모델 작성
    
    - 이제 상품을 장바구니에 담기 위한 모델을 작성합니다.
    
    - 어떤 데이터를 넣어야 할까요?
        - 어떤 상품을 담았는지, 몇개를 담았는지 알 수 있어야 합니다!
    - **/schemas/cart.js 예시**
        
        ```jsx
        const mongoose = require("mongoose");
        
        const cartSchema = new mongoose.Schema({
          goodsId: {
            type: Number,
            required: true,
            unique: true
          },
          quantity: {
            type: Number,
            required: true
          }
        });
        
        module.exports = mongoose.model("Cart", cartSchema);
        ```
        
- 3) 장바구니 목록 조회 API 작성
   
    - 첫째로 장바구니의 데이터를 찾아와줍니다.
    
    - 그리고 장바구니 데이터베이스에는 `goodsId`와 `quantity` 정보밖에 담겨있지 않기 때문에 장바구니에 담겨있는 상품의 아이디에 맞는 상품 정보를 한번 더 가져와 줍니다.
   
    - **아래의 모양으로 응답하는것이 목적입니다.**
        
        ```jsx
        {
        	"carts": [
        		{
        			"quantity": 10,
        			"goods": {
        		    "goodsId": 3,
        		    "name": "시원한 콜라3333",
        		    "thumbnailUrl": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRk7JqMw7ZYZP4ZW136wcoMTmLzbrMIJzUWb1Dhu9cHwCPp0gA&usqp=CAc",
        		    "category": "drink",
        		    "price": 3000
        		  }
        		},
        		{
        			"quantity": 3,
        			"goods": {
        		    "goodsId": 1,
        		    "name": "시원한 콜라1",
        		    "thumbnailUrl": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRk7JqMw7ZYZP4ZW136wcoMTmLzbrMIJzUWb1Dhu9cHwCPp0gA&usqp=CAc",
        		    "category": "drink",
        		    "price": 3000
        		  }
        		}
        	]
        }
        ```
        
    
    그럼 `routes/carts.js` 파일을 생성해서 한번 작성해보세요!
    
    - **/routes/carts.js 예시**
        
        ```jsx
        const express = require("express");
        const Goods = require("../schemas/goods");
        const Cart = require("../schemas/cart");
        const router = express.Router();
        
        router.get("/carts", async (req, res) => {
          const carts = await Cart.find();
          const goodsIds = carts.map((cart) => cart.goodsId);
        
          const goods = await Goods.find({ goodsId: goodsIds });
        
          const results = carts.map((cart) => {
        		return {
        			quantity: cart.quantity,
        			goods: goods.find((item) => item.goodsId === cart.goodsId)
        		};
          });
        
          res.json({
            carts: results,
          });
        });
        
        module.exports = router;
        ```
        
    - **/app.js 예시**
        
        ```jsx
        const cartsRouter = require("./routes/carts");
        
        app.use("/api", [goodsRouter, cartsRouter]);
        ```
        
    - API가 잘 동작하는지 확인해봅니다!
        - 이전에 Thunder Client로 요청했던것처럼 GET 메소드로 `http://localhost:3000/api/carts` 를 호출해봅시다.
        - 아래 스크린샷처럼 Status는 200 이 나왔지만 Response 안에 carts에 빈 배열이 오는 것이 정상입니다!
        이는 장바구니안에 아무것도 아직 추가를 하지 않았기 때문입니다. 😇
            
            ![스크린샷 2022-06-06 오전 2.39.33.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0ed1730a-ad61-452a-866f-cf3e4e83cabb/스크린샷_2022-06-06_오전_2.39.33.png)
            
        

---

## 04. 장바구니 구현 (2)

- 1) 장바구니에 상품 추가 API 작성
    
    이 API는 상품 추가 API와 거의 비슷하게 구현할 수 있습니다!
    
    - 구현하려면 어떤 값이 필요할까요?
        
        - goodsId
       
        - quantity
   
    - 어떻게 구현하면 될까요?
        
        POST 메서드와 `/goods/:goodsId/cart` 주소에 대응하는 API를 만들어보세요!
        
    - 이후 받아온 `:goodsId` 값을 통해 이미 장바구니에 상품이 들어가 있는지 확인 후, 존재하면 수량만 수정하고, 존재하지 않는다면 새로운 카트에 상품정보를 새로 생성하도록 작성해볼거예요!
    
    - **/routes/goods.js 예시**
        
        ```jsx
        const Cart = require("../schemas/cart");
        router.post("/goods/:goodsId/cart", async (req, res) => {
          const { goodsId } = req.params;
          const { quantity } = req.body;
        
          const existsCarts = await Cart.find({ goodsId: Number(goodsId) });
          if (existsCarts.length) {
            return res.json({ success: false, errorMessage: "이미 장바구니에 존재하는 상품입니다." });
          }
        
          await Cart.create({ goodsId: Number(goodsId), quantity: quantity });
        
          res.json({ result: "success" });
        });
        ```
        
    - [http://localhost:3000/api/goods/**:goodsId**/cart](http://localhost:3000/api/goods/2/cart)
        
        - URL에 수정을 원하는 **`:goodsId`**값을 넣어준후 body에 quantity 값을 json형태로 입력한뒤 POST method로 요청을 해줍니다.
            
            
        - 위와 같이 success 메시지가 나온 뒤 Studio 3T에서 새로고침을 해주면 아래와 같이 carts document 에 장바구니 데이터가 저장되어 있는것을 확인할 수 있습니다.
            
            
- 2) 장바구니의 상품 수량 수정 API 작성
   
    - 이번 API는 장바구니에 상품  추가 API와 굉장히 비슷한 코드의 모습을 하고 있습니다.
    
    - 하지만 이번에는 POST 메소드가 아닌 PUT 메소드를 사용해 데이터를 update 해줄것 입니다.
   
    - URI는 추가 API와 같은 포맷을 가지고 있지만, 이번 API에서는 간단하게 goodsId를 이용해서 상품정보가 장바구니내에 존재한다면 body를 통해 받아온 quantity 값에 맞게 상품 수량을 수정해 줍니다.
    
    - **/routes/goods.js 예시**
        
        ```jsx
        router.put("/goods/:goodsId/cart", async (req, res) => {
          const { goodsId } = req.params;
          const { quantity } = req.body;
        
          const existsCarts = await Cart.find({ goodsId: Number(goodsId) });
          if (existsCarts.length) {
            await Cart.updateOne({ goodsId: Number(goodsId) }, { $set: { quantity } });
          }
        
          res.json({ success: true });
        })
        ```
        
    - [http://localhost:3000/api/goods/:goodsId/cart](http://localhost:3000/api/goods/2/cart)
        
        New Request로 PUT 메소드를 설정해준뒤 goodsId에 맞는 상품의 수량을 body에 담아 요청해 수정해봅니다.
                
        입력한 값과 마찬가지로 수량이 5로 수정되면 성공입니다!
        
- 3) 장바구니의 상품 제거 API 작성
    
    - 이번 API는 장바구니에 상품 추가 API 와 동일한 URI를 사용하게 됩니다.
    
    - 하지만 이번에는 간단하게 goodsId를 통해 상품이 장바구니 안에 존재한다면 장바구니 내에서 상품 정보를 삭제해줍니다.
    
    - **/routes/goods.js 예시**
        
        ```jsx
        router.delete("/goods/:goodsId/cart", async (req, res) => {
          const { goodsId } = req.params;
        
          const existsCarts = await Cart.find({ goodsId });
          if (existsCarts.length > 0) {
            await Cart.deleteOne({ goodsId });
          }
        
          res.json({ result: "success" });
        });
        ```
        
    
    <aside>
    👉 데이터를 지울 때는 보통 `DELETE` `method` 를 사용합니다.
    지우는 행동에서는 URL 만으로 지워야할 리소스를 명시하는데 충분하다는 이유가 있습니다. 😎
    
    </aside>
    
    - [http://localhost:3000/api/goods/**:goodsId**/cart](http://localhost:3000/api/goods/2/cart)
        
        DELETE 메소드를 통해 호출을 하면 아래와 같이 success 메시지와 Studio 3T 내에서 장바구니가 사라진것을 볼 수 있습니다.
                

---

## 05. Quiz

<aside>

❓ **1. "장바구니의 상품 수량 수정 API"에서 수량을 1 미만으로 보내면 요청 거부 기능 구현**

- 상세내용
   
    - 현재 장바구니 상품 수량을 0 또는 그 이하의 값으로 바꿀 수 있는 상태입니다.
   
    - 프론트엔드에서 어떤 값을 가지고 API를 호출하더라도 API는 이상한 데이터가 저장되게 하면 안됩니다!
    
    - 상품 수량이 1 미만(ex. 0)인 값을 가지고 호출되면 서버에서는 HTTP status code 400으로 빈 응답을 반환하도록 구현해보세요!
</aside>

<aside>
❓ **2. “장바구니 목록 조회 API”의 경로 변경하기**

- 상세내용
   
    - 아마 지금은 장바구니 목록 조회 API만 “/api/carts” 경로로 API를 제공하고 있을거예요!
    
    - “/api/carts” → “/api/goods/cart” 경로로 제공할 수 있도록 변경해보세요!
   
    - cart 리소스가 goods 리소스에 의존하는 데이터라는것을 간접적으로 표현하도록 해볼 예정이에요!
</aside>

## 06. Quiz 답안

- `장바구니의 상품 수량 수정 API` 답안
    
    ```jsx
    router.put("/goods/:goodsId/cart", async (req, res) => {
      const { goodsId } = req.params;
      const { quantity } = req.body;
    
      if (quantity < 1) {
        res.status(400).json({ errorMessage: "수량은 1 이상이어야 합니다." });
        return;
      }
    
      const existsCarts = await Cart.find({ goodsId: Number(goodsId) });
      if (existsCarts.length) {
        await Cart.updateOne({ goodsId: Number(goodsId) }, { $set: { quantity } });
      }
    
      res.json({ success: true });
    });
    ```
    
- `장바구니 목록 조회 API` 답안
   
    1. `/routes/carts.js` 에 있던 라우터 코드를 `/routes/goods.js` 로 옮기기
    
    2. router가 입력받는 주소 `/goods/cart` 로 변경하기
        
        ```jsx
        router.get("/goods/cart", async (req, res) => {
          const carts = await Cart.find();
          const goodsIds = carts.map((cart) => cart.goodsId);
        
          const goods = await Goods.find({ goodsId: goodsIds });
        
          res.json({
              carts: carts.map((cart) => ({
                  quantity: cart.quantity,
                  goods: goods.find((item) => item.goodsId === cart.goodsId),
              })),
          });
        });
        ```
        
    3. `/app.js` 에서 `cartsRouter` 제거
        
        ```jsx
        const cartsRouter = require("./routes/carts"); // <- 해당 줄 제거
        
        app.use("/api", [goodsRouter]);
        ```
        
    4. `/routes/carts.js` 파일 제거

---

## etc) 키워드

<aside>
💡 더 찾아보면 좋을 키워드들에 대한 힌트에요!

1. **RDBMS**와 **NoSQL**은 어떻게 다를까요?

2. **PUT**과 **PATCH** Method의 차이점은 무엇일까요?

3. **URL**과 **URI**은 다른걸까요?

</aside>