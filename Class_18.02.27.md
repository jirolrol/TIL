# **Extended Parameter Handling**

## 1. 기본 파라미터 초기값 (Default Parameter value)

```
// ES5
function plus(x, y) {
  x = x || 0;
  y = y || 0;
  return x + y;
}

console.log(plus());     // 0
console.log(plus(1, 2)); // 3
```

혼자 함수를 짜는 것이 아니라 만약 분업을 한다고 치면 파라미터에 어떤 값을 넣어야 하는지 다 주석으로 남겨주어야 한다. 

또 사용자가 사용 했을 때 에러가 발생할 수 있다.

위에서 x, y는 숫자가 되어야 하는데 다른 값을 넣어주면 에러가 난다. 그래서 방어 코드를 넣어주어야 한다. 

x가 있는지 없는지 일단 체크하고 x가 undefined 가 되고(false) 뒤에 숫자인 0으로 초기화 된다. 함수를 만들 떄 마다 써주어야 해서 부담스럽다.

```
// ES6
function plus(x = 0, y = 0) {
  // x, y에 인수가 할당되지 않으면 초기값 0이 할당된다.
  return x + y;
}

console.log(plus());     // 0
console.log(plus(1, 2)); // 3
```

인수를 전달하면 0은 무효가 되고 인수를 전달하지 않으면 0이 된다. 



## 2. Rest 파라미터 (Rest Parameter)

### 2.1 Syntax

```
function foo(...rest) {
  console.log(Array.isArray(rest)); // true
  console.log(rest); // [ 1, 2, 3, 4, 5 ]
}

foo(1, 2, 3, 4, 5);
```

...rest 는 풀어져있는 인수를 묶어서 배열로 만들으라는 뜻



```
function foo(param, ...rest) {
  console.log(param); // 1
  console.log(rest);  // [ 2, 3, 4, 5 ]
}

foo(1, 2, 3, 4, 5);

function bar(param1, param2, ...rest) {
  console.log(param1); // 1
  console.log(param2); // 2
  console.log(rest);   // [ 3, 4, 5 ]
}

bar(1, 2, 3, 4, 5);
```

Rest 파라미터는 반드시 마지막 파라미터이어야 한다. 맨 앞에 있다면 모든 인수를 앞에 다 넣어주고 뒤에 인수는 의미가 없어진다.



### 2.2 arguments와 rest 파라미터

```
// ES5
var foo = function () {
  console.log(arguments);
};

foo(1, 2); // { '0': 1, '1': 2 }
```



