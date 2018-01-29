# Chapter 1. Coding!

## 1. 프로그래밍 언어(Programming Language)

언어: 말로 표현할 수 있지만 TEXT로도 전달할 수 있어야 한다. 즉, 의사전달 목적을 달성할 수 있어야 한다. 

프로그램밍 언어는 개발자가 컴퓨터와 이야기하려고 만든 특수한 목적을 가진 인공어다.

그렇다면 HTML/ CSS 는 프로그래밍 언어인가요??

-명령을 전달했을 때 명령되로 실현되는 것이 있기 때문에 프로그밍 언어라고 볼 수 있다.

"결국 프로그래밍은 문법에 부합하는 것은 물론이고 수행하고자 하는 바를 정확히 수행하는 것 즉, **요구사항이 실현(문제가 해결)** 되어야 의미가 있다."

## 2. Computational thinking

수행되어져야 하는 명령을 정의하기 위해서는 해결과제(문제/요구사항)를 이해한 후,복잡함을 단순하게 분해(Deomposition)하고 자료를 정리혹 구분 (Modeling)해야하며 순서에 맞게 행위를 배열해야 한다.

**Decomposition?**

ex)
어떤 일을 해야 할 때 일을 최대한 잘게 쪼개보는 것!
to do 프로그램을 만든다고 했을 때 어떤게 우선순위로 해야하는지 알아야 하고 그 우선순위를 정하려면 사전에 자세한 리서치가 되어야 한다. 이것이 베이스로 깔리지 않으면 기획단계부터 엉클어지게 된다.


## 3. Syntax & Semantics

컴퓨터는 0,1 밖에 모르는 바보.
어떻게 컴퓨터에게 명령을 내려야하지??
 - 자연어를 가지고 사람이 이해할 수 있는 레벨의 인공어를 만들자.
 - 인공어로 명령을 작성하고 컴파일러(compiler) 혹은 인터프리터(interpreter) 라는 번역기를 통해 컴퓨터가 알아들을 수 있는 언어로 번역해서 다시 전달한다.


	프로그래밍은 요구사항의 집합을 분석하여 적절한 자료구조와    
    함수의 집합으로 변환한 후 그 흐름을 제어하는 것이다.


# Chapter 2. Javascript Introduction

## 1. Introduction

1995년 브렌던 **아이크(Brendan Eich)** 가 Netscape Navigator 2를 위하여 개발한 웹페이지에 포함되는 스크립트 언어이다.

**script? 스크립트가 뭘까요?**

- 순서가 있다. 시간의 흐름이 위에서 부터 아래로 있는 것으로 순차적으로 한줄 한줄 실행된다. 
- C 언어는 스크립트 언어가 아니다. C 언어는 compile이란 작업이 있는데 기계어를 컴퓨터가 알아듣도록 해석해준다. 하지만 script는 compile 작업 없이 자동적으로 순간순간 parsing 해서 전달한다. 동시통역이냐 번역이냐? 
- C언어는 운영체제가 실행시키지만 Javascript는 웹브라우져가 실행시킨다. 따라서 모든 플랫폼은 OS 위에서 구동하는 브라우져에서 구동된다. 브라우져가 어떻게 동작하는지에 대해서 잘 알고 있어야 한다. 

**HTML5의 등장과 Javascript 의미**

HTML5가 등장함으로 인해서 Javascript 의 관점에서 보았을 때 매우 다르다. Flash가 있었던 시기. 모든 웹페이지에 움직이는 것은 모두 Flash였으나 웹브라우져에서 동작하긴 하지만 추가적인 설치를 해야 움직일 수 있었다.HTML5는 추가적인 설치를 배제하고 동작하게 한다. 한편 애플에는 Flash를 사용하지 못하게 할꺼라고 선언. 따라서 Flash 가 퇴출당하게 되고 Flash가 가졌던 많은 기능들을 Javascript가 해주게 되었고 따라서 Javascript가 해야 될 일들이 많아졌다. 

**Javascript와 Google**

구글은 광고회사이지만 자바스크립트가 동작하는 파워풀한 엔진을 만들었다. 굉장히 빠른 V8, 그리고 이것이 구동되는 크롬 웹브라우져가 등장. Gmail, Googlemap을 보았을 때 성능이 매우 놀라웠다.

구글맵---> Ajax

