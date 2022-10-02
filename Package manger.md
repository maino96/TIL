## 01. Package Manager

- 1) Package Manager 란?
    
    - 패키지 매니저는 패키지를 손쉽게 다루는 작업을 안전하고 편리하게 사용하기 위한 툴입니다!
   
    - 다른 사람들이 만들어준 코드를 다운로드 받거나, 자신의 코드를 배포하여 다른 사람이 쓸 수 있도록 할 수 있습니다.
    
    - Node.js에서 대표적으로 사용하는 패키지 매니저는 **npm**과 **yarn**이 존재합니다.
    
    - ❓ 패키지는 뭘까요?
       
        - **npm**이나 **yarn**에 업로드된 Node.js 모듈을 패키지라고 부릅니다.
        
        - **모듈**이 다른 **모듈**을 참조하여 사용하는 것과 같이, **패키지**도 다른 **패키지**를 사용할 수 있습니다.
            
            - 이런 관계를 **의존 관계**라고 표현합니다.

- 2) npm 이란?
    
    - **npm**은 자바스크립트에서 사용할 수 있는 **패키지(모듈) 관리자**입니다!
    
    - 여러분이 **Python**과 같은 언어에서 **Flask**나 **BeautifulSoup**과 같은 패키지를 설치할 때 **pip**가 필요했다면 **Node.js**에서는 **npm을** 통해 필요한 패키지를 설치할 수 있습니다.
    
    - 혹시 **pip**를 모르신다면 우선 **npm**은 "*Node.js를 사용하는데 필요한 패키지를 설치해주는 프로그램*" 이라고 생각하시면 좋습니다 🙂
    
    - **npm**을 통해 여러분이 사용할 라이브러리를 쉽게 설치하고 버전을 관리할 수 있고, 제거할 수도 있습니다.
    
    - [npmjs.com](http://npmjs.com) 에서 검색해서 확인할 수 있는 패키지만 설치가 가능합니다.
    
    - 누구나 새로운 패키지를 등록할 수 있습니다.
   
    - Node Package Manager의 약자로 **npm**이라는 이름을 가졌지만, 지금은 Node.js와 관계없이 프론트엔드에서만 사용 가능한 자바스크립트 패키지들도 모두 등록되어 있습니다.

- 3) yarn 이란?
    
    - **npm**의 대체제로 **FaceBook**이 출시한 패키지 매니저입니다!
    
    - **npm**에서 부족한 부분을 보완하여 편리한 기능이 추가되었고, 더욱 빠른 속도로 패키지를 관리할 수 있는 패키지 매니저입니다.
    
    
    
- 4) Package.json 이란?
    
    - 설치한 패키지들의 **버전을 관리**할 때 사용하는 파일입니다.
    
    - 동일한 패키지를 사용하더라도 버전별로 기능을 다르게 사용할 수 있으므로 특정한 버전을 설치할 때 필요합니다.
    
    - 패키지 관리 외에도 **프로젝트명**, **작성자**, **라이센스 정보**등 다양한 메타데이터들을 기록할 수 있습니다.
   
    - **npm**과 **yarn** 모두 동일한 `package.json` 파일을 참조합니다.

- 5) Pacakge-lock.json 이란?
    
    - `package.json`파일에서 정의한 패키지 외에도 `node_modules`에 들어있는 패키지들의 버전과 의존 관계가 상세하게 기록되어 있습니다.
    
    - **npm**으로 패키지를 **설치, 수정, 삭제**할 때마다 패키지들의 **의존 관계**를 `package-lock.json`파일에 저장합니다.
    
    - 저장된 패키지들은 **정확히 일치하는 버전**만 기록되므로, 프로젝트에서 의존하는 패키지 버전을 정확하게 관리할 때 사용할 수 있습니다.

---

## 02. 배포를 위한 npm 학습

- 1) npm 복습
    
    여러분이 사용해본 npm 기능은 아래와 같습니다.
    
    <aside>
    🚩 VS Code 하단의 Terminal에서 진행하면 됩니다!
    
    </aside>
    
    - `npm init`
     
        - 명령어를 통해 package.json 파일을 만들 때 사용됩니다. package.json 은 npm 으로 설치된 모듈에 대한 정보가 들어있습니다.
        
        - 새로운 프로젝트나 패키지를 만들 때 사용됩니다.
       
        - 패키지명, 프로젝트 버전, Github URL등 프로젝트와 관련된 다양한 정보를 설정할 수 있습니다.
    
    - `npm install express`
        
        - npm 으로 모듈을 설치할 때 쓰는 명령어입니다.
        
        - `install` 대신 `i` 라는 별명을 대신 사용할 수 있습니다.
       
        - `install` 뒤에 따라오는 `express` 는 설치하고자 하는 모듈의 이름을 명시합니다.
        
        - `npm install express` 로 `express` 한개의 모듈을 설치할 수 있는데 띄어쓰기로 구분을 하여 여러개의 모듈을 설치하는것도 가능합니다.
        
        ex) `npm install express mongoose jest`
- 2) node_modules?
    
    - `package.json` 파일 내용 기반으로 `npm install` 명령어를 통해 설치된 모듈 파일들이 모여있는 곳입니다.
    
    - `package.json`에 설정된 모듈과 해당 모듈들이 참고하고 있는 또 다른 모듈도 함께 설치됩니다.
    
    - 여러분이 사용중인 환경에 맞는 파일들이 설치되기 때문에 이 폴더는 다른곳에 공유하거나 배포할 때 포함하면 안됩니다.

- 3) npm install?
    
    - 명령어가 입력되면 `package.json` 기반으로 `node_modules`에 명시된 모듈들을 설치해주는 명령어 입니다.
    
    - 내 프로젝트를 다른사람에게 공유하거나 다른 사람의 프로젝트를 사용할 때 모듈을 설치하기위해 실행하는 명령어입니다.
    
    - ❓ **devDependencies**
       
        - 개발 단계에서만 필요한 모듈들을 설치할 경우 이곳에 포함됩니다.
        `npm install -D (모듈이름)` 으로 추가할 수 있습니다.
       
        - 참고: [https://selenehyun.notion.site/NPM-bb21551cb0e649ee9c0fa28bf3e52201](https://www.notion.so/bb21551cb0e649ee9c0fa28bf3e52201)

- 4) 마무리
    
    - `node_modules` 공유하거나 배포할때 포함 X
    
    - `package.json`만 있으면 언제든 환경에 맞는 모듈들 설치 가능
    
    - 이미 추가된 모듈 설치는 `npm install`

---

## etc) 키워드

<aside>
💡 더 찾아보면 좋을 키워드들에 대한 힌트에요!

1. 패키지 매니저를 사용하는 이유는 어떤점들이 있을까요?
2. npm과 yarn은 각각 어떤 장단점들이 있을까요?
3. package.json이 왜 필요할까요?
</aside>