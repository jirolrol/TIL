18.03.05(월)



# 1. Node.js Basics

프론트엔드는 대체 어떤걸 하는 사람일까?

VIEW에서 상태변화가 일어난다. Input text는 사용자가 입력한다. 

서버에 알린다, 서버에 등록한다는 뜻은 서버에 리퀘스트를 한다는 뜻. 

리퀘스트를 받은 서버가 어떤 일을 할텐데 어떤걸 할까? 

매번 상태를 자동적으로 감지해서 view에 뿌려준다면 좋지 않을까??  ---> 이러한 기능이 있다. 이것을 변화감지라고 한다.  

모던한 Library, Framework을 이용하여 변화감지를 쉽게 할 수 있다.



그럼 백엔드는 어떤 일을 할까?

**요청을 받으면** 내가 이것을 해버려야지! 라고 일을 시작한다.

1. 정적 파일의 제공.

2. REST API를 처리. 

3. DATA BASE : 프론트엔드와 백엔드의 가장 큰 차이.

   Java/Spring(Framework), PHP 언어는 다양하지만 어떤 언어로 만들든 프론트에서는 상관이 없다. 



Node.js는 빨리 쉽게 만들 수 있다. 

서버는 안정성 있어야 한다. 24시간 절대 뻗으면 안되고 돌아가야 한다.

속도가 중요하다. (performence)

Node.js에 적합한 애플리케이션만 사용하는 것이 좋다. 

## 1. Introduction

Node.js는 서버가 아니다. 

