18.02.22(목)

# 28. Ajax

서버랑 어떻게 통신을 해서 DOM을 다루냐??

화면이 바뀌는 것. 라우팅을 구현하는 것은 쉽지 않으니까 

## 1. Ajax (Asynchronous JavaScript and XML)

XML 

HTML 처럼 생겼다.  이전에 서버와 클라이언트 간에 데이터를 오갈때 기본 포맷.

<div class = "red"> Hi </div>

여기서 진짜 데이터는 Hi, div 는 메타 데이터.



서버로 부터 데이터를 받아서 어떻게 활용할 것인가?

서버와 어떤식으로 통신하는가? 통신은 늘 양방향. 왔다 갔다 해야한다. 

Ajax 말고 다른 통신방법이 있냐? 있다.

![req_res](/Users/mac/Documents/dev/TIL/req_res.png)

브라우져가 화면을 전환하는 케이스가 있다. 

1.  주소창에 URI를 입력하면 브라우져가 도메인 컴퓨터(서버)를 찾아가서 index.html을 요구한다. 요구하고 나서는 기다리지 않고 내 할일은 끝. 서버가 주면 알아채고 기존의 DOM을 지우고 새로운 DOM 받아 새롭게 그린다. 
2. 웹페이지의 링크 즉 <a> 링크를 클릭하면 화면이 전환된다.
3. 브라우저의 히스토리(뒤로가기 앞으로가기), 리로드를 누르면 



클라이언트가 서버에게 항상 html(파일)을 리퀘스트 하면 그 파일을 가지고 로드 한 후 파싱해서 랜더 트리 만들어서 랜더링 한다. 그럴 때 깜빡 하는데 이렇게 하고 싶지 않은 욕구가 생기게 된다. 플러그인의 도움을 받아서 (여러가지를 깔아서) 이런 저러한 것들을 구현하려고 했지만 매우 불편. 보안도 약해진다. 결국 W3C가 웹의 생태계를 고민해서 만들어낸 것이 HTML5이다. 잡스가 flash를 지원하지 않을꺼라고 선언하니까 소니처럼 뻘짓한다고 욕함. 결국은 flash가 점점 배제되기 시작했다. 왜 그랬을까? flash의 대안이 있어야 하는데 뭐가 있을까? 그것이 바로 Javascript! 지금은 flash 개발자가 거의 멸종되었음. 

새로운 Ajax라는 기술을 처음 알아본 것이 구글. Ajax가 돌아가기에는 엔진이 약하니까 구글이 만든 것이 A8.

그걸 시현하는 것이 Gmail, Google Maps.

결국 깜빡거리는 것은 uri가 바뀌기 때문인데 이를 막기 위해서는 바꾸지 말아야 한다.

부작용? 검색이 안된다. SEO(Search Engine Optimizing)

![traditional-webpage-lifecycle](/Users/mac/Documents/dev/TIL/traditional-webpage-lifecycle.png)

단방향 통신이 문제다. 무전기하고 유사하다. 내가 할 말을 하고 끊지 않으면 상대방이 통신을 못한다. 

전화가 양방향 통신. 서로 함께 얘기할 수 있다.

단방향 통신의 문제는 request 가 response를 모른다. 서버와 통신한 이력을 어딘가에 저장해야 하는데 그것이 바로 쿠키. 그 다음이 세션. 그 다음이 토큰.

여기서 받는 html은 완전한 html. 페이지 전체를 그릴 수 있어야 하니까. 

![ajax-webpage-lifecycle](/Users/mac/Documents/dev/TIL/ajax-webpage-lifecycle.png)

Ajax 방식에서는 처음에 html을 한 번만 가져오고 그 다음 부터는 데이터만 가지고 오면 된다. 

