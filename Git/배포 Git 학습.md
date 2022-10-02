## 01. 배포를 위한 Git 학습

- 1) Git 이란 뭘까?
    - Git 은 체계적인 개발과 프로그램의 배포를 도와주는 **형상 관리 도구**, 또는 **버전 관리 시스템** 입니다.
- 2) 형상 관리 도구는 왜 사용할까요?
    - 프로젝트의 개발 단계에서 소스 코드의 버전을 효과적으로 관리 할 수 있습니다.
    - **같은 파일**을 **여러명이서 동시에 작업**할 수 있게 합니다.
- 3) Git 사용에 필요한 개념 배워보기
    - Repository
        
        **레파지토리란**? **모든 파일의 변경 사항을 저장할 수 있는 저장소**입니다.
        
        여기서도 두 종류가 존재합니다!
        
        - **Local Repository**: 여러분의 컴퓨터에 존재하는 **Repository** 그 자체를 말합니다.
        - **Remote Repository**: GitHub와 같이 Git 서버에서 제공되는 **Repository**를 말합니다.
    - Commit
        
        이전 변경사항 기준으로 **새로 변경된 내용을 기록하는 단위**를 **Commit**이라 부릅니다.
        
    - Branch
        
        여러 사람이 하나의 레파지토리에서 작업을 할 때 **작업 내용이 충돌하지 않도록 해주는 개념**입니다.
        우리는 아직 브랜치를 거의 사용하지 않을 예정이기 때문에 개념정도만 배우고 넘어갑니다!
        
        참고: [https://backlog.com/git-tutorial/kr/stepup/stepup1_1.html](https://backlog.com/git-tutorial/kr/stepup/stepup1_1.html)
        
- 4) Git 명령어 맛보기
    - `git init`
        
        Git 저장소를 초기화 하여 해당 프로젝트 폴더를 Git repository 로 만들어줍니다.
        
    - `git add`
        
        지금 변경한 변경 사항을 스테이징 영역(Staging Area)에 올립니다.
        
        - `git add .`: 모든 변경 사항을 올린다.
        - `git add app.js`: app.js 변경사항만 올린다.
    - `git commit`
        
        스테이징 영역에 올라가 있는 변경사항을 하나의 기록(History)으로 남깁니다.
        
    - `git remote add`
        
        `git remote add <name> <url>` 명령어로 Local Repository 에 `<name>`이라는 이름의 Remote Repository 를 추가할 수 있습니다.
        `<url>` 에는 Remote repository의 주소가 들어갑니다.
        
    - `git push`
        
        Local Repository에 존재하는 Push 되지 않은 변경사항을 Remote Repository에 업로드 합니다.
        
    - `git clone`
        
        Remote Repository로 부터 프로젝트를 복제합니다.
        
    - `git pull`
        
        Remote Repository에 새로 올라온 변경사항을 Local Repository로 가져옵니다.
        
    - **.gitignore** 파일?
        - **.gitignore** 라는 이름의 파일을 프로젝트 폴더 최상단에 두고 파일 내용을 아래처럼 넣어보세요!
            
            ```jsx
            node_modules
            ```
            
        - 이전 시간에 배웠던 것 처럼 `node_modules` 폴더는 git의 변경사항에 속하지 않게 해주는 역할을 해서 여러분 컴퓨터에 있는 `node_modules` 폴더를 업로드하지 않도록 도와줍니다.
- 5) 배포 할때 Git은 어떻게 활용될까요?
    - 처음 배포하는 서버인 경우
        1. `git clone`
        2. `npm install`
        3. 서버 켜기
    - 이미 배포 했던 서버의 코드를 최신 코드로 재시작 하고 싶은 경우
        1. `git pull`
        2. (필요한경우) `npm install`
        3. 서버 재시작
- 6) 배포 할 때 Git을 사용하면 어떤 장점이 있을까요?
    - 위에서 형상 관리 도구를 사용하는 이유와 비슷합니다!
    - 원하는 때에 원하는 형상으로 서버를 켤 수 있습니다.
        - 서버를 최신 형상으로 올렸는데 갑자기 예기치 못한 에러가 발생한다면?
        곧바로 이전 형상으로 돌려서 다시 서버를 켤 수 있습니다!
        - 물론 지금은 알려드리지 않은 git의 checkout 기능을 알아야 하지만 일단 Git을 사용한다면 위와 같은 상황에 대비가 가능한것이죠 😉

## 02. GitHub에 Repository 올리기

- 1) GitHub 웹 사이트 접속 및 로그인
    - **[코드스니펫] GitHub 주소 복사**
        
        ```jsx
        https://github.com/
        ```
        
    - 이전에 숙제 시간에 가입했던 계정 혹은 기존에 갖고 계시던 계정으로 로그인을 해주세요!
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/84dcf398-acbd-46c6-b6f5-b39e4c641a91/Untitled.png)
        