Gmail---> 순수한 HTML5로 만들어졌지만 일반 Application 처럼 동작한다. 고성능의 자바스크립트의 엔진으로! 

Javascript가 브라우져에서만 동작했지만 Node.js 라는걸 이용해서 웹에서 빼내게 됐다. 범용적으로 사용할 수 있도록 만들어졌다. Node.js는 V8이 있어서 탄생할 수 있게 되었다. 

**Javascript와 다른 언어의 차이점**

다른 언어들과 비교했을 때 조금 이상하게 느껴지는 부분이 있다. 
대부분의 개발자들은 Class 기반 언어를 먼저 공부한다. 그 관점에서 바라보면 이상한 점이 있다. 자바스크립트는 **프로토타입 기반의 객체 지향 언어.**

**jQuery**

DOM을 쉽게 컨트롤 할 수 있다. Ajax 호출 기능이 있어서 더 각광을 받았다. 모던한 페이지를 만들 떄는 jQuery를 사용하지 않는다. 

자바스크립트는?
인터프리트 언어는 compile 필요없다.
멀티 유즈가 가능한 언어이다. 어떤 문제가 있냐?
사용법이 어려워진다. 따라서 자바스크립트도 어렵다. 프로토타입 기반이이 때문에 클래스가 없다. ES6에는 클래스기반이 새로 들어왔다. 
함수형이란?
함수의 매개변수, 리턴형으로 객체를 받을 수 있는 것. 
프론트엔드 개발자가 다른 언어를 배우지 않고 Javascript로 백엔드 공부까지 할 수 있는 것.

Full stack 개발 언어?? 과연 좋은것이냐?
규모가 어느정도 있는 어플리케이션에서는 말이 되지 않는 일.

SPA(Single Page Application)
Angular, React, Vue.js
웹 애플리케이션이지만 데스크탑 애플리케이션과 흡사하게 동작시켜주는 기술.
Ecma International에 JavaScript의 표준화를 요청하였다.
비영리재단에서 관리해달라고 넘김


## 2. History

ECMAScript Version

![ECMAScript Version](./ECMAScript Version.png)

ES4 리젝트 당함--->Browsers War
Internet Explorer 전성기여서 발언권이 강했는데 ES4에 대한 표준을 받아들이지 않았다. Ecma International 스폰서는 대부분 브라우져사들. ES5와 거의 비슷하다. 이것이 Browser War. 

현재는 결국 연합군이 승리. 연합군 대장은 Google. 이런 저런 표준 제안을 해서 스테이지가 올라가 표준이 되고 각 브라우져들이 받아들이는데 구글은 만들어서 크롬에 올려버려 결국 표준을 만들어 버린다. 

## 3. Browsers Support

모던 브라우저의 ES6 지원은 97%로 거의 100%에 육박하지만 IE 지원을 고려한다면 **babel**과 같은 Transpiler를 사용하여야 한다.

[babel](https://babeljs.io/)


# Chapter 3. Javascript Syntax Basics

## 1. Hello World



## 2. 외부의 Javascript 실행하기 (External JavaScript)
script는 닫는 바디 태그 바로 직전에 사용해야 한다. 스크립트는 html 파일을 먼저 읽어들어와야 그 다음에 해석을 할 수 있다. script파일이 먼저 오면 해석할 html 파일이 없기 때문에 오류가 있을 수 있다. 

## 3. 브라우저 동작 원리

https://
브라우져와 서버간의 약속.
html 파일을 주세요! 
하지만 단방향 통신이다. (무전기 방식)
 
그럼 css, Javascript 두가지는 어떻게 왔지?

![브라우저 동작 원리](./브라우저 동작 원리.png)


**라이브 서버(VS CODE)**


http://127.0.0.1:5500/index.html

127.0.0.1--_>로컬 서버 
:5500---> 포트 넘버 즉 서버의 넘버. 여러개의 서버가 존재할 때 구분하기 위해 붙이는 넘버


## 5. Javascript Syntax Basics

- 기본 자료형 (primitive data type)

 1. Boolean
 2. null
 3. undefined
 4. Number
 5. String
 6. Symbol (New in ECMAScript 6)
 
- Object



[The 2018 Web Developer Roadmap](https://codeburst.io/the-2018-web-developer-roadmap-826b1b806e8d)