만약 로그인을 하낟고 하면 서버에 요청하면 서버는 그 유저가 있는지 없는지 확인을 한 다음 있다면 그 데이터를 클라이언트에 전달한다. html은 모든 형식의 파일을 보낼 수 있는데 왜 사용하지 않을까? 서버는 한정되어 있다. 서버는 돈. 클라이언트에서 html을 만들어 내는 것이 기업 입장에서는 좋다. 돈이 안든다. 

서버에서 html을 만드는 걸 server rendering. ( SEO 가 잘된다. 즉 검색이 잘된다. 프론트엔드 개발자 코딩이 간편해진다. )

클라이언트에서 html 만드는 걸 client rendering.



## 2. JSON (JavaScript Object Notation)

''자바스크립트의 표기법을 따른다.'' 라는 뜻.

클라이언트와 서버에 데이터 교환이 필요한 데 그 데이터를 담을 데이터 포맷을 이야기 한다.  그 포맷이 자바스크립트의 Object와 거의 비슷하게 생겼다. 기본적으로 텍스트(문자열)이다.



인터넷에 데이터를 태우려면 결국 문자열 아스키 코드로 만들어 주어야 한다.

 **JSON은 순수한 텍스트로 구성된 규칙이 있는 데이터 구조이다**



```
{
  "name": "Lee",
  "gender": "male",
  "age": 20,
  "alive": true
}
```

**키는 반드시 큰따옴표(작은따옴표 사용불가)로 둘러싸야 한다.**



### 2.1 JSON.stringify

객체를 JSON 타입으로 바꿔줘야 할 때 쓰는 함수.

```
var o = {
  name: 'Lee',
  gender: 'male',
  age: 20
};

// 객체 => JSON 형식의 문자열
var strObject = JSON.stringify(o);
console.log(typeof strObject, strObject);
// string {"name":"Lee","gender":"male","age":20}

// 개행을 하면 데이터가 더 커지기 때문에 개행하지 않고 만들어준다. 

// 객체 => JSON 형식의 문자열 + prettify (조금 더 예쁘게 보여주려는 방법)
var strPrettyObject = JSON.stringify(o, null, 2); 
// null은 filtering 하는 함수 2는 space 2개
console.log(typeof strPrettyObject, strPrettyObject);
/*
string {
  "name": "Lee",
  "gender": "male",
  "age": 20
}
*/

// replacer
// 값의 타입이 Number이면 필터링되어 반환되지 않는다.
function filter(key, value) {
  return typeof value === 'number' ? undefined : value;
}

// 결국 숫자만 보내겠다는 뜻.

// 객체 => JSON 형식의 문자열 + replacer + prettify
var strFilteredObject = JSON.stringify(o, filter, 2);
console.log(typeof strFilteredObject, strFilteredObject);
/*
string {
  "name": "Lee",
  "gender": "male"
}
*/

var arr = [1, 5, 'false'];
// 배열에서도 사용할 수 있다. 

// 배열 객체 => 문자열
var strArray = JSON.stringify(arr);
console.log(typeof strArray, strArray); // string [1,5,"false"]

// replacer
// 모든 값을 대문자로 변환된 문자열을 반환한다
function replaceToUpper(key, value) {
  return value.toString().toUpperCase();
}

// 배열 객체 => 문자열 + replacer
var strFilteredArray = JSON.stringify(arr, replaceToUpper);
console.log(typeof strFilteredArray, strFilteredArray); // string "1,5,FALSE"
```



### 2.2 JSON.parse

 JSON 데이터를 가진 문자열을 객체로 변환한다. (== 역 질렬화 )

```
// JSON 형식의 문자열 => 객체
var obj = JSON.parse(strObject);
console.log(typeof obj, obj); // object { name: 'Lee', gender: 'male' }

// 문자열 => 배열 객체
var objArray = JSON.parse(strArray);
console.log(typeof objArray, objArray); // object [1, 5, "false"]
```



## 3. XMLHttpRequest

브라우저는 **XMLHttpRequest 객체**를 이용하여 Ajax 요청을 <u>생성하고 전송한다.</u>