- 2) GitHub에 Repository 생성
    - 레파지토리 생성 페이지 이동
        
        우측 상단 프로필 옆 `+`  버튼을 눌러 `New repository` 페이지로 이동합니다.
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cf4d8de4-7a7d-4aad-8c2b-50d198ad0ea0/Untitled.png)
        
    - 레파지토리 생성 정보 입력 및 생성
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/040e7389-9521-43d4-9172-080133af3127/Untitled.png)
        
        - Repository name: `nodejs_spa_mall`
            - 원래의 프로젝트 이름과 달라도 상관 없어요. 이건 Remote Repository의 이름입니다!
            - 수업 진도를 따라오는것에 문제만 없다면 다른 이름으로 하셔도 됩니다!
        - Description: 생략 혹은 자유롭게 입력
        - Public or Private: `Public`
            - Public: 아무나 여러분의 레파지토리를 볼 수 있어요! 지금은 민감한 보안 정보가 없고,
            **배포를 쉽게 하기 위해 Public**으로 설정하고 진행합니다!
        - Initialize this repository with: **아무것도 체크하지 말것!**
            - GitHub가 **Remote Repository**를 만들어준 뒤 기본 파일들을 추가해줄지 물어보는 항목입니다.
            - 우리는 이미 존재하는 Local Repository가 있기 때문에 절대로 체크하지 않도록 합니다!
            - 만약 체크하면? **Remote Repository**에 다른 **Commit History**가 생겨납니다.
            이렇게 되면 **Local Repository**에 있는 Commit History를 **Remote Repository**에 올리려고 시도하는 경우 충돌이 발생해 정상적으로 올릴 수 없습니다.
        
        위와 같이 잘 입력했다면 `Create repository` 버튼을 눌러 레파지토리를 생성해줍니다!
        아래와 같은 화면이 보인다면 성공!
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/24ffb7a5-00d7-4d43-b768-e81eac78d9ba/Untitled.png)
        
- 3) SSH Key 발급받기
    
    생성한 Remote Repository를 사용하기 위해선 Local 환경에서 Github를 사용하기 위해 인증을 받아야합니다.
    
    기존에는 Private Repository를 접근하거나, Commit, Push 등의 기능을 사용하기 위해선 로그인 방식을 많이 채용하였는데요, 2021년 8월 13일 부터 Github를 인증할 때 계정을 로그인하는 방식으로 진행할 수 없습니다.
    
    그로인해 현재는 Github를 사용하기 위해 인증을 받는 방법은 대표적으로 2가지가 존재하는데요.
    
    첫번째는 **Personal access token을 등록**하는것과
    
    두번째는 **SSH를 등록**하는것이 있습니다.
    
    저희는 SSH Key를 발급받아 Github 계정을 인증받도록 하겠습니다.
    
    - 터미널에서 SSH Key 발급
        
        Window에선 Git Bash, mac에선 터미널을 이용해서 SSH Key를 발급 받도록 하겠습니다.
        
        - **[코드 스니펫] 터미널에서 SSH Key 발급받기**
            - `“archepro84@gmail.com”`은 자신의 이메일로 변경해야합니다.
            
            ```jsx
            ssh-keygen -t rsa -b 4096 -C "archepro84@gmail.com"
            ```
            
        
        ![스크린샷 2022-09-07 오전 1.45.53.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/26120a68-abc7-4459-9ae1-a4ccd7b8fa45/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_1.45.53.png)
        
        - RSA 키를 등록할 때 위치를 지정하거나, 패스워드를 지정하지 않고 기본값으로 설정합니다.
        
        ![스크린샷 2022-09-07 오전 1.47.32.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9f553040-94ad-49dd-8540-f08a6bff8751/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_1.47.32.png)
        
        - `~/.ssh` 경로에 2개의 `rsa` 파일이 생성된 것을 확인할 수 있습니다.
    - 설정 페이지로 이동
        - 정상적으로 SSH Key를 발급 받은 경우 개인키를 Github에 등록해야합니다.
        - 우측 상단에 프로필을 눌러 Settings 페이지로 이동합니다.
        
        ![스크린샷_2022-09-07_오전_1_55_31.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/df7d87da-1e97-40f7-9147-6dc9c48c2e47/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_1_55_31.png)
        
    - SSH and GPG keys 페이지로 이동
        - 좌측에 있는 SSH and GPG Keys 탭을 눌러 페이지를 이동합니다.
        
        ![스크린샷_2022-09-07_오전_1_58_41.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a9a109aa-bdc0-4111-adb4-bee44b1aede9/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_1_58_41.png)
        
    - SSH Key 등록 페이지로 이동
        - 우측 상단에 있는 New SSH Key 버튼을 눌러 SSH Key를 등록하는 페이지로 이동합니다.
        
        ![스크린샷_2022-09-07_오전_2_01_10.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/569ad470-da92-4d4c-8b2a-60d0cb45ac49/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2_01_10.png)
        
    - SSH Key 복사하기
        - SSH Key를 등록하기 전 저희가 발급했던 SSH Key를 가져와야하는데요.
        - 코드스니펫을 이용해서 저장되어 있는 SSH Key를 확인하도록 하겠습니다.
        
        - **[코드 스니펫] SSH Key 복사하기**
            
            ```jsx
            cat ~/.ssh/id_rsa.pub
            ```
            
        
        ![스크린샷 2022-09-07 오전 2.09.43.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/694ce8b0-8677-4d6f-afce-873b7e5c5bf6/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2.09.43.png)
        
        - 출력된 SSH Key를 복사하고, 다음 단계로 넘어갈게요!
        
    - SSH Key 등록하기
        
        ![스크린샷 2022-09-07 오전 2.12.23.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4fe03dd0-2665-467b-9696-ecd6c5ab8938/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2.12.23.png)
        
        - Title: SSH Key의 이름이에요. 원하는대로 설정해주세요!
        - key type: 등록하려는 SSH Key의 타입이에요. 저희는 `Authentication Key`로 설정하겠습니다.
        - Key: 이전 단계에서 복사한 SSH Key 정보를 등록해주세요!
        
        **마지막으로 Add SSH Key 버튼을 눌러 등록하겠습니다!** 
        
        ![스크린샷 2022-09-07 오전 2.13.36.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e58c98f8-b558-4267-9a48-b0feb7a627f5/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2.13.36.png)
        
        SSH키가 정상적으로 등록된 것을 확인할 수 있습니다! 😁
        
