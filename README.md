# WeTube

Cloning Youtube with Vanilla and NodeJS

## WETUBE 를 만들면서 배운 이론과 기능들 정리.

### Node.js란 무엇인가?

브라우저에 종속 되어 있고 브라우저에 맞춰진 언어였던,  Javascript를 브라우저 밖으로 가지고 나와서 유저가 사용 할 수 있게 한 것이다.

이것을 통해서 우리는 file system을 다룰수 있다. 

서버를 만들수있고, Web scrapper를 만들어서 웹페이지에 접속해서 정보들을 수집 할 수 있다.

위에 일이 가능한 이유는 Javascript가 프로그래밍 언어 이기 때문이다. 

Node.js를 쓰는 이유는 무엇일까?

	1. 프론트와 백엔드 모두를 Javascript로 만들때 
	2. 특정 라이브러리 없이 처음 부터 하나 하나 쌓아가는 식으로 작업을 수행한다. (호불호가 갈리지만 정확히 내가 무엇을 하고 있는지 인식 할 수 있다.)
	3. 내가 많은 데이터를 움직여야 할 때 사용하기 정말 좋다. 즉, 많은 데이터를 다뤄야 할때 ex) database 생성, database 삭제, 사용자에게 전송하고, 어떤 곳에 저장하고 등등 node.js는 데이터를 다루는 성능이 아주 좋다.

* macOS에서 사용하는 홈브루(Homebrew)는 자유 오픈소스 소프트웨어 패키지 관리 시스템의 하나이며, macOS 운영체제의 소프트웨어 설치를 단순하게 만들어 준다.

### ExpressJS 서버

#### What is a Server?

서버는 우리가 사용하는 인터넷이 연결 된 모든 컴퓨터를 말한다. 

물리적인 서버와 소프트웨어 적인 서버로 구분하며 온종일 온라인에 접속 된 상태이다.

서버 하나당 엄청 많은 하드 드라이브와 메모리, 보드들로 구성되어 있다.

1. 물리적인 서버의 모습 
	
    ![Server_image](img/Server_image.jpg)

2. 소프트웨어 적인 서버의 모습
    
    간단히 말하면 인터넷에 연결된 한 덩어리의 코드를 의미한다.
    
    일종의 네트워크에 연결 된 것이며, public 네트워크와 private 네트워크 두가지 모두 이며, URL에 응답하고, 접속을 허락하는 일을 한다.
    
    예를들어 네이버 사이트도 어딘가에서 Hosting 되고 있을 것이며, 그 말은 어딘가 서버가 있다는 것이다.

#### Installing Express with NPM

우리는 Express를 설치하기 전에 Node pachage Manager를 알아야한다. 

줄임말로 NPM이라고 하며, 이것은 Express, react, electron 등등의 오브젝트들을 NPM을 통해 다운로드하고 업로드하고 업데이트하며, 관리가 가능하도록 한다. 

하나의 공장에 node.js와 관련된 오브젝트들이 모여 있고 그곳에서 작업들이 이뤄진다. 

이렇게 사용하는 이유는 Express, react, electron 들이 따로 있는것 보다 관리하기 쉽고, 만약 내 프로젝트가 오픈소스라면 다른 사용자가 처음 부터 설치 및 셋팅을 하지 않아도 간단하게 NPM을 통해서 내가 작업 했던 환경을 빠르게 셋팅하고 이용하고 작업 할 수 있기 때문이다.

그럼 NPM의 설치 하는 법은 무엇일까? 사실 우리는 Node.js를 설치할때 같이 설치 되었다고 보면 된다.

설치 된 NPM을 이용해서 프로젝트를 시작해야 한다. (이유는 위에 작성한 것 처럼 다양한 사람과 공유를 하고 좀 더 쉽고 빠르게 설치 및 관리 하기 위해서)

1. npm init

	이 명령어를 통해서 우리는 첫 시작을 하며, 프로젝트 명, 버전, 어떠한 프로젝트 인지 묘사, 이 프로젝트의 주인 등등 작성을 한다.
    
    작성이 끝나면 pachage.json이라는 파일이 생성 되고, 그 안에 우리가 작성 했던 사항들이 Javascrip에서 정보를 담는 방식으로 작성되어 있는것을 확인 할 수 있다.)

    ![NPMinit](img/npminit.png)

    ![packagejson](img/packagejson.png)

   
