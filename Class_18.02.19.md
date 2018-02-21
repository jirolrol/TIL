18.02.19(월)



현업에서는 이벤트 핸들러를 만들 일이 많다.

순수한 자바스크립트로 만들려면 굉장히 까다로운 것이 많다. (바닐라) 

바닐라를 배우고 라이브러리를 배워야 한다. 

jquery 는 현 상황에서 많이 안쓰려는 경향이 있다. jquery DOM 에 종속되어 버린다. HTML 은 자꾸 바뀌기 때문에...HTML이 바뀌어도 javascript  구조가 바뀌지 않는 방법을 택해야 한다. 



DOM은 설계가 매우 안좋고 불편하다. 실무에 나가면 DOM API를 쓸 일이 거의 없다. 하지만 기본이기 때문에 배우긴 배워야 함.  



# 24. DOM

## 1. DOM (Document Object Model)



여기서 문서(Document)가 뭘까요? 

웹 페이지상에서의 문서. 결국 **HTML & CSS & Javascript** 

문서가 텍스트파일로 만드는 것 (.html) 확장자만 이럴 뿐 결국은 문자열 파일. 그 파일을 브라우져에게 읽히게 해서 브러우져에 표시하기 위한 것. 로드에서 파싱해서 그 결과물을 변수에 Object type 으로 넣어놓아야 한다. 그 파일을 위에서 부터 아래로 읽으면서 랜더링 한다. 



여기서 모델(Model)이 뭘까요?

데이터와 관련이 있다. 그 모델을 가지고 HTML 을 만든다. 데이터 베이스에서의 형식, 애플리케이션에 전달될 때에 형식(JASON), 애플리케이션으로 넘어왔을 때의 형식은 모두 다르다.   

form 으로 받은 데이터를 기본적으로 객체로 묶어서 관리해야한다. 대표적인게 DOM.



 Load HTML: 주소창에 주소를 치고 엔터키를 치면 HTML을 로드하는 것. 이 주소값에 해당하는 것을 달라고 요청. 그럼  Response해서 주면 그것을 객체화해야하는데 파싱부터 시작한다.  

CSS는 HTML 없이는 존재의 의미가 없으므로 합쳐져서 Render tree 를 만든다.  

Syntax tree는 합쳐지는게 중요한게 아니라 DOM tree, CSSOM tree를 제어하는게 중요하다. 

이 그림이 머릿속에 있어야 한다. 밑에 있는 tree 그림까지도! (면접단골질문)

DOM은 W3C의 공식 표준인데 따로 관리. 어떤 프로그램으로도 관리 할 수 있게 되어있다. 

**HTML** 문서에 대한 모델 구성 : 로드 파싱하는 것

## 2. DOM tree

객체에 관한 분류 배웠을 때, document

DOM 에 접근하려면 document 를 통해야한다. document의 부모는 window.

document는 DOM에 접근하기 위한 진입점이다. 

하나하나의 객체가 노드라고 부른다. (가지)

요소가 되려면 태그(여는 태그, 닫는 태크)가 있어야 한다.

요소 노드와 attribute(id, class)노드 가 항상 링크로 연결되어 있어야 한다. 둘은 형제 관계다. 

모든 요소의 종점에는 text를 가지게 된다. 

예를 들어 li 요소에 접근하고 싶을 때 ,

li 모든 요소? 아님 그 중에 첫번째?

## 3. DOM Query / Traversing (요소에의 접근)

### 3.1 하나의 요소 노드 선택(DOM Query)

Query = 질의, 선택  : 한가지를 찝어서 찾는 것.  

Traversing = 탐색:  한가지를 선택한 다음 그것을 기준으로 찾아가는 것 



-  document.getElementById(id)

```
// id로 하나의 요소를 선택한다. 어디다 담아두어야 하기 때문에 변수를 선언해준다. 
var elem = document.getElementById('one');
// 클래스 어트리뷰트의 값을 변경한다. Name을 왜 붙였을까? 
elem.className = 'blue';
```



- document.querySelector(cssSelector)

  css 문법을 그대로 써줄 수 있다. IE8	이상에서 동작한다.  첫번째 요소만 반환한다.