- 4) Local Repository에 Remote Repository로 올리기
    - **Remote Repository** 주소 복사
        
        ![스크린샷_2022-09-07_오전_2_16_24.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5820ef2e-de68-4171-be6c-ae60799c5220/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2_16_24.png)
        
        - 저희는 이전단계에서 SSH Key를 등록했습니다. SSH 버튼을 누른 뒤 주소를 복사해주세요!
        
    - **Remote Repository**를 **Local Repository**에 추가: `git init` & `git remote add`
        
        위에서 복사한 주소를 아래 양식에 맞춰 VS Code의 터미널에 넣어 실행해주세요!
        **반드시 SSH가 선택된 상태에서 복사하는것 잊지 마세요!**
        
        ![엔터를 쳐서 아무것도 안나오면 에러가 발생하지 않은것이므로 정상입니다! 
        확인해보고 싶다면 `git remote -v` 명령어를 입력하여 현재 프로젝트의 remote 저장소를 확인할 수 있습니다!](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ed9fc227-0781-4e63-a65b-410b7a8d58c4/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2.22.57.png)
        
        엔터를 쳐서 아무것도 안나오면 에러가 발생하지 않은것이므로 정상입니다! 
        확인해보고 싶다면 `git remote -v` 명령어를 입력하여 현재 프로젝트의 remote 저장소를 확인할 수 있습니다!
        
        ```jsx
        git init
        git remote add origin <github 페이지에 나오는 주소>
        ```
        
        - **명령어 예시**
            
            ```jsx
            git remote add origin git@github.com:archepro84/nodejs_spa_mall.git
            ```
            
    - **Local Repository**를 **Remote Repository**에 올리기: `git add` & `git commit` & `git push`
        
        이번에는 스파르타 쇼핑몰 프로젝트에서 Add → Copmmit → Push 순서대로 진행할거에요!
        
        저희는 현재까지 구현한 코드들을 Git에 등록해야하는데요, 그러기 위해선 `git add` → `git commit`을 입력해야합니다!
        
        ```jsx
        git add .
        git commit -m "first commit"
        // 모든 변경된 파일을 등록하고, first commit이라는 커밋 메시지로 업로드한다라는 뜻이에요!
        ```
        
        Github에 업로드하기 위한 준비가 전부 완료되었습니다! 
        
        다음으로는 등록한 커밋을 Github에 업로드해야겠죠? 
        
        **커밋**을 **Remote Repository**인 GitHub의 **레파지토리**에 올리는 명령어가 `git push`예요!
        
        ```bash
        git push -u origin master
        // 해당 명령어 입력시에 오류가 발생한다면 master 대신에 main으로 명령어를 수정합니다!
        ```
        
        ![스크린샷 2022-09-07 오전 2.31.59.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/30518888-aad7-4a4b-8fd5-f335c48db802/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2.31.59.png)
        
        `git push`를 입력하면 위와 같은 메시지가 출력되는데, **yes**를 입력하도록 하겠습니다!
        
        ![스크린샷 2022-09-07 오전 2.33.23.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c6ad62f4-26cc-439a-9069-8a405b549ead/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2.33.23.png)
        
        성공적으로 **spa_mall** 프로젝트가 Github에 업로드되었습니다!
        
    - **GitHub**에서 확인해보기
        
        ![스크린샷 2022-09-07 오전 2.40.48.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/094e6d00-995b-476a-b070-1588f1a38f21/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-09-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2.40.48.png)
        
        위와 같이 나온다면 성공!
        
        여러분은 지금 **Local Repository**에 **Remote Repository**를 연결하고, **Local Repository**에 있던 **Commit History**를 **Remote Repository**에 업로드한거예요!
        
        여기까지 마쳤다면 **Remote Repository**에 있는 내용은 언제 어디서든 여러분 컴퓨터에 받아서(**clone**) 작업이 가능합니다!
        