2. 두번째로 npm install express 
    
    설치를 마치게 되면, 두 가지가 생성 되는데 그중에서 node_modules 폴더가 중요하다.
    
    설치 완료 이후 우리의 package.json에는 "dependencles" : {"express":"해당 버전명"} 이 작성 되어 있는 것을 확인 할 수 있다.
    
#### Your First Express Server 및 .gitignore에 대해서

해당 서버의 첫 걸음은

    const express = require('express'); 를 통해서 node_modales 폴더에 있는 Express를 import하고 
    const app = express(); 를 통해서 사용하면 된다. app로 사용 가능
      
    const PORT = 4000; ---> 좀 더 깔끔하게 보이기 위한 코딩 밑에 ${PORT}를 위해 사용

	function handleListening() {
  		console.log(`Listening on: http://localhost:${PORT}`);
	}
    콜백함수를 사용하는 것. 

	app.listen(PORT, handleListening); app에게 (app는 express와 같다) 4000번 포트를 listen 하게 해주고, 
    listening 하기 시작할때, handleListening 이라는 함수를 호출 해준다.
    
 이러면 localhost:40000 으로 가게 되면 서버가 실행 된 것을 알 수 있다. 그전에 서버 가동 해줘야함. 
 나는 package.json에 
 
 	"scripts": {
    "start": "node index.js"
    }
    
설정을 해주었기에 npm start만 해주면 서버가 가동 된다.


* .gitignore이란?
	
    git 저장소에 저장 될때 무시목록을 작성해서 관리 할 수 있는 것이다. 가령 중요한 키값이 저장소에 올라가지 않게 할 수 있다.

    ![gitinit](img/git1.png)

     위 이미지는 첫 프로젝트를 만들고 git 저장소를 만들때의 방식이다.

 #### Handling Routes with Express
 
 우리는 HTTP 메소드 중에 get과 post를 이용해서 서버와 라우터 핸들링을 할 것이다. 
 
 * GET Method
     
     GET 요청을 캐시할 수 있고, 브라우저 기록에 남아 있고, 예약 할 수 있으며, 중요한 데이터를 처리할 때 GET 요청을 사용해서는 안된다. 그리고 길이 제한이 있고, 마지막으로 데이터 요청에만 사용된다.
     
     예를들어 게시판의 리스트를 본다거나, 글을 본다거나, 검색을 한다거나 등등.
     
     GET은 가져오는 것(read) 정보조회.
   
 * POST Method

    GET과는 다르게 캐시되지 않고, 브라우저 기록에 남아 있지 않고, 예약 할 수 없고, 데이터 길이 제한이 없다.
    
    예를들어 게시판 작성 또는 회원가입 등등.
    
    POST는 수행하는 것(create) 새로운 정보등록.
    
![reqres](img/reqres.png)

허나 이 이미지 속 작업방식과 다르게 실제로는 완전한 html,css 파일을 send 해줘야하며, 앞으로 우리가 배울 것이다.

즉, 서버를 생성 -> route를 생성 -> 응답(res) 하는 방식.

#### ES6 on NodeJS Using Babel

##### Babel

Babel은 최신의 Javascript 코드를 아주 무난한 예전의 Javascript 코드로 변환해 준다.

babel은 여러가지 방법으로 사용 가능하며, 우리가 사용 할 방법은 babel node다.

이 변환을 써주기 위해서 3가지 설치를 해준다.

	1. npm install @babel/node
	2. npm install @babel/core
	3. npm install @babel/preset-env

그 이후 우리는 .babelrc 파일을 만들어주고 이 파일에 우리가 원하는 node.js와 js를 필요에 의해서 넣을 것이다.

즉, babel 넌 이런 preset을 가질 것이라 설정 해주는 것이다.

또한 기본 함수를 arrow function 방식으로 변환이 가능하게 된다.


##### 번외

우리는 수동으로 서버를 켜고 끄는건 별로 좋은 방법이 아니기에 nodemon 이라는 package를 설치 한다.

허나 이건 프로젝트를 위하기 보단 프로그래머를 위한 설정이기에 dependency에 포함 시키기 보단. 이 밖에 따로 설치 해주는게 좋다.

	npm install nodemon -D 
    해주면 package.json에 해당 nodemon이 설치가 된 것이 표시가 되게 된다. 
    
