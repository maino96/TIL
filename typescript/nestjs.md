Node.js는 손쉽게 사용할 수 있고 뛰어난 확장성을 가지고 있지만, 과도한 유연함으로 인해 SW의 품질이 일정하지 않고 알맞은 라이브러리를 찾기 위해 사용자가 많은 시간을 할애해야 한다는 단점이 있다.

이에 반해 NestJS는 데이터베이스, ORM, 설정(Configuration), 유효성 검사 등 수많은 기능을 기본 제공하고 있다. 그러면서도 필요한 라이브러리를 쉽게 설치하여 기능을 확장할 수 있는 Node.js 장점은 그대로 가지고 있는 프레임워크다.

프로젝트를 설치하면 다음과 같은 파일들이 생긴다

app.controller.ts : 하나의 라우트가 있는 파일

app.controller.spec.ts : app.controller.ts 파일을 테스트하는 파일

app.moudule.ts : 애플리케이션의 루트 모듈

app.service.ts : 라우트의 로직을 작성하는 파일

main.ts : NestFactory를 사용하여 Nest 애플리케이션 인스턴스를 생성하는 애플리케이션 엔트리 파일

이렇게 처음 생긴 파일들은
service -> controller -> module -> main
이 순서대로 의존성을 가진다.

NestJS를 실습했을 때는 기본형에서 조금 변형된 더 실용적인 방법을 사용했다.


의존성은

service-> resolver -> starbucks.module -> app.module -> main

starbucks service,resolver,starbucks.module을 한 폴더 에 모으고 기본형과 같이 연결한 뒤 app.module에서 임포트하는 방식이다.

이렇게 구조를 짜면 여러 파일들을 쉽게 분류해 MVC패턴을 만들 수 있어 편리해 보였다.

service-controller-module 방식은 비슷하지만 이를 폴더를 만들어 옮기고 메인 모듈에서 서브 모듈들을 한꺼번에 임포트하여 다양한 모듈들을 사용할 수 있는 실용적인 방식이라고 할 수 있다