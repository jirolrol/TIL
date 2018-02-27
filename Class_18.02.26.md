18.02.26(월)



# 1.  let, const와 블록 레벨 스코프

## 1. let

### 1.1 Block-level scope



- var의 가장 큰 문제점은 scope. Function-level scope (Block-level scope를 지원하지 않는다.)


- 전역변수는 여러면에서 문제가 많은데, 

  코딩측면에서 바라보면 의도치 않게 변수명이 중복될 수 있다. 의도치 않게 변수 값이 바꿀 수 있다.

  var 키워드를 생략하면 전역변수로 선언이 된다. 

- 변수 호이스팅 

  실행 컨텍스트 상에서 변수를 만들 때 선언, 초기화, 할당 중 선언 초기화가 한 번에 이루어진다. 선언을 어디에 하든지 참조가 가능하다. 변수값은 할당 단계에서 이루어지기 때문에 할당하지 않는 이상 undefined 가 할당된다.

let은 블록레벨 스코프레벨이 가능하고 재할당이 안되고, 호이스팅이 안되는 것 처럼 움직인다. 

함수를 작게 쓰는 연습을 해야한다. 함수를 될 수 있으면 한줄로 쓰려고 한다. 영어 읽듯이 읽히는 코드를 쓰려고 한다. 

if문, for문 내에서 쓴 let은 지역변수이다. 

```
// ES5

console.log(foo); // undefined
var foo = 123;
console.log(foo); // 123
{
  var foo = 456;
}
console.log(foo); // 456

// ES6

let foo = 123;
{
  let foo = 456;
  let bar = 456;
}
console.log(foo); // 123
console.log(bar); // ReferenceError: bar is not defined
```



### 1.2 중복 선언 금지

let은 **중복 선언 시 SyntaxError**가 발생한다.

```
var foo = 123;
var foo = 456;  // OK

let bar = 123;
let bar = 456;  // Uncaught SyntaxError: Identifier 'bar' has already been declared
```



### 1.3 호이스팅(Hoisting)