- 5) 최신 변경사항 올려보기
    
    아마 여러분이 저 몰래 **Git Commit**을 따로 하지 않았다면 첫 커밋 이후 새로운 변경사항들이 생겼을거예요!
    새로운 변경사항을 커밋으로 만들어서 다시 **Remote Repository**인 GitHub에 올리도록 해봅니다.
    
    - 변경사항이 있는지 확인: `git status`
        
        ```jsx
        git status
        ```
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/04481ea2-18c8-494b-ad75-37ed7e7854e8/Untitled.png)
        
        - **modified**: 수정된 파일이 2개 존재한다고 합니다.
        - **Untracked files**: `static` 폴더 하위의 파일이 모두 Untracked 상태라고 알 수 있습니다.
        
        <aside>
        💡 **Git에서 Untracked 상태는 뭘까요?**
        아직 Git을 통해 관리하지 않고 있는 상태에 있는 파일을 말합니다!
        
        </aside>
        
    - 변경사항을 Staging Area 에 올리고 Commit
        
        이전에 했던것과 동일합니다!
        `git add` 명령어를 이용해 **변경사항**을 **Staging Area**에 올리고 `git commit` 명령어를 이용해 커밋을 해줍니다.
        
        ```jsx
        git add .
        git commit -m "프론트엔드 코드 추가"
        ```
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9217aa86-27ff-4c33-a38e-df7e7070485e/Untitled.png)
        
    - Commit을 푸시!
        
        이번에는 처음과 달리 짧게 해도 됩니다!
        
        ```jsx
        git push
        ```
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/20c558c8-1dae-4b3d-8bf1-9a8d2e4db1dd/Untitled.png)
        
        <aside>
        💡 **왜 명령어가 조금 다를까요?**
        
        처음엔 Remote Repository에 `master` 라는 이름의 브랜치가 없었기 때문에 새로운 브랜치를 생성하기 위해 `-u` 옵션을 붙였고,
        Remote Repository 이름으로 등록해둔 `origin` 을 적어 어떤 Remote Repository에 Commit을 push할건지 적었습니다.
        
        Remote Repository에도 존재하는 브랜치에서 작업하는 경우 단순히 `git push` 명령어로도 Local Repository에 있는 Commit을 올릴 수 있습니다.
        
        </aside>
        
    - GitHub에서 확인해보기
        
        아래 사진과 같이 방금 올린 커밋 메세지와 함께 확인이 가능해야 합니다.
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3337001b-dc5c-487d-a27a-6a5276dd7af2/Untitled.png)
        
    - 만약 Push를 하지 않는다면?
        - 여러분의 컴퓨터에 있는 Local Repository에만 기록이 남아 비상시에 다른 컴퓨터로는 작업이 불가능합니다!
        - 때문에 아래와 같은 개발자 화재 대피 요령이라는 이미지도 돌아다닙니다 😂
            
            ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/50842f56-9a8a-4505-a956-e753b143cf4d/Untitled.png)
            
            ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0b0b11de-e632-4065-8522-35bc3b17458b/Untitled.png)
            
- 6) 마무리
    - 우리는 이제 **GitHub**라는 **Remote Repository**에 코드를 올릴 수 있게 되었습니다! 🎉
    - 이후 시간에는 이 **Remote Repository**에 있는 코드를 서버에서 사용해 여러분의 서버 컴퓨터에서 서버 프로그램이 실행될 수 있게 할 예정입니다. 😁
    - 많은 회사에서는 이 GitHub와 같은 Git 호스팅 서비스를 이용해 협업과 코드 리뷰라는것을 진행하고 있는데요, 아직 시작은 미약하지만 여러분도 할 수 있는 첫걸음을 내딛었다고 볼 수 있습니다!

<aside>
💡 더 찾아보면 좋을 키워드들에 대한 힌트에요!

1. Git에서 Branch는 어떻게 쓰는걸까요? 왜 쓰는걸까요?
2. Github에서 PR은 무엇일까요?
</aside>