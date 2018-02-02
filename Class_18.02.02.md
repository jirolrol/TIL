18.02.02(금)

## 7. 함수의 다양한 형태

### 7.1. 즉시호출함수표현식 (IIFE, Immediately Invoke Function Expression)

    // 기명 즉시실행함수(named immediately-invoked function expression)
    
    (function myFunction() {
      var a = 3;
      var b = 5;
      return a * b;
    }());
    
    --->별도의 호출문을 사용하지 않아도 한 번 호출된다. 
    
    // 익명 즉시실행함수(immediately-invoked function expression)
    
    (function () {
      var a = 3;
      var b = 5;
      return a * b;
    }());
    
    --->익명이면 절대 호출되지 않는다. 
    
### 7.2 내부 함수 (Inner function)

함수 내부에 있는 함수.

    function parent(param) {
      var parentVar = param;
      function child() {
        var childVar = 'lee';
        console.log(parentVar + ' ' + childVar); // Hello lee
      }
      child();
      console.log(parentVar + ' ' + childVar);
      // Uncaught ReferenceError: childVar is not defined
    }
    parent('Hello');


### 7.3 콜백 함수 (Callback function) **중요**

나중에 호출하는 함수.

    <!DOCTYPE html>
    <html>
    <body>
      <button id="myButton">Click me</button>
      <script>
        var button = document.getElementById('myButton');
        button.addEventListener('click', function() {
          console.log('button clicked!');
        });
      </script>
    </body>
    </html>

# 5.10 프로토타입과 객체지향

## 1. 프로토타입 객체


    var student = {
      name: 'Lee',
      score: 90
    };

    // student에는 hasOwnProperty 메소드가 없지만 아래 구문은 동작한다.
    console.log(student.hasOwnProperty('name')); // true

    console.dir(student);
    
기본적으로 들어있는 메소드 hasOwnProperty.
    
## 2. [[Prototype]] 프로퍼티 vs prototype 프로퍼티

[[Prototype]] 은 크롬에서 __ proto __

## 3. constructor 프로퍼티
## 4. Prototype chain

### 4.1 객체 리터럴 방식으로 생성된 객체의 프로토타입 체인

객체 리터럴은 단 하나의 객체를 만들 때만 사용해라.
단 하나의 --proto__ 단계만 존재한다. 

### 4.2 생성자 함수로 생성된 객체의 프로토타입 체인

## 5. 프로토타입 객체의 확장

    function Person(name) {
      this.name = name;
    }

    var foo = new Person('Lee');

    Person.prototype.sayHello = function(){
      console.log('Hi! my name is ' + this.name);
    };

    foo.sayHello();
    

## 6. 기본자료형(Primitive data type)의 확장

    var str = 'test';
    console.log(typeof str);                 // string
    console.log(str.constructor === String); // true
    console.dir(str);

    var strObj = new String('test');
    console.log(typeof strObj);                 // object
    console.log(strObj.constructor === String); // true
    console.dir(strObj);

    console.log(str.toUpperCase());    // TEST
    console.log(strObj.toUpperCase()); // TEST
    
기본형자료는 . 을 찍는 순간 객체로 바뀐다. 
만약 문자열이라면 . 을 찍는 순간 객체로 사용하려고 하는구나 라고 생각하고 객체로 바꿔 메소드를 사용하게 하고 다시 기본 자료형으로 돌려 놓는다. 
    
    
## 7. 프로토타입 객체의 변경


# 5.11 Javascript Scope 

Scope=유효범위

    var x = 0;
    {
      var x = 1;
      console.log(x); // 1
    }
    console.log(x);   // 1

    let y = 0;
    {
      let y = 1;
      console.log(y); // 1
    }
    console.log(y);   // 0
    
    ----> let은 블록 레벨 스코프를 지원한다. 
    
    
Javascript는 진입점이 없다. 쓴 순서대로 실행된다. 
전역변수는 어디서든 참고할 수 있다. 

기본적으로 타 언어들은 코드블록이 하나의 지역이다. 하지만 Javascript는 코드블럭을 지역으로 인정하지 않는다. ---> block level scope
함수 영역만 지역으로 인정한다.---> **function level scope** 

지역변수는 지역에서만 참조할 수 있다. 


	var global = 'global';

    function foo() {
      var local = 'local';
      console.log(global);
      console.log(local);
    }
    foo();

    console.log(global);
    console.log(local); // Uncaught ReferenceError: local is not       defined

**왜 지역변수, 전역변수를 만들었을까?** 
- 한 폴더 내에서 똑같은 이름의 파일 2개를 만들 수 없는 것처럼 전역변수도 이름을 사용하지 못한다. 
- 전역변수는 어디서든 참조할 수 있으니까 라이프 사이클이 무한정이다. 이 애플리케이션이 살아있는 한 존재한다. 즉 브라우져를 끄지 않는 한 계속 메모리를 점유하고 있다. 다 전역변수면 메모리를 엄청나게 잡아먹는다. 
- 지역변수는 메모리를 효율적으로 사용한다. 