```
var es5 = function () {};
console.log(es5.hasOwnProperty('arguments')); // true

const es6 = () => {};
console.log(es6.hasOwnProperty('arguments')); // false
```

 ES6의 [Arrow function](http://poiemaweb.com/es6-arrow-function)에는 함수 객체의 arguments 프로퍼티가 없다. 따라서 화살표 함수에서 가변 인자 함수를 구현해야하는 경우, 반드시 rest 파라미터를 사용하여야 한다. 이중지원하지 않는다. 



## 3. Spread 연산자 (Spread Operator)

Spread 연산자(`...`)는 연산자의 대상 배열 또는 [이터러블](http://poiemaweb.com/es6-iteration-for-of)을 개별 요소로 분리한다.

이터러블: 순회할 수 있는. 쉽게 얘기하면 유사배열 객체. 객체는 프로퍼티를 가지고 있는데 그것을 순회하면서 꺼내올 수 있다. 하지만 순서가 보장되지 않는다. 객체를 순회 가능한 객체로 만들어 주는 것을 이터러블이라고 한다.

이터럴에는 어떤 것이 있을까? 

- 'string' 객체: 'string' 생성자 함수로 'string' 객체를 만들 수 있다. 
- HTML collection: getElements 계열의  객체들.
- querySelectorAll: node list.  이것도 이터러블. 
- 배열 
- Map, Set 자료구조(ES6)

```
// ...[1, 2, 3]는 [1, 2, 3]을 개별 요소로 분리한다. 풀어진다. (-> 1, 2, 3)
console.log(...[1, 2, 3]) // -> 1, 2, 3

// 문자열은 이터러블이다.
console.log(...'Helllo');  // H e l l l o

// Map과 Set은 이터러블이다.
console.log(...new Map([['a', '1'], ['b', '2']]));  // [ 'a', '1' ][ 'b', '2' ]
console.log(...new Set([1, 2, 3]));  // 1 2 3
```



### 3.1 함수의 인자로 사용하는 경우

```
// ES5
function foo(x, y, z) {
  console.log(x); // 1
  console.log(y); // 2
  console.log(z); // 3
}

// 배열을 foo 함수의 인자로 전달하려고 한다.
const arr = [1, 2, 3];

// apply 함수의 2번째 인자(배열)는 호출하려는 함수(foo)의 개별 인자로 전달된다.
foo.apply(null, arr);
// foo.call(null, 1, 2, 3);
```

apply는 apply 앞에 있는 함수를 호출하는 것이 1번 목적. 

그런데  this를 앞에 있는 null을 써라. 원래는 foo를 가르키고 있지만.

2번째 인자는 배열을 주어야 하는데 매개변수에게 줄 리스트다. 



call은 어떤 차이가 있나? 

다른건 다 똑같은데 2번쨰 인자에 배열이 아닌 리스트가 들어간다.

```
// ES6
function foo(x, y, z) {
  console.log(x); // 1
  console.log(y); // 2
  console.log(z); // 3
}

// 배열을 foo 함수의 인자로 전달하려고 한다.
const arr = [1, 2, 3];

// ...[1, 2, 3]는 [1, 2, 3]을 개별 요소로 분리한다(-> 1, 2, 3)
// spread 연산자에 의해 분리된 배열의 요소는 개별적인 인자로서 각각의 매개변수에 전달된다.
foo(...arr);
```



```
// ES6
function foo(v, w, x, y, z) {
  console.log(v); // 1
  console.log(w); // 2
  console.log(x); // 3
  console.log(y); // 4
  console.log(z); // 5
}

// ...[2, 3]는 [2, 3]을 개별 요소로 분리한다(-> 2, 3)
// spread 연산자에 의해 분리된 배열의 요소는 개별적인 인자로서 각각의 매개변수에 전달된다.
foo(1, ...[2, 3], 4, ...[5]);
```



### 3.2 배열에서 사용하는 경우

#### 3.2.1 concat

```
// ES5
var arr = [1, 2, 3];
console.log(arr.concat([4, 5, 6])); // [ 1, 2, 3, 4, 5, 6 ]
```

```
// ES6
const arr = [1, 2, 3];
// ...arr은 [1, 2, 3]을 개별 요소로 분리한다
console.log([...arr, 4, 5, 6]); // [ 1, 2, 3, 4, 5, 6 ]
```

concat을 사용하지 않아도 된다. 

#### 3.2.2 push

```
// ES6
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

// ...arr2는 [4, 5, 6]을 개별 요소로 분리한다
arr1.push(...arr2); // == arr1.push(4, 5, 6);

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```

될 수있으면 push를 사용하지 말아라. 원본 배열을 바꾼다.

#### 3.2.3 splice

```
// ES5
var arr1 = [1, 2, 3, 6];
var arr2 = [4, 5];

// apply 메소드의 2번째 인자는 배열. 이것은 개별 인자로 push 메소드에 전달된다.
// [3, 0].concat(arr2) => [3, 0, 4, 5]
// arr1.splice(3, 0, 4, 5) => arr1[3]부터 0개의 요소를 제거하고 그자리(arr1[3])에 새로운 요소(4, 5)를 추가한다.
Array.prototype.splice.apply(arr1, [3, 0].concat(arr2));

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```

```
// ES6
const arr1 = [1, 2, 3, 6];
const arr2 = [4, 5];

// ...arr2는 [4, 5]을 개별 요소로 분리한다
arr1.splice(3, 0, ...arr2); // == arr1.splice(3, 0, 4, 5);

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```

#### 3.2.4 copy

```
// ES5
var arr  = [1, 2, 3];
var copy = arr.slice();

console.log(copy); // [ 1, 2, 3 ]

// copy를 변경한다.
copy.push(4);

console.log(copy); // [ 1, 2, 3, 4 ]
// arr은 변경되지 않는다.
console.log(arr);  // [ 1, 2, 3 ]
```

```
// ES6
const arr = [1, 2, 3];
// ...arr은 [1, 2, 3]을 개별 요소로 분리한다
const copy = [...arr];

console.log(copy); // [ 1, 2, 3 ]

// copy를 변경한다.
copy.push(4);

console.log(copy); // [ 1, 2, 3, 4 ]
// arr은 변경되지 않는다.
console.log(arr);  // [ 1, 2, 3 ]
```



#### 3.3 객체에서 사용하는 경우

Spread 연산자를 사용하면 객체를 결합할 수 있다.

```
const o1 = { x: 1, y: 2 };
const o2 = { ...o1, z: 3 };

console.log(o2); // { x: 1, y: 2, z: 3 }

const target = { x: 1, y: 2 };
const source = { z: 3 };

// Object.assign를 사용하여도 동일한 작업을 할 수 있다.
// Object.assign은 타깃 객체를 반환한다
console.log(Object.assign(target, source)); // { x: 1, y: 2, z: 3 }
```





# 6. Enhanced Object property

## 1. 프로퍼티 축약 표현

```
// ES5
var x = 1, y = 2;

var obj = {
  x: x,
  y: y
};

console.log(obj); // { x: 1, y: 2 }

```

ES6에서는 프로퍼티 값으로 변수를 사용하는 경우, <u>프로퍼티 이름을 생략(Property shorthand)할 수 있다.</u> 이때 프로퍼티 이름은 변수의 이름으로 자동 생성된다.

```
// ES6
let x = 1, y = 2;

const obj = { x, y };

console.log(obj); // { x: 1, y: 2 }
```



## 2. 프로퍼티 이름 조합

이런 방법이 있는 것만 알아두기.

```
// ES5
var i = 0;
var propNamePrefix = 'prop_';

var obj = {};

obj[propNamePrefix + ++i] = i;
obj[propNamePrefix + ++i] = i;
obj[propNamePrefix + ++i] = i;

console.log(obj); // { prop_1: 1, prop_2: 2, prop_3: 3 }
```

객체 내부에서 진행할 수 있다. 

```
// ES6
let i = 0;
const propNamePrefix = 'prop_';

const obj = {

[propNamePrefix + ++i]: i,
[propNamePrefix + ++i]: i,
[propNamePrefix + ++i]: i

};

console.log(obj); // { prop_1: 1, prop_2: 2, prop_3: 3 }
```



## 3. 메소드 축약 표현

```
// ES5
var obj = {
  name: 'Lee',
  sayHi: function() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee

```

ES6에서는 메소드를 선언하기 위해서 <u>function 키워드를 생략한 축약 표현을 사용할 수 있다.</u>

```
// ES6
const obj = {
  name: 'Lee',
  // 메소드 축약 표현
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee
```

sayHi: function() {
​    console.log('Hi! ' + this.name);

sayHi() {
​    console.log('Hi! ' + this.name);
  }

메소드에는 화살표 함수 쓰지 말아라. 



## 4. __proto__ 프로퍼티에 의한 상속

이것도 알아만 두기.

```
// ES5
var parent = {
  name: 'parent',
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};

// 프로토타입 패턴 상속
var child = Object.create(parent);
child.name = 'child';

parent.sayHi(); // Hi! parent
child.sayHi();  // Hi! child
ㅇ
```

var child = Object.create(parent);

Object.create()의 인자에 준 객체 자신의 __proto__ 로 지정해줄 수 있다. 

```
// ES6
const parent = {
  name: 'parent',
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};

const child = {
  // child 객체의 프로토타입 객체에 parent 객체를 바인딩하여 상속을 구현한다.
  __proto__: parent,
  name: 'child'
};

parent.sayHi(); // Hi! parent
child.sayHi();  // Hi! child
```

부작용이 많고, 많은 브라우저에서 지원하지 않으므로 사용금지.



# 6. Destructuring

디스트럭처링(Destructuring)은 구조화된 객체(배열 또는 객체)를 Destructuring(비구조화, 파괴)하여 개별적인 변수에 할당하는 것이다. <u>배열 또는 객체 리터럴에서 필요한 값만을 추출하여 변수에 할당하거나 반환할 때 유용하다.</u>

## 1. 배열 디스트럭처링 (Array destructuring)

```
// ES5
var arr = [1, 2, 3];

var one   = arr[0];
var two   = arr[1];
var three = arr[2];

console.log(one, two, three); // 1 2 3
```

```
// ES6 Destructuring
const arr = [1, 2, 3];

// 인덱스를 기준으로 배열로부터 요소를 추출하여 변수에 할당
const [one, two, three] = arr;

console.log(one, two, three); // 1 2 3
```

항상 순서가 유의미하다. 

const [one, two, three] = arr;

여기서 one, two, three는 변수다. 

```
let x, y, z;
[x, y, z] = [1, 2, 3];

// 위의 구문과 동치이다.
let [x, y, z] = [1, 2, 3];
```



```
[x, y] = [1, 2, 3];
console.log(x, y); // 1 2

[x, , z] = [1, 2, 3];
console.log(x, z); // 1 3

// default value
[x, y, z = 3] = [1, 2];
console.log(x, y, z); // 1 2 3

[x, y = 10, z = 3] = [1, 2];
console.log(x, y, z); // 1 2 3

// spread operator
[x, ...y] = [1, 2, 3];
console.log(x, y); // 1 [ 2, 3 ]
```

default value 는 줄 애가 없으면 쓰고 줄 애가 있으면 무시된다. 



## 2. 객체 디스트럭처링 (Object destructuring)

```
// ES5
var obj = { firstName: 'Ungmo', lastName: 'Lee' };
var name = {};

name.firstName = obj.firstName;
name.lastName  = obj.lastName;

console.log(name); // { firstName: 'Ungmo', lastName: 'Lee' }
```

객체 디스트럭처링은 객체의 각 프로퍼티를 객체로부터 추출하여 변수 리스트에 할당한다. 이때 할당 기준은 **프로퍼티 이름(키)**이다.

```
// ES6 Destructuring
const obj = { firstName: 'Ungmo', lastName: 'Lee' };

const { firstName, lastName } = obj;

console.log(firstName, lastName); // Ungmo Lee
```



객체 디스트럭처링은 객체에서 프로퍼티 이름(키)으로 필요한 프로퍼티 값만을 추출할 수 있다.

```
function margin() {
  const left = 1, right = 2, top = 3, bottom = 4;
  return { left, right, top, bottom };
}
const { left, bottom } = margin();
console.log(left, bottom); // 1 4
```



# 7. Class

Javascript는 **프로토타입 기반(prototype-based)** 객체지향형 언어다. 

왜냐? 자바스크립트의 대부분은 객체다. 

타언어보다 객체를 훨씩 쉽게 만든다. Class가 없어도 만들 수 있다. 

생성자 함수 자체가 Class 와 비슷하다고 보면 된다. 

```
// ES5
var Person = (function () {
  // private member 내부에서만 사용할 수 있는 지역변수.
  var _name = '';

  // Constructor 생성자 함수
  function Person(name) {
     setName(name);
  }

  // private mathods 내부 함수 
  function setName(name) {
     _name = name;
  }

  function getName() {
     return _name;
  }

  // public methods 공개되어야 하는 메소드들
  Person.prototype = {
     sayHi: function () {
       console.log('Hi! ' + getName());
     },
     sayBye: function () {
       console.log('Bye~ ' + getName());
     }
   };

  // return constructor
  return Person;
}());
```

 ES6의 클래스가 새로운 객체지향 모델을 제공하는 것이 아니며 사실 **클래스도 함수**이고 기존 프로토타입 기반 패턴의 [Syntactic sugar](https://en.wikipedia.org/wiki/Syntactic_sugar)일 뿐이다.



## 1. 클래스 정의 (Class Definition)

```
class Person {
  constructor(name) {
    this._name = name;
  }

  sayHi() {
    console.log(`Hi! ${this._name}`);
  }
}

const me = new Person('Lee');
me.sayHi(); // Hi! Lee

console.log(me instanceof Person); // true
```

class 라는 키워드를 이용해서 정의해준다. class 는 결국 함수다. 첫 문자는 대문자로 써준다. 내부에는 반드시 constructor라는 함수를 가지고 있어야 한다. 객체를 만들어 준다. class에서는 프로퍼티라고 하지 않고 멤버라고 한다. class 안에는 반드시 함수만 있어야 한다. 

얘도 선언식인데 모든 선언식은 호이스팅이 일어난다. 하지만 ES6에서는 호이스팅이 일어날 떄 조금 다른다. 선언과 초기화 사이에 TMZ가 있어서 에러가 일어난다. 



## 2. 인스턴스의 생성

클래스의 인스턴스를 생성하려면 new 연산자와 함께 생성자를 호출한다.

```
class Foo {}

const foo = new Foo();

```

**new 연산자**를 사용하지 않고 생성자를 호출하면 에러가 발생한다.

```
class Foo {}

const foo = Foo(); // TypeError: Class constructor Foo cannot be invoked without 'new'
```

언제 에러가 날까? 런타임에 에러가 난다. 