```
// CSS 셀렉터를 이용해 요소를 선택한다
var elem = document.querySelector('li.red');
// 클래스 어트리뷰트의 값을 변경한다.
elem.className = 'blue';
```



-  document.querySelectorAll(css)

  Return: NodeList (non-live) —> 유사배열로 도출해준다. 

  non-live?

```
// Nodelist를 반환한다.
var elems = document.querySelectorAll('li.red');

for (var i = 0; i < elems.length; i++) {
  elems[i].className = 'blue';
}
```



- document.getElementsByClassName(class)

  Return: HTMLCollection (live)

  live?

  length 프로퍼티를 가지고 있다는 것은 for문 돌리라는 뜻.

  live이기 때문에 싹 다 blue로 바뀌지 않는다. 속성들이 바뀌면 바뀐 것을 순간 캐치에서 객체의 내용을 바꾼다. length가 줄어든다. 

```
// HTMLCollection을 반환한다.
var elems = document.getElementsByClassName('red');

for (var i = 0; i < elems.length; i++) {
  // 클래스 어트리뷰트의 값을 변경한다.
  elems[i].className = 'blue';
}
```



해결방법 (참고로 알아둘 것)

1. 반복문을 역방향으로 돌린다.

```
var elems = document.getElementsByClassName('red');
for (var i = elems.length - 1; i >= 0; i--) {
  elems[i].className = 'blue';
}
```

2. while 반복문을 사용한다. 이때 elems에 요소가 남아 있지 않을 때까지 무한반복하기 위해 index는 0으로 고정시킨다.
3. HTMLCollection을 배열로 변경한다.

```
var elems = document.getElementsByClassName('red');

// ** 유사배열을 배열로 변환 **
var arr = [].slice.call(elems);

console.log(arr);
// [li#one.red, li#two.red, li#three.red]
// 각 요소는 HTMLLIElement

for (var i = 0; arr.length > 0; i++) {
  arr[i].className = 'blue';
}
```



- document.getElementsByTagName(tagName)



### 3.3 DOM Traversing (탐색)

- parentNode

```
var elem = document.querySelector('#two');
// var elem = document.getElementById('two');

var parentNode = elem.parentNode;
parentNode.className = 'blue';
```

퍼포먼스 측면에서는 좋지 않다. 그냥 한 번에 선택하는 방법이 가장 옳다. 



- firstChild, lastChild

  첫째와 막내만 찾을 수 있음. 

```
var elem = document.querySelector('ul');
// var elem = document.getElementsByTagName('ul')[0];

// first Child
elem.firstChild.className = 'blue';
// last Child
elem.lastChild.className = 'blue';
```