이 방법을 통해서 우리는 서버를 수동적으로 키고 끄는걸 안해도 되지만, 문제가 babel이 코드를 변환 하는 사이에 서버의 재시작이 더 빠르게 이뤄져서 정확히 코드를 못읽는 사태가 발생한다.

이 오류를 고치기 위해서 우리는 package.json에 

	"scripts":{"start":"nodemon --exec babel-node index.js --delay 2"}
    
    --delay 2 딜레이 2초를 해준다.
    
#### Express core: Middlewaes.

Express의 middleware란 웹사이트에 접속 이후 index.js파일을 실행하고 우리의 application이 route가 존재하는지 살펴보는데, 

그럼 우리가 작성한 코딩에서 

	app.get("/", handleHome); (/)home을 찾고, handleHome 함수를 실행 할 것이다.
    
그럼 handleHome은 응답을 해주는데, 바로 그전에 home과 함수 사이에 미들웨이가 존재하게 된다.

즉, 접속 이후 route 실행 이전에 미들웨이가 위치하게 되며, 그 미들웨어는 모든 함수들이 될 수 있다.

예를들자면 유저의 로그인을 체크하거나, 접속 되는 log들을 작성하는 미들웨어를 만들수도 있다. 

사용 방법은 밑에 이미지 처럼 사용되고, 저 위치에 미들웨어가 있다면 /home, /profile route 기능 이전에 미들웨어 먼저 동작하게 된다.

![middleware](img/middleware.png)

또한 우리는 추가적으로 middleware에 포함 된 다양한 기능들을 쓸 것인데, 그중에서도 밑에 이미지에 보이는 것 처럼 

1. morgan
2. helmet
3. body-parser
4. cookie-parser

를 사용 할 것이다.

![middleware2](img/middleware2.png)

#### Express Core: Routing

우리가 routing을 하기 전에 이해 해야할 것이 있다. 우선 프로젝트를 진행할때 다양한 방법으로 작업을 진행 하겠습니다.

대체적으로 또는 내가 이해하기론 동작들을 하나 하나 쪼개서 정리하는게 참 편리하고 좋다고 생각한다. 

지금 하는 작업들도 하나로 묶어서 코드를 작성해도 되지만, 작은 조각으로 쪼개 놓으면 수정 할때나 다양한 파일에서 모듈을 가져다 쓸때 더 기능적이고 편하다. 

예를들면 우리는 init.js를 만들기 전에 index.js 안에 두고 init.js 코드와 app 기능 등등 같이 묶어서 쓰고 있었다. 

이렇게 쓰면 한 곳에 너무 많은 코드가 길게 늘어져 있을 뿐 아니라 가독성이 너무 떨어진다. 

그래서 이미지에 보이는거 처럼 init.js를 만들어서 나두고, index.js는 app.js로 바꿔서 관련 app만 관리하게 둔다. 

또한 이렇게 관리하기 위해서 app.js에서 ES6 기능인 모듈을 이용해 init.js import 해준다. 

app.js에서 export default app; 이후 init.js에서 import app from "./app";  해준다는 것이다.

이 내용을 정리하자면 이 밑에 이미지와 같다.

![appjs](img/appjs.png)

![initjs](img/initjs.png)

![routerjs](img/routerjs.png)

다시 한번 간단히 설명하자면, 가독성 및 편의성을 위해서 프로젝트의 코드를 쪼개는게 좋은데, 이번 챕터에서 init.js를 만들고

index.js를 app.js로 바꿔준 이후 app.js에서 ES6 기능인 모듈을 이용해서 다른 파일의 object를 이용 할 수 있는데, 우리는 app.js object를 사용 할 것이다. 

그러므로 app.js에 export default app;(ES6 모듈 기능을 이용 하기 위한 코딩) 해주고, init.js에서 import해준다. 

또한 이제는 router.js를 만들어서 route들의 복잡함을 쪼개 줄 것이고 이것은 주소창을 세분화 하고 해당 주소에 작성되고 동작하게 코딩한 것들을 웹사이트에 띄어주는 역활을 한다. 

가령 /user 주소창으로 이동 했을때 나오는 유저 관련 정보가 웹사이트에 보여지면, /user/edit 으로 이동해서 유저 정보 관련을 수정 할 수도 있다. 

즉, 주소창 이름을 좀 더 직관적으로 만들고 그에 맞춰서 기능들도 한곳에 다 모아두는 것이 아니라 나눠서 세분화 시킨다고 보면 된다.