XMLHttpRequest 객체 결국 생성자 함수다. 



XMLHttpRequest 객체를 사용해서 서버에 요청하기 위한 준비를 하고 서버에 요청을 하고 서버로부터 다시 받아준다. 



### 3.1 Ajax request

요청을 보내는 방법

```
// XMLHttpRequest 객체의 생성
var xhr = new XMLHttpRequest();

// 비동기 방식으로 Request를 오픈한다. 통신 채널을 오픈한다. 
xhr.open('GET', '/users');
// GET: 메소드, /users: url Get 방식으로 통신하고 /users로 비동기 통신한다. 

// Request를 전송한다. 
xhr.send();
```



#### 3.1.1 XMLHttpRequest.open

통신을 준비한다. 인자로 3개를 가진다. 

```
XMLHttpRequest.open(method, url[, async])
```



- method 5개 (GET, POST 등등 ) 정도면 알면 된다. 
- /url 
- 비동기식으로 동작하는 걸 원하면 false를 적어준다.



#### 3.1.2 XMLHttpRequest.send

인자로 payload 라는 걸 준다.

payload란 ? 리퀘스트 메세지

GET 방식은 보낼 때도 있고 안보낼 때도 있다. 인자가 없다는 건 다 가져온다는 것

POST방식은 내용이 있어야 한다. 반드시 페이로드가 있다. 서버는 페이로드를 가지고 데이터를 만든다.



준비된 요청을 서버에 전달한다. 

순서가 중요하다. open —> send ![HTTP_request+response_message](/Users/mac/Documents/dev/TIL/HTTP_request+response_message.gif)



request 가 어떻게 생겼을까? 첫번째 그림이 request 객체이다. 

**Request Message**

Header는 그 웹문서의 정보에 관해서만 표시된다. body를 위한 메타 데이터다. 

Host(클라이언트가 어떤 서버에 보낸다는 뜻)의 주소가 써있는데

```
xhr.open('GET', '/users'); 

// 여기서는 host가 없는데 그럼 어디로 가나?
클라이언트가 서버랑 한번 통신을 하면 즉 서버로 부터 html을 한 번 받게되면 이미 호스트(서버)를 알 수 있다. 
```



Accept: 내가 받을 타입

Content-type:  내가 보낼 타입

Content-length:  길이 

NAME-Smith&ADDRESS = Berlin:  페이로드

--------------------------------------

**Response Message**

200 ok : 통신결과, 성공적으로 통신이 완료된다는 뜻.

통신이 안되면 어떤 이유로 처리가 안됐다는 이유를 담아서 준다.  

Server: 서버의 애플리케이션 종류

Content-type: 서버가 보내는 타입



XMLHttpRequest.send 메소드에는 **request body**에 담아 전송할 인수를 전달할 수 있다.

```
req.send(null);
// req.send('string');
// req.send(new Blob()); // 파일 업로드와 같이 바이너리 컨텐트를 보내는 방법
// req.send({ form: 'data' });
// req.send(document);

// 날려보낼 자료를 인자에 담아준다. 
```



#### 3.1.3 XMLHttpRequest.setRequestHeader

인자로 종류와 타입을 줘야한다. 

```
// json으로 전송하는 경우
req.open('POST', '/users');

// 클라이언트가 서버로 전송할 데이터의 MIME-type 지정: json
req.setRequestHeader('Content-type', 'application/json');

var data = { id: 3, title: 'JavaScript', author: 'Park', price: 5000};

req.send(JSON.stringify(data));
```



### 3.2 Ajax response

클라이언트는 서버에 요청하고 바로 다른 일 한다. (비동기) 서버에 이벤트가 감지되면 