Node.js는 [Chrome V8 JavaScript 엔진](https://developers.google.com/v8/)으로 빌드된 JavaScript [런타임 환경(Runtime Environment)](https://ko.wikipedia.org/wiki/%EB%9F%B0%ED%83%80%EC%9E%84)이다. 

웹 브라우저에서 돌아가지 않는다. 

Node.js는 백엔드에서 사용하는 것보다 간단한 토이프로젝트에 사용하는 것이 좋다. 



현재 Node.js를 사용하는 기업은 Microsoft, Paypal, eBay, Yahoo, GoDaddy 등이 있다.

하지만 오해하지 말아야 할 것이 여러개의 서버중 한 두개를 Node.js를 사용하고 있다는 뜻.



프론트엔드 개발자도 백엔드와 겹치는 부분에 있어서는 매우 잘 알고 있어야 한다. 깊은 이해까지는 필요 없지만!



Node.js는 **Non-blocking I/O와 단일 스레드 이벤트 루프**를 통한 높은 Request 처리 성능을 가지고 있다.

-  **Non-blocking I/O**: 비동기 처리를 한다. 
- 기본적으로 하나의 처리가 무거운 애플리케이션은 Node.js가 좋지 않다.  (SNS, KAKAOTALK에 적합하다.)



버전업 할 때 애매하다. 기존 버전을 지우고 다른 버전을 깔아야 한다. 

혹은 여러가지 버전을 사용해야 할 때. A 프로젝트는 8버전  B 프로젝트는 9 버전 이런식으로 사용해야 할 때는 



REPL(Read Eval Print Loop: 입력 수행 출력 반복)은 Node.js는 물론 대부분의 언어(Java, Python 등)이 제공하는 가상환경으로 간단한 코드를 직접 실행해 결과를 확인해 볼 수 있다. 



## 5. Node.js 맛보기 : HTTP Server

노드를 사용해서 파일을 열어볼 수 있다. 



```
// app.js
const http = require('http'); // 1
// require 가 node.js의 모듈
   'http'라는 모듈을 http에 담았다. 클라이언트와 서버간의 여러가시 통신을 담고있는 객체일 것이다. 
   동기방식이다. 왜 비동기로 안했을까? 구지 비동기로 할 필요가 없다. http가 없으면  이 이후에 처리는 되지 않기  	 때문에.

http.createServer((request, response) => { // 2
  response.statusCode = 200;
  response.setHeader('Content-Type', 'text/plain');
  response.end('Hello World');
}).listen(3000); // 3

console.log('Server running at http://127.0.0.1:3000/');

```

request, response 객체를 늘 필요하고 늘 담는다. createServer가 만들어 준다. 

response.statusCode = 200;

--->서버가 클라이언트에게 response를 할 때 늘 코드가 있어야 한다. 

response.setHeader('Content-Type', 'text/plain');

---> respose 메세지의 헤더를 세팅하는 것.

response.end('Hello World');

---> end라는 메소드를 호출하면서 respose 메세지를 만들어서 클라이언트로 센드한다. 

listen(3000)

—> 3000번 포트를 쓰겠다. 



라우터의 역할이 없다. 거기에 대한 구별은 없고 모든 요청에 대해서 무조건 성공했다고 200번 셋하고 성공했다고 메세지를 보낸다는 것.



결국 Node.js를 배운다는 것은 이 안의 메소드와 객체들을 배운다는 것이다. 



# 2. Node.js & **npm**

npm 

결국 모듈화에 대한 이야기를 알아야 한다. 

모듈화란 파일단위로 스코프를 갖게 하는 것이다. 

모듈화란 내가 필요한 것들만 공개할 수 있어야 하고 그것을 import할 수 있어야 한다. 

## 1. 모듈화와 CommonJS





## 2. npm

 [npm(node package manager)](https://www.npmjs.com/)은 자바스크립트 패키지 매니저이다.

짝퉁들이 있다. 사이트에서 꼭 검색! 악성 코드가 숨겨져 있을 수도 있다. 

혹은 안돌아가는 것도 있다. 

사내에서 개발한 모듈을 사내에서만 쓰고 싶을 떄는 돈 내고 사용.



### 2.1 패키지 설치

package.json 을 회사에서 주면 프로젝트 폴더 밑에 가져다 두고 npm install 하면 된다. 



패키지를 설치할 때에는 `npm install` 명령어 뒤에 설치할 패키지 이름을 지정한다.

```
$ npm install <package>
```



### 2.2 지역(local) 설치와 전역(global) 설치

npm install 명령어에는 지역(local) 설치와 전역(global) 설치 옵션이 존재한다.

옵션을 별도로 지정하지 않으면 지역으로 설치되며 프로젝트 루트 디렉터리에 `node_modules` 디렉터리가 자동 생성되고 그 내부에 패키지가 설치된다. 지역으로 설치된 패키지는 해당 프로젝트 내에서만 사용할 수 있다.



### 2.3 package.json과 의존성(dependency) 관리

package.json 을 깔고 install을 하는 것이 좋다. 많은 패키지들을 사용하게 되었을 때 필요하다. 

```
$ npm init -y
Wrote to /Users/leeungmo/Desktop/emoji/package.json:

{
  "name": "emoji",
  "version": "1.0.0",
  // name 과 version은 생략할 수 없다. 폴더명을 기준으로 name이 만들어진다. name은 결국 프로젝트 이름.
  "description": "",
  // 프로젝트에 관한 설명을 써주는 곳.
  "main": "index.js",
  // 진입점을 말한다. 맨 처음으로 실행되는 파일을 말함. 생략 가능.
  "dependencies": {
    "node-emoji": "^1.8.1"
  // 버전을 지정안하면 최신 버전이 깔린다. 1.8.1이 아니라 1.0.0을 깔고 싶으면 @1.0.0 이라고 쓴다. 	
  },
  "devDependencies": {},
  // 개발 할때만 필요한 의존성들을 깐다. 
  	--save-dev 를 이곳으로 들어간다. 이 옵션 안주면 위에 dependencies로 들어간다. 
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  // shell 스크립트를 나열해주면 된다.
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

### 2.4 Semantic versioning(유의적 버전)

npm install 명령어의 패키명 뒤에 @버전을 추가하면 패키지 버전을 지정하여 설치할 수 있다.

```
$ npm install node-emoji@1.5.0

...
  "dependencies": {
    "node-emoji": "^1.5.0"
  },
...
```

"^1.5.0" 

^(캐럿)가 무엇인가? 

나중에 업그레이드가 되었을 떄 알아서 버전 업이 된다.

캐럿을 지우면 1.5.0으로만 깐다. 

![sementic-versioning](/Users/mac/Documents/dev/TIL/sementic-versioning.png)



메이저 버전이 올라가면 호환사이 보장되진 않는다. 

마이너 버전이 올라가면 호환성이 보장된다.

패치 버전이 올라가면 호환성이 보장되고 버그가 있었던 것들이 보완된다. 

ex) ^1.7.3 이라고 기입했다고 하면,

1.9.0으로는 버전을 올리지만 2.0.0으로는 올리지 않는다. 호화성이 보장되지 않기 때문에.



# 3. Node.js **module**

## 1. Node.js 모듈

모듈은 **module.exports 또는 exports 객체**를 통해 정의하고 외부로 공개한다. 그리고 공개된 모듈은 **require 함수**를 사용한다. 



## 2. exports

```
// circle.js
const { PI } = Math;
// 외부에 공개하지 않겠다는 뜻. 즉 exports하지 않겠다. 
exports.area = (r) => PI * r * r;
// 객체, 메소드명 

exports.circumference = (r) => 2 * PI * r;
```



```
// app.js
const circle = require('./circle.js'); // == require('./circle')
// 우리가 만든 모듈이기 때문에 경로를 꼭 기입해줘야 한다. circle에는 exports 객체 자체가 들어온다. 

console.log(`지름이 4인 원의 면적: ${circle.area(4)}`);
console.log(`지름이 4인 원의 둘레: ${circle.circumference(4)}`);
```



## 3. module.exports

```
// circle.js
const { PI } = Math;

module.exports = function (r) {
// 여기서 r은 자유변수/
  return {
    area() { return PI * r * r; },
    circumference() { return 2 * PI * r}
  };
```

| 구분           | 모듈 정의 방식                                               | require 함수의 호출 결과                                     |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| exports        | **exports 객체에는 값을 할당할 수 없고 공개할 대상을 exports 객체에 프로퍼티 또는 메소드로 추가한다.** | exports 객체에 추가한 프로퍼티와 메소드가 담긴 객체가 전달된다. |
| module.exports | **module.exports 객체에 하나의 값(기본자료형, 함수, 객체)만을 할당한다.** | module.exports 객체에 할당한 값이 전달된다.                  |

## 5. 코어 모듈과 파일 모듈

Node.js는 기본으로 포함하고 있는 모듈이 있다. 이를 코어 모듈이라 한다. 코어 모듈을 로딩할 때에는 패스를 명시하지 않아도 무방하다.

```
const http = require('http');
http는 빌트인 모듈
```

기본적인 맥락만 잡고 나머지는 찾으면서 공부한다. 



Node.js 도 서버를 만들 때 Framework를 사용한다. 대표적인 것이 Express.



todolist V3는 서버를 만들어야 하는데.

mongodb (데이터 베이스 접근)



# 1. Express **Basics**

여러가지 서버를 만드는 방법이 있는데 조금 애매하다. 폴더 구조를 어떻게 가져갈까? 라는 것을 우리가 결정해야 하는데 이것이 애매모호하다. Node.js가 없으면 Express는 돌아가지 않는다. 

가파른 버전업이 진행되다가 이제는 안정화 상태. 

## 1. Install



## 2. Hello world example

```
const express = require('express');
// 우리가 install한 express를 부르는 것.
const app = express();
// 불러서 객체생성해서 변수에 담아서 사용해라.

app.get('/', (req, res) => res.send('Hello World!'));
// app (express 객체). 루트로 온 리퀘스트의 리스판스를 이렇게 해라.
   res, req 이름은 뭐든 상관 없지만 순서는 정해져있다. 
   
app.listen(3000, () => console.log('Example app listening on port 3000!'));
//  3000번 서버를 실행하면서 실행해야 하는 일들을 써준다. 부팅 되었는지 확인하기 위해서 cons
```

하지만 이 상황에서는 정적 파일을 제공 못한다. 기본 뼈대만 가지고 있는 상황이다. 우리가 필요한 것을 계속 설정해 나가야 한다.

## 3. Routing

![define-route](/Users/mac/Documents/dev/TIL/define-route.png)



### 3.2 Route path

```
// localhost:3000/user/<userId>/item/<itemId>
app.get('/user/:userId/item/:itemId', (req, res) => {
  const { userId, itemId } = req.params;
  res.send(`userId: ${userId}, itemId: ${itemId}`);
});
```

**params**



### 3.4 Response method

| 메소드                                                       | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [res.download()](http://expressjs.com/ko/4x/api.html#res.download) | 다운로드될 파일을 전송한다.                                  |
| [res.end()](http://expressjs.com/ko/4x/api.html#res.end)     | 응답 프로세스를 종료한다.                                    |
| [res.json()](http://expressjs.com/ko/4x/api.html#res.json)   | JSON 응답을 전송한다.                                        |
| [res.jsonp()](http://expressjs.com/ko/4x/api.html#res.jsonp) | JSONP 지원을 통해 JSON 응답을 전송한다.                      |
| [res.redirect()](http://expressjs.com/ko/4x/api.html#res.redirect) | 요청 경로를 재지정한다. 다른 라우터로 redirect 하는 것.      |
| [res.render()](http://expressjs.com/ko/4x/api.html#res.render) | view template을 렌더링한다.                                  |
| [res.send()](http://expressjs.com/ko/4x/api.html#res.send)   | 다양한 유형의 응답을 전송한다.                               |
| [res.sendFile()](http://expressjs.com/ko/4x/api.html#res.sendFile) | 파일을 옥텟 스트림(이메일이나 http에서 사용되는 content-type에서 application의 형식이 지정되어 있지 않은 경우에 octet-stream이라고 한다)의 형태로 전송한다. |
| [res.sendStatus()](http://expressjs.com/ko/4x/api.html#res.sendStatus) | 응답 상태 코드(response status code)를 설정한 후 해당 코드를 문자열로 표현한 내용을 응답 본문으로서 전송한다. |

## 4. Middleware

```
const express = require('express');

const bodyParser = require('body-parser');
const cookieParser = require('cookie-parser');

const app = express();

// parse application/json
app.use(bodyParser.json());
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }));
app.use(cookieParser());
```

 **next()** 를 호출하여 그 다음 미들웨어 함수에 제어를 전달해야 한다.



## 6. Template engine

서버가 html을 만들어서 주는 경우도 있다.

 [handlebars](http://handlebarsjs.com/), [pug](https://pugjs.org/api/getting-started.html), [ejs](http://ejs.co/) 이것 모두 클라이언트에서 만들때 사용하는 것이었지만 ES6가 오면서 잘 사용하지 않는다.