## 2. Non block-level scope

    if (true) {
      var x = 5; // The scope is inside the if-block
    }
    console.log(x);
    
    if문 안에서 선언된 변수는 전역변수. for문도 마찬가지
    
## 3. Function scope

    var a = 10;     // 전역변수

    (function () {
      var b = 20;   // 지역변수
    })();

    console.log(a); // 10
    console.log(b); // "b" is not defined
    
    
    var x = 'global';
    
    

    function foo() {
      var x = 'local';
      console.log(x);
    }

    foo();          // local
    console.log(x); // global
    
    
    
## 4. 암묵적 전역 (implied globals)

    function foo() {
      x = 1;   // Throws a ReferenceError in "use strict" mode
      var y = 2;
    }

    foo();
 
var를 생략했기 때문에 x를 전역변수로 지정해준다. 

## 5. Lexical scoping (Static scoping)

선언시점 당시에 scope를 갖는다!

    var i = 5;

    function foo() {
      var i = 10;
      bar();
    }

    function bar() { // 선언된 시점에서의 scope를 갖는다!
      console.log(i);
    }

    foo(); // ?
    
    
## 6. 변수명의 중복

    // x.js
    
    function foo (){
    
      // var i = 0;
      
      i = 0;
      
      // ...
    }

    // y.js
    
    for(var i = 0; i < 5; i++){
    
      foo();
      ----> 여기서 계속 i 를 0으로 만들기 때문에 무한루프가 돈다. 
      console.log(i);
      
    }
    
전역변수는 안쓰면 안되는 이유가 꼭 있어야 사용할 수 있다.

## 7. 최소한의 전역변수 사용

## 8. 즉시실행함수를 이용한 전역변수 사용 억제


# ESlint

타 언어들이 기본적으로 파일단위의 scope를 가지고 있다. 
node.js는 파일 단위의 scope를 가지고 있다. 
애플리케이션으로 사용하려는 

자바스크립트가 다른 자바스크립트를 부를 수 있어야 하고 불렀을 때 서로 다른 영역으로 가지고 있어야 한다. 

웹팩이라는 것이 있는데 

npm
package= module의 개념이다.
npm의 package들을 다운받아 사용한다. 
버전 업그레이드가 쉽다.


# 5.12 Javascript this

this는 언제나 전역 개체이다. 

단, 2가지만 빼고!

- 메소드 안에 있는 this: 메소드를 호츨한 객체가 this.
- 생성자 함수 안에 있는 this: 자신이 생성할 객체를 가르킨다. 

this는 항상 메소드나 생성자 함수에 담겨있다. 즉 함수에 담겨있다. 

## 1. 함수 호출 패턴(Function Invocation Pattern)

브라우져에서 도는 자바스크립트는 DOM BOM 이라는 걸 알아야 한다.


전역객체란 객체중에 가장 사위 객체다. 유일하고 하나만 생성된다. 
그 객체는 브라우져에서는 window node.js 에서는 global을 가르킨다.
즉, 전역변수는 window 객체의 프로퍼티다.


    var ga = 'Global variable';

    console.log(ga);
    console.log(window.ga);

    function foo() {
      console.log('invoked!');
    }
    window.foo();
    
결국 모든 함수는 메소드이다! 

### 3.1 생성자 함수 동작 방식

new 란 키워드. 즉 명령어다. 
new가 어떤걸 해줄까?

new를 붙이면 생성자 함수를 인식하고 암묵적으로(자동으로)3가지를 한다.

    ar Person = function(name) {
      // 생성자 함수 코드 실행 전 -------- 1
      this.name = name;  // --------- 2
      // 생성된 함수 반환 -------------- 3
    }

    var me = new Person('Lee');
    console.log(me.name);

1. 빈 객체를 하나를 만든다.
2. window를 가르키고 있던 this가 그 빈 객체를 가르키게 한다. 그리고 새로 생성한 객체를 부른다. 새로 생성한 빈객체에다가 네임 프로퍼티와 Lee를 집어 넣어준다. 
3. 리턴해준다. 


## 4. apply 호출 패턴(Apply Invocation Pattern)

    function convertArgsToArray() {
      console.log(arguments);

      // arguments 객체를 배열로 변환
      // slice: 배열의 특정 부분에 대한 복사본을 생성한다.
      var arr = Array.prototype.slice.apply(arguments); // 
      arguments.slice
      // var arr = [].slice.apply(arguments);

      console.log(arr);
      return arr;
    }

    convertArgsToArray(1, 2, 3);