모든 선언(var, let, const, function, [function*](http://poiemaweb.com/es6-generateor), class)을 호이스팅(Hoisting)한다.



```
console.log(foo); // undefined
var foo;

console.log(bar); // Error: Uncaught ReferenceError: bar is not defined
let bar;

// 호이스팅은 일어나지만 일어나지 않는 것 처럼 보인다. 실제로는 호이스팅이 일어난다. 
```

![let-lifecycle](/Users/mac/Documents/dev/TIL/let-lifecycle.png)



### 1.4 클로저

```
var funcs = [];

// 함수의 배열을 생성한다
// i는 for loop에서만 유효한 지역변수이면서 자유변수이다
for (let i = 0; i < 3; i++) {
  funcs.push(function () { console.log(i); });
}
// 여기서 i 는 closure에서 말했던 자유변수이다. 


// 배열에서 함수를 꺼내어 호출한다
for (var j = 0; j < 3; j++) {
  funcs[j]();
}
```



### 1.5 전역 객체와 let

let 키워드로 선언된 변수를 전역 변수로 사용하는 경우, let 전역 변수는 전역 객체의 프로퍼티가 아니다. 즉 window.foo와 같이 접근할 수 없다. let 전역 변수는 보이지 않는 개념적인 블럭 내에 존재하게 된다.

```
let foo = 123; // 전역변수

console.log(window.foo); // undefined
```



# 2. const

### 2.1 선언과 초기화

재할당이 불가능하기 때문에 선언시 바로 초기화해야 한다. 선언과 초기화를 따로 할 수 없다. 

```
const FOO; // SyntaxError: Missing initializer in const declaration

{
  const FOO = 10;
  console.log(FOO); //10
}

// FOO가 대문자인 이유는 상수라는 뜻. 변하지 않는 수를 상수라고 한다. 

console.log(FOO); // ReferenceError: FOO is not defined
```



### 2.2 상수

```
// x의 의미를 알기 어렵기 때문에 가독성이 좋지 않다.
if (x > 10) {
}

// 변수의 의미를 명확히 기술하여 가독성이 향상되었다.
const MAXROWS = 10;
if (x > MAXROWS) {
}
```

조건문 내의 10은 어떤 의미로 사용하였는지 파악하기가 곤란하다. 하지만 네이밍이 적절한 상수로 선언하면 가독성과 유지보수성이 대폭 향상된다.



const를 쓸 때는 꼭 상수에만 사용하지는 않는다. obj를 소문자로 사용했다. 객체타입에는 const를 쓰는 것이 좋다. 즉 객체는 재할당을 하지 않는 것이 좋다. 객체의 내용을 바꾸었을 때 주소가 바뀔까? 안바뀐다. 따라서 const를 사용해도 무방하다. 하지만 재할당을 해야하는 객체에 대해서는 const를 사용하지 않아도 좋다. 

```
const obj = { foo: 123 };
obj = { bar: 456 }; // TypeError: Assignment to constant variable.
```



### 2.3 const와 객체

**객체의 프로퍼티는 보호되지 않는다.** 다시 말하자면 재할당은 불가능하지만 할당된 객체의 내용(프로퍼티)은 변경할 수 있다.

```
const user = {
  name: 'Lee',
  address: {
    city: 'Seoul'
  }
};

// const 변수는 재할당이 금지된다.
// user = {}; // TypeError: Assignment to constant variable.

// 프로퍼티 값의 재할당은 허용된다!
user.name = 'Kim';

console.log(user); // { name: 'Kim', address: { city: 'Seoul' } }
```

**객체 타입 변수 선언에는 const를 사용하는 것이 좋다.**



## 3. var vs. let vs. const



# 2. Templete Literals

ES6는 템플릿 리터럴(template Literals)이라고 불리는 새로운 문자열 표기법을 도입하였다. 백틱(backtick) 문자 ```를 사용한다.

```
const template = `템플릿 리터럴은 '작은따옴표(single quotes)'과 "큰따옴표(double quotes)"를 혼용할 수 있다.`;

console.log(template);
```

```
const template = `<ul class="nav-items">
  <li><a href="#home">Home</a></li>
  <li><a href="#news">News</a></li>
  <li><a href="#contact">Contact</a></li>
  <li><a href="#about">About</a></li>
</ul>`;

console.log(template);
```

```
const first = 'Ung-mo';
const last = 'Lee';

// 기존의 문자열 연결
console.log('My name is ' + first + ' ' + last + '.');

// ES6 String Interpolation
console.log(`My name is ${first} ${last}.`); // My name is Ung-mo Lee.
```

`${expression}`을 템플릿 대입문(template substitution)이라 한다. string interpolation


```
// 템플릿 대입문에는 문자열뿐만 아니라 표현식도 사용할 수 있다.
console.log(`1 + 1 = ${1 + 1}`); // 1 + 1 = 2

const name = 'ungmo';

console.log(`Hello ${name.toUpperCase()}`); // Hello UNGMO
```

하지만 템플릿 대입문 안에 복잡한 식을 사용하는 것은 피해야 한다. 



# 3. Arrow funciton

## 1. Arrow function의 선언

Arrow function(화살표 함수)은 function 키워드 대신 화살표(=>)를 사용하여 간략한 방법으로 함수를 선언할 수 있다.

```
// 매개변수 지정 방법
    () => { ... } // 매개변수가 없을 경우
     x => { ... } // 매개변수가 한개인 경우, 소괄호를 생략할 수 있다.
(x, y) => { ... } // 매개변수가 여러개인 경우, 소괄호를 생략할 수 없다.

// 함수 몸체 지정 방법
function(x){
    return x * x ;
}
x => { return x * x }  // single line block
x => x * x  // 함수 몸체가 한줄의 구문이라면 중괄호를 생략할 수 있으며 암묵적으로 return된다. 위 표현과 동일하다.

() => { return { a: 1 }; }
() => ({ a: 1 })  // 위 표현과 동일하다. 객체 반환시 소괄호를 사용한다.

() => {           // multi line block.
  const x = 10;
  return x * x;
};
```



## 2. Arrow function의 호출

Arrow function은 익명 함수로만 사용할 수 있다. 즉 기본적으로 콜백 함수에만 사용한다.

```
// ES5
var pow = function (x) { return x * x; };
console.log(pow(10)); // 100

// ES6
const pow = x => x * x;
console.log(pow(10)); // 100
```



```
// ES5
var arr = [1, 2, 3];
var pow = arr.map(function (x) { // x는 요소값
  return x * x;
});

console.log(pow); // [ 1, 4, 9 ]

// ES6
const arr = [1, 2, 3];
const pow = arr.map(x => x * x);

console.log(pow); // [ 1, 4, 9 ]
```



## 3. this





### 3.2 Arrow function의 this

```
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  return arr.map(x => `${this.prefix}  ${x}`);
};

const pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```



## 4. Arrow Function을 사용해서는 안되는 경우

### 4.1 메소드

```
// Bad
const obj = {
  name: 'Lee',
  sayHi: () => console.log(`Hi ${this.name}`)
};

obj.sayHi(); // Hi undefined

//여기서의 this는 바로 위 window를 가르킨다. 

// Good
const obj = {
  name: 'Lee',
  sayHi() { // === sayHi: function() {
    console.log(`Hi ${this.name}`);
  }
};

obj.sayHi(); // Hi Lee
```



## 4.2 prototype

```
// Bad

const obj = {

  name: 'Lee',

};

Object.prototype.sayHi = () => console.log(Hi ${this.name});

obj.sayHi(); // Hi undefined


// Good
const obj = {
  name: 'Lee',
};

Object.prototype.sayHi = function() {
  console.log(`Hi ${this.name}`);
};

obj.sayHi(); // Hi Lee

```



### 4.4 addEventListener 함수의 콜백 함수

addEventListener 함수의 콜백 함수를 화살표 함수로 정의하면 this가 상위 컨택스트를 가리킨다.



```
// Bad
var button = document.getElementById('myButton');

button.addEventListener('click', () => {
  console.log(this === window); // => true
  this.innerHTML = 'Clicked button';
});

```

따라서 addEventListener 함수의 콜백 함수는 function 키워드로 정의한 함수를 사용하여야 한다.

```
// Good
var button = document.getElementById('myButton');

button.addEventListener('click', function() {
  console.log(this === button); // => true
  this.innerHTML = 'Clicked button';
});
```