위 예제를 실행해 보면 예상대로 동작하지 않는다. 그 이유는 IE를 제외한 대부분의 브라우저들은 요소 사이의 공백 또는 줄바꿈 문자를 텍스트 노드로 취급하기 때문이다. 이것을 회피하기 위해서는 아래와 같이 HTML의 공백을 제거하거나 [jQuery: .prev()](https://api.jquery.com/prev/)와 [jQuery: .next()](https://api.jquery.com/next/)를 사용한다.

```
<ul><li
  id='one' class='red'>Seoul</li><li
  id='two' class='red'>London</li><li
  id='three' class='red'>Newyork</li><li
  id='four'>Tokyo</li></ul>
```



- hasChildNodes()

  자식 노드가 있는지 확인하고 Boolean 값을 반환한다.



-  childNodes

```
var elem = document.querySelector('ul');
console.log(elem); // ul

if (elem.hasChildNodes()) {
  console.log(elem.childNodes);
  // HTML의 공백을 제거하지 않은 경우
  // NodeList(9) [text, li#one.red, text, li#two.red, text, li#three.red, text, li#four, text]
  // HTML의 공백을 제거한 경우
  // NodeList(4) [li#one.red, li#two.red, li#three.red, li#four]

  elem.childNodes[1].className = 'blue';
}
```



- previousSibling, nextSibling

  형제 노드를 탐색.  우아하지 않은 방법.



## 4. DOM Manipulation (조작)

### 4.1 텍스트 노드에의 접근/수정



 텍스트 노드에 접근하려면 아래와 같은 수순이 필요하다.

1. 해당 텍스트 노드의 부모 노드를 선택한다. 텍스트 노드는 요소 노드의 자식이다.

2. firstChild 프로퍼티를 사용하여 텍스트 노드를 탐색한다.

3. 텍스트 노드의 유일한 프로퍼티(`nodeValue`)를 이용하여 텍스트를 취득한다.

4. `nodeValue`를 이용하여 텍스트를 수정한다.

   ​

- nodeValue

```
var one = document.getElementById('one');
console.dir(one); // HTMLLIElement: li#one.red

// nodeName, nodeType을 통해 노드의 정보를 취득할 수 있다.
console.log(one.nodeName); // LI
console.log(one.nodeType); // 1: Element node

// firstChild 프로퍼티를 사용하여 텍스트 노드를 탐색한다.
var textNode = one.firstChild;

// nodeName, nodeType을 통해 노드의 정보를 취득할 수 있다.
console.log(textNode.nodeName); // #text
console.log(textNode.nodeType); // 3: Text node

// nodeValue 프로퍼티를 사용하여 노드의 값을 취득한다.
console.log(textNode.nodeValue); // Seoul

// nodeValue 프로퍼티를 이용하여 텍스트를 수정한다.
textNode.nodeValue = 'Pusan';
```



### 4.2 어트리뷰트 노드에의 접근/수정

- className

  class 어트리뷰트의 값을 취득 또는 변경한다. className 프로퍼티에 값을 할당하는 경우, class 어트리뷰트가 존재하지 않으면 class 어트리뷰트를 생성하고 지정된 값을 설정한다. class 어트리뷰트의 값이 여러개일 경우, 공백으로 구분된 문자열이 반환되므로 <u>String 메소드 `split(' ')`를 사용하여 배열로 변경하여 사용한다.</u>

```
var elems = document.querySelectorAll('li');

for (var i = 0; i < elems.length; i++) {
  // class 어트리뷰트의 값을 취득하여 확인
  if (elems[i].className === 'red') {
    // class 어트리뷰트의 값을 변경한다.
    elems[i].className = 'blue';
  }
}
```

- id 

  id 어트리뷰트의 값을 취득 또는 변경한다. id 프로퍼티에 값을 할당하는 경우, id 어트리뷰트가 존재하지 않으면 <u>id 어트리뷰트를 생성하고 지정된 값을 설정한다.</u>

```
// h1 태그 요소 중 첫번째 요소를 취득
var heading = document.querySelector('h1');

console.dir(heading); // HTMLHeadingElement: h1
console.log(heading.firstChild.nodeValue); // Cities

// id 어트리뷰트의 값을 변경.
// id 어트리뷰트가 존재하지 않으면 id 어트리뷰트를 생성하고 지정된 값을 설정
heading.id = 'heading';
console.log(heading.id); // heading
```



 **중요** 

- hasAttribute(attribute)
- getAttribute(attribute)
- setAttribute(attribute, value)
- removeAttribute(attribute)



### 4.3 HTML 콘텐츠 조작(Manipulation)

ul을 선택해서 자식 li를 조작하는 방법이 없을까?

- textContent 

```
var ul = document.querySelector('ul');
// var ul = document.getElementsByTagName('ul')[0];

// 요소의 텍스트 취득
console.log(ul.textContent);
// IE를 제외한 대부분의 브라우저들은 요소 사이의 공백 또는 줄바꿈 문자를 텍스트 노드로 취급한다
/*
        Seoul
        London
        Newyork
        Tokyo
*/
// li에서 줄바꿈을 했기 때문에 줄바꿈이 되어서 나온다. 

var one = document.getElementById('one');

// 요소의 텍스트 취득
console.log(one.textContent); // Seoul

// 요소의 텍스트 변경
one.textContent += ', Korea';

console.log(one.textContent); // Seoul, Korea

// 요소의 마크업이 포함된 콘텐츠 변경.(태그가 달린 문자열)
one.textContent = '<h1>Heading</h1>';

// 마크업이 문자열로 표시된다. 태그로 인식하지 않고 문자열로 인식되어 반영된다. 
console.log(one.textContent); // <h1>Heading</h1>
```

- innerText 

  비표준이므로 사용하지 마시오.

- innerHTML

```
var ul = document.querySelector('ul');

// innerHTML 프로퍼티는 모든 자식 요소를 포함하는 모든 콘텐츠를 하나의 문자열로 취득할 수 있다. 이 문자열은 마크업을 포함한다.
console.log(ul.innerHTML);
// IE를 제외한 대부분의 브라우저들은 요소 사이의 공백 또는 줄바꿈 문자를 텍스트 노드로 취급한다
/*
        <li id="one" class="red">Seoul</li>
        <li id="two" class="red">London</li>
        <li id="three" class="red">Newyork</li>
        <li id="four">Tokyo</li>
*/
```

```
// 크로스 스크립팅 공격 사례

// 스크립트 태그를 추가하여 자바스크립트가 실행되도록 한다.
// HTML5에서 innerHTML로 삽입된 <script> 코드는 실행되지 않는다.
// 크롬, 파이어폭스 등의 브라우저나 최신 브라우저 환경에서는 작동하지 않을 수도 있다.
elem.innerHTML = '<script>alert("XSS!")</script>';

// 에러 이벤트를 발생시켜 스크립트가 실행되도록 한다.
// 크롬에서도 실행된다!
elem.innerHTML = '<img src="#" onerror="alert(\'XSS\')">';
```

untrust data	 

보안에 유의해야 한다. 



### 4.4 DOM 조작 방식

createElement(tagName)





```
// 태그이름을 인자로 전달하여 요소를 생성
var newElem = document.createElement('li');
// var newElem = document.createElement('<li>test</li>');
// Uncaught DOMException: Failed to execute 'createElement' on 'Document': The tag name provided ('<li>test</li>') is not a valid name.

// 텍스트 노드를 생성
var newText = document.createTextNode('Beijing');

// 텍스트 노드를 newElem 자식으로 DOM 트리에 추가
newElem.appendChild(newText);

var container = document.querySelector('ul');

// newElem을 container의 자식으로 DOM 트리에 추가
container.appendChild(newElem);

var removeElem = document.getElementById('one');

// container의 자식인 removeElem 요소를 DOM 트리에 제거한다.
container.removeChild(removeElem);
```

한개 바꾸는건 가능하지만 여러개를 바꿀때는 효율적이지 않다. 

### 4.5 insertAdjacentHTML()

정확한 위치를 지정해 주어야 한다. 

```
var one = document.getElementById('one');

// 마크업이 포함된 요소 추가
one.insertAdjacentHTML('beforeend', '<em class="blue">, Korea</em>');
```



### 4.6 innerHTML vs. DOM 조작 방식 vs. insertAdjacentHTML()

이것들을 비교해보자. 어떤 것을 사용해야 하나?

그냥 innerHTML 을 쓰지만 찜찜한 마음을 가지고 있어야 한다. 



## 5. style

style 프로퍼티를 사용하면 inline 스타일 선언을 생성한다.  

inline요소는 우선순위가 최고순위.

```
var four = document.getElementById('four');

// inline 스타일 선언을 생성
four.style.color = 'blue';

// font-size와 같이 '-'으로 구분되는 프로퍼티는 카멜케이스로 변환하여 사용한다.
four.style.fontSize = '2em';

원래 css 프로퍼티는 캐밥 케이스. css 프로퍼티는 카멜 케이스로 사용하는 것을 사용한다. 
```

```
 function getStyle(elem, prop) {
      return window.getComputedStyle(elem, null).getPropertyValue(prop);
    }
```

두번째 요소에 null 을 주면 모든 css 스타일 요소를 가져다 주고 이어서 .getPropertyValue(css속성)을 주면 원하는 속성값을 가져다 준다. 



# 25. Asynchronous processing model

지금까지 우리가 배운 것은 동기식. 동기식이란 순서가 보장된다. 커피가 나오기 전 까지 딴짓을 못한다. 브라우져에서 얘기하면 멈춘 것 처럼 보인다. 대표적인 것이 alert 함수. 

비동기식이란 순서가 보장되지 않는다. 



웹애플리케이션의 웹인것 처럼 보이면 안된다. 

SPA (Single Page Application): Angular에서 배우게 된다. 

애플리케이션에 필요한 모든 리소스를 한 번에 가지고 온다. (css, Javascript, img etc...)

---> 이런 것이 가능하려면 동기식이면 안된다. 

'브라우져는 싱글 스레드이고 이벤트 드리븐 방식으로 동작한다.'

이 말은 멀티 스레드를 지원하지 않는다. 한 번에 하나 밖에 못한다. 이렇게 되면 중간에 툭툭 끊어져 보인다. 따라서 비동기 방식을 도입한다. 카페로 치면 진동벨을 가지고 커피가 완성될 때 까지 내 일을 한다. 

이후에 배우는 Event의 대부분도 비동기식으로 동작한다. 

```
// 동기식

function func1() {
  console.log('func1');
  func2();
}

function func2() {
  console.log('func2');
  func3();
}

function func3() {
  console.log('func3');
}

func1();
```

```
// 비동기식

function func1() {
  console.log('func1');
  func2();
}

function func2() {
  setTimeout(function() {
    console.log('func2');
  }, 0);

  func3();
}

function func3() {
  console.log('func3');
}

func1();
```



자바스크립트의 대부분의 DOM 이벤트와 Timer 함수(setTimeout, setInterval), Ajax 요청은 비동기적으로 동작한다.

비동기식으로 처리하려면 코딩이 난해해진다. 따라서 Javascript가 일급객체를 지원하게 되었다. 

함수가 값처럼 사용되는 것이 일급 객체다. 

함수 func1이 호출되면 함수 func1은 Call Stack에 쌓인다. 그리고 함수 func1은 함수 func2을 호출하므로 함수 func2가 Call Stack에 쌓이고 setTimeout가 호출된다. **setTimeout의 콜백함수는 즉시 실행되지 않고 지정 대기 시간만큼 기다리다가 “tick” 이벤트가 발생하면 이벤트 큐로 이동한 후 Call Stack이 비어졌을 때 Call Stack으로 이동되어 실행된다.**

(call stack 이 실행 컨텍스트라고 생각하면 된다.)

**이벤트 루프**(시험문제)



Array forEach callback function 

```
var total = 0;
var testArray = [1, 3, 5, 7, 9];

// forEach 메소드는 원본 배열을 변경하지 않는다.
testArray.forEach(function (item, index, array) {
  console.log('[' + index + '] = ' + item);
  total += item;
});

//
[0] = 1
[1] = 3
[2] = 5
[3] = 7
[4] = 9

console.log(total); // 25
console.log(testArray); // [ 1, 3, 5, 7, 9 ]
```

콜백 함수는 인자로 2갸를 받는데 첫번째 인자는 함수여야 한다. 

array 를 순회하면서 시키는데 결국 순회시키는 함수가 forEach 함수다. 



# 26. Event

이벤트가 발생하면 브라우져가 감지하고 우리는 브라우져가 이벤트를 감지했을 때 뭘 해야하는지 알려줘야 한다. 

```
function func1() {
  console.log('func1');
  func2();
}

function func2() {
  // <button id="foo">foo</button>
  var elem = document.getElementById('foo');

  elem.addEventListener('click', function () {
    this.style.backgroundColor = 'indigo';
    console.log('func2');
  });

  func3();
}

function func3() {
  console.log('func3');
}

func1();
```

첫번째 인자로 이벤트를 받는다. 브라우저가 click 이벤트를 감지하면 addEventListener에게 알려주고 그럼 함수

function () {
​    this.style.backgroundColor = 'indigo';
​    console.log('func2');
  }

를 호출한다. 

이벤트 큐에 실행될 이벤트가 있는지 콜스택이 비워졌는지 감시하는게 이벤트 루프라고 한다. 



## 3. 이벤트의 종류

볼드체로 쓴 것은 외워둘 것!



### 3.1 UI Event (대부분 브라우져에 관련된 것)

| Event    | Description                                                  |
| -------- | ------------------------------------------------------------ |
| **load** | 웹페이지의 로드가 완료되었을 때                              |
| unload   | 웹페이지가 언로드될 때(주로 새로운 페이지를 요청한 경우)     |
| error    | 브라우저가 자바스크립트 오류를 만났거나 요청한 자원이 존재하지 않는 경우 |
| resize   | 브라우저 창의 크기를 조절했을 때                             |
| scroll   | 사용자가 페이지를 위아래로 스크롤할 때 (스크롤을 내렸을 때 헤더를 줄이거나 할 때 ) |
| select   | 텍스트를 선택했을 때                                         |

### 3.2 Keyboard Event

| Event     | Description            |
| --------- | ---------------------- |
| keydown   | 키를 누르고 있을 때    |
| **keyup** | 누르고 있던 키를 뗄 때 |
| keypress  | 키를 누르고 뗏을 때    |

### 3.3 Mouse Event

| Event     | Description                                                  |
| --------- | ------------------------------------------------------------ |
| **click** | 마우스 버튼을 클릭했을 때                                    |
| dbclick   | 마우스 버튼을 더블 클릭했을 때                               |
| mousedown | 마우스 버튼을 누르고 있을 때                                 |
| mouseup   | 누르고 있던 마우스 버튼을 뗄 때                              |
| mousemove | 마우스를 움직일 때 (터치스크린에서 동작하지 않는다)          |
| mouseover | 마우스를 요소 위로 움직였을 때 (터치스크린에서 동작하지 않는다) |
| mouseout  | 마우스를 요소 밖으로 움직였을 때 (터치스크린에서 동작하지 않는다) |

### 3.4 Focus Event

| Event              | Description               |
| ------------------ | ------------------------- |
| **focus**/focusin  | 요소가 포커스를 얻었을 때 |
| **blur**/foucusout | 요소가 포커스를 잃었을 때 |

### 3.5 Form Event

| Event      | Description                                                 |
| ---------- | ----------------------------------------------------------- |
| **input**  | input 또는 textarea 요소의 값이 변경되었을 때               |
|            | contenteditable 어트리뷰트를 가진 요소의 값이 변경되었을 때 |
| **change** | select box, checkbox, radio button의 상태가 변경되었을 때   |
| submit     | form을 submit할 때 (버튼 또는 키)                           |
| reset      | reset 버튼을 클릭할 때 (최근에는 사용 안함)                 |

- contenteditable: div 요소 안에 쓰면 글씨를 쓸 수 있다. 

### 3.6 Clipboard Event

| Event | Description            |
| ----- | ---------------------- |
| cut   | 콘텐츠를 잘라내기할 때 |
| copy  | 콘텐츠를 복사할 때     |
| paste | 콘텐츠를 붙여넣기할 때 |

## 4. Event Binding

어떠한 요소에서 이벤트가 발생했을 때 (요소가 이벤트를 발생시킴) 바인딩 한다. 

버튼이 클릭 되었을 때 무엇을 할 것이다.

어떤 버튼이 클릭 되었을 때 이러한 함수를 호출해라 라고 하는 것을 바인딩이라고 한다.



### 4.1 HTML Event Handler

```
<!DOCTYPE html>
<html>
<body>
  <button onclick="myFunction()">Click me</button>
  <script>
    function myFunction() {
      alert('Button clicked!');
    }
  </script>
</body>
</html>
```

onclick(어트리뷰트) 이 되었을 떄 myFunction() 함수를 호출해라!

문제가 뭐냐?

Javascript와 HTML이 섞여있다. 관심사가 틀리다. 분리하는 것이 좋다. 

**HTML속성 값으로 Javascript 코드를 쓰고 있다.** 



### 4.2 전통적(Traditional) DOM Event Handler

Javascript 와 HTML 을 분리했는데 이번엔 어떤 문제가 있나?

- 하나의 이벤트에 두개의 메소드를 달 수 없다. 

  두번째가 실행되고 첫번째는 무시된다. 둘 다 실행시킬 수 없다.

- 콜백함수에 매개변수를 줄 수 없다. 호출문을 쓸 수 없으므로 인자를 전달할 수 없다. 



### 4.3 DOM Level 2 Event Listener 

결국은 3번째 방식을 사용해야 하지만 이전 방법들도 알고 있어야 한다. 

![event_listener](/Users/mac/Desktop/event_listener.png)



- 하나의 이벤트에 대해 하나 이상의 핸들러를 추가할 수 있다.
- 캡처링과 버블링을 지원한다.
- HTML 요소뿐만아니라 모든 DOM 요소에 대해 동작한다. (SVG도 DOM 요소로 들어올 수 있다.)

[addEventListener()](https://developer.mozilla.org/ko/docs/Web/API/EventTarget/addEventListener) 함수는 IE 9 이상에서 동작한다. IE 8 이하에서는 [attachEvent()](ttps://developer.mozilla.org/ko/docs/Web/API/EventTarget/attachEvent) 함수를 사용한다.

아래와 같이 사용하면 된다. 

```
if (elem.addEventListener) {    // IE 9 ~
  elem.addEventListener('click', func);
} else if (elem.attachEvent) {  // ~ IE 8
  elem.attachEvent('onclick', func);
}
```



```
<!DOCTYPE html>
<html>
<body>
  <script>
    addEventListener('click', function() {
      alert('Clicked!');
    });
  </script>
</body>
</html>
```

window 에다가 달은 것. 어떤 걸 클릭해도 이벤트가 발생된다. 이렇게 하면 안된다.



```
<!DOCTYPE html>
<html>
<body>
  <label for="username">User name </label>
  <input type="text" id="username">
  <em id="message"></em>
  <script>
    var elem = document.getElementById('username');
    var msg  = document.getElementById('message');

    elem.addEventListener('blur', function () {
      if (elem.value.length < 2) {
        msg.innerHTML = '이름은 2자 이상 입력해 주세요';
      } else {
        msg.innerHTML = '';
      }
    });
  </script>
</body>
</html>
```

문자열에 .을 붙인 순간 배열로 바뀌고 length 를 쓸 수 있게 된다. 이름이 2글자 미만이면 '이름을 2자 이상 입력해 주세요' 가 뜨고 아니면 문자열을 지워준다. 



## 5. 핸들러 함수 내부의 this

### 5.3 DOM Level 2 Event Listener

콜백함수에서 this는 이벤트가 바인딩 된 객체다. 

```
<!DOCTYPE html>
<html>
<body>
  <button id="btn">Button</button>
  <script>
    var elem = document.getElementById('btn');
    elem.addEventListener('click', function (event) {
      console.log(this); // <button id="btn">Button</button>
      console.log(event.currentTarget); // <button id="btn">Button</button>
      console.log(this === event.currentTarget); // true
    });
  </script>
</body>
</html>
```



## 6. Event Flow (이벤트의 흐름)

**주의할 것은 버블링과 캡처링은 둘 중에 하나만 발생하는 것이 아니라 캡처링부터 시작하여 버블링으로 종료한다는 것이다.**즉, 이벤트가 발생했을 때 캡처링과 버블링은 순차적으로 발생한다.



## 7. Event 객체

```
<!DOCTYPE html>
<html>
<body>
  <p>클릭하세요. 클릭한 곳의 좌표가 표시됩니다.</p>
  <em id="message"></em>
  <script>
  function showCoords(e) { // e: event object
    var msg = document.getElementById('message');
    msg.innerHTML =
      'clientX value: ' + e.clientX + '<br>' +
      'clientY value: ' + e.clientY;
  }
  addEventListener('click', showCoords);
  </script>
</body>
</html>
```

(e) 는 이벤트 객체. 첫번째 매개변수로 이벤트 객체를 넣어줘야 한다. 꼭 e라고 쓰지 않아도 된다. 

### 7.1 Event Property

#### 7.1.1 Event.target

```
<!DOCTYPE html>
<html>
<body>
  <div class="container">
    <button id="btn1">Hide me 1</button>
    <button id="btn2">Hide me 2</button>
  </div>

  <script>
    function hide(e) {
      e.target.style.visibility = 'hidden';
      // 동일하게 동작한다.
      // this.style.visibility = 'hidden';
    }

    document.getElementById('btn1').addEventListener('click', hide);
    document.getElementById('btn2').addEventListener('click', hide);
  </script>
</body>
</html>
```

e.target.style.visibility = 'hidden';

실제로 이벤트를 발생시킨 타겟을 숨긴다. 

버튼이 만약 2000개 있으면 2000개를 써줘야 한다. 결국 아래처럼 코드를 바꾸어 주어야 한다. 

```
<!DOCTYPE html>
<html>
<body>
  <div class="container">
    <button id="btn1">Hide me 1</button>
    <button id="btn2">Hide me 2</button>
  </div>

  <script>
    function hide(e) {
      // e.target은 실제로 이벤트를 발생시킨 DOM 요소를 가리킨다.
      e.target.style.visibility = 'hidden';
      // this는 이벤트에 바인딩된 DOM 요소(.container)를 가리킨다. 따라서 .container 요소를 감춘다.
      // this.style.visibility = 'hidden';
    }

    var container = document.querySelector('.container');
    container.addEventListener('click', hide);
  </script>
</body>
</html>
```

하나의 addEventListner만 달아도 해결할 수 있다. 



#### 7.1.2 Event.currentTarget

Event.currentTarget 은 항상 this와 동치이다. 



#### 7.1.3 Event.type

발생한 이벤트의 종류를 나타내는 문자열을 반환한다.



#### 7.1.4 Event.cancelable

a 태그의 기본동작은 입력한 사이트로 이동하는 것인데 이것을 하고 싶지 않을 때 사용할 수 있다.

막을 수 있는 이벤트라면  e.preventDefault(); 를 이용하여 동작을 막을 수 있다. 



#### 7.1.5 Event.eventPhase

이벤트 흐름(event flow) 상에서 어느 단계(event phase)에 있는지를 반환한다.

| 반환값 | 의미        |
| ------ | ----------- |
| 0      | 이벤트 없음 |
| 1      | 캡쳐링 단계 |
| 2      | 타깃        |
| 3      | 버블링 단계 |

### 7.2 Event Method

#### 7.2.1 Event.preventDefault() 

이벤트의 기본 동작을 취소한다. 단 Event.cancelable가 true일 경우에 한한다.

**많이 사용한다. **



#### 7.2.2 Event.stopPropagation()

이벤트의 전파(propagation: 버블링, 캡처링)를 중단한다.



## 8. Event Delegation (이벤트 위임)

```
<ul id="parent-list">
  <li id="post-1">Item 1</li>
  <li id="post-2">Item 2</li>
  <li id="post-3">Item 3</li>
  <li id="post-4">Item 4</li>
  <li id="post-5">Item 5</li>
  <li id="post-6">Item 6</li>
</ul>
```

모든 li 요소가 클릭 이벤트에 반응하는 처리를 구현하고 싶은 경우, li 요소에 이벤트 핸들러를 바인딩하면 총 6개의 이벤트 핸들러를 바인딩하여야 한다.

```
function printId() {
  console.log(this.id);
}

document.querySelector('#post-1').addEventListener('click', printId);
document.querySelector('#post-2').addEventListener('click', printId);
document.querySelector('#post-3').addEventListener('click', printId);
document.querySelector('#post-4').addEventListener('click', printId);
document.querySelector('#post-5').addEventListener('click', printId);
document.querySelector('#post-6').addEventListener('click', printId);
```

```
<!DOCTYPE html>
<html>
<body>
  <ul id="parent-list">
    <li id="post-1">Item 1</li>
    <li id="post-2">Item 2</li>
    <li id="post-3">Item 3</li>
    <li id="post-4">Item 4</li>
    <li id="post-5">Item 5</li>
    <li id="post-6">Item 6</li>
  </ul>
  <div id="msg">
  <script>
    var msg = document.getElementById('msg');

    document.getElementById('parent-list').addEventListener('click', function (e) {
      console.log('[target]: ' + e.target);
      console.log('[target.nodeName]: ' + e.target.nodeName);

      // li 요소 이외의 요소에서 발생한 이벤트는 대응하지 않는다.
      if (e.target && e.target.nodeName == 'LI') {
        msg.innerHTML = 'li#' + e.target.id + ' was clicked!';
      }
    });
  </script>
</body>
</html>
```