```
// XMLHttpRequest.readyState 프로퍼티가 변경(이벤트 발생)될 때마다 이벤트 핸들러를 호출한다.
req.onreadystatechange = function (e) {
  // readyStates는 XMLHttpRequest의 상태(state)를 반환
  // readyState: 4 => DONE(서버 응답 완료)
  if (req.readyState === XMLHttpRequest.DONE) {
    // status는 response 상태 코드를 반환 : 200 => 정상 응답
    if(req.status === 200) {
      console.log(req.responseText);
    } else {
      console.log("Error!");
    }
  }
};
```

XMLHttpRequest.DONE: 서버에 응답이 왔다. 

req.status === 200: 정상으로 들어왔다. 만약 200이 아니면 정상 처리가 아니다. 

if 문을 같이 쓰지 않는 이유는 정상처리만 가능하기 때문이다. 정상이 아니면 처리가 안된다. 



```
// XMLHttpRequest 객체의 생성
var req = new XMLHttpRequest();
// 비동기 방식으로 Request를 오픈한다
req.open('GET', 'data/test.json');
// Request를 전송한다
req.send();

// XMLHttpRequest.readyState 프로퍼티가 변경(이벤트 발생)될 때마다 콜백함수(이벤트 핸들러)를 호출한다.
req.onreadystatechange = function (e) {
  // 이 함수는 Response가 클라이언트에 도달하면 호출된다.
};
```

- 'data/test.json'

무슨뜻일까?

json파일을 호출한 것. 서버가 미리 만들어 놓은 정적인 데이터를 받겠다. 서버 루트의 데이터 폴더에 있는 테스트 제이슨 파일을 달라는 것.

- '/users'

이것은 동적 파일을 달라는 것.



node.js는 웹서버가 아니다. 자바스크립트가 서버가 아닌 곳에서 돌아가기 위해 만든 환경이다. 



### 5.3 Load JSONP



서버간에는 통신이 가능하기 때문에 처음 http를 요청한 서버 말고 다른 서버에 리스판스를 가지고 올 수 있다. 



# 29. REST API



## 1. REST API 중심 규칙

-  URI는 자원을 표현하는 데에 집중해아 한다. (명사를 의미. 무엇을)
- 행위에 대한 정의는 HTTP Method를 통해 하는 것 (동사를 의미. ~을 한다.)

RESTful 하다는 것은 REST 규칙을 잘 지켰다. 즉 명사와 동사를 정확히 사용하였다는 뜻. 



xhr.open('GET', '/todos')'

todos를 조회하라는 뜻.

조회에는 2가지의미가 있다. 하나는 싹 다 가지고 와라, 다른 하나는 특정한 한가지만 가지고 와라.

여기서는 싹 다 가져와라는 뜻.

xhr.open('GET', '/todos/: id ')—> 서버에 줄 데이터가 있는 상황.



POST / todos/ 10

POST는 생성하라는 뜻. 

반드시 페이로드가 있어야 한다. 뭔가를 주고서 만들라고 해야하니까. 



DELETE/ todos/ 10 

DELETE는 지우라는 뜻.

무엇을 지울지 써줘야 한다. 아니면 싹 다 지우라는 뜻. 



PUT/ todos/ 10

PUT은 무엇을 고치라는 뜻.

반드시  페이로드가 있어야 한다. 어떤걸 고칠지 알려줘야 하니까. 



## 2. HTTP Method

4가지의 Method(GET, POST, PUT, DELETE)를 사용하여 CRUD를 구현한다.

| Method | Action         | 역할                    |
| ------ | -------------- | ----------------------- |
| GET    | index/retrieve | 모든/특정 리소스를 조회 |
| POST   | create         | 리소스를 생성           |
| PUT    | update         | 리소스를 갱신           |
| DELETE | delete         | 리소스를 삭제           |

## 4. REST API의 Example





POSTMAN?

백엔드가 우리에게 REST API를 만들어져 있다고 하면 코디없으 프론트 개발자가 접근해 볼 수 있어야 한다. 백엔드가 늦어지면 페이크 데이터를 만들어야 한다. 



### 4.3 POST



POST는 기본 201번이 넘어온다. 생성에 성공했다는 뜻. 