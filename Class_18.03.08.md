18.03.08(목)



# 1. TypeScript - Intro & Install

## 1. Introduction

Type을 지원한다. 

IDE 또는 에디터를 사용해서 개발을 하게 되는데 TypeScript를 사용하면 에디터의 도움을 지원받을 수 있다. 

자바나 C#을 아는 사람은 TypeScript가 정말 쉽다. TypeScript를 개발한 사람이 C#을 개발한 사람. 클래스 기반 언어처럼 사용하는 것이라 prototype을 생각하지 않아도 된다. 기본적인 클래스 기반의 언어를 배우고 이것을 배워야는데 만약 모르는 상태라면 나중에라도 공부해야함. 2~3년이 지나면 2~3가지 언어를 해야 발전이 있음. 한가지 언어에 함몰되면 안된다. 



ES6도 아직 부족한 것이 모듈 지원이 안된다. 클래스도 완벽하지 않음. class라는 키워드로 객체 생성하고 상속하는 기능밖에 없다. 결국 javascript가 범용적으로 사용되기에는 아직 부족하다. 

CoffeeScript, Dart, Haxe —> AltJS(Javascript 대체언어) 얘네들이 컴파일 되고 나면 Javascript가 된다. 이걸로도 결국 부족해서 Microsoft에서 TypeScript 와 VS Code를 같이 개발하기 시작. 

TypeScript를 쓰면 Barbel이 필요 없다. 단, 개발환경을 갖춰야 한다. Angular도 Typescript에서 돌아간다. 

OOP를 공부한다는 것은 대규모 어플리케이션을 만들 수 있는 능력을 기른다는 것. Class, 



## 2. TypeScript를 사용하는 이유

### 2.1 정적 타입

정적타입을 가능하게 된다. 타입을 정해 놓으면 실수가 줄어든다. 그렇게 사용할 수 밖에 없는 환경을 만들어야 한다. 

아래 코드는 개발자의 의도를 정확하게 전달하지 못한다. 

```
function sum(a, b) {
  return a + b;
}
```

타입스크립트를 도입하면 개발자의 의도가 완벽히 표현된다. 

**명시적인 정적 타입 지정은 개발자의 의도를 명확히 코드에 기술할 수 있다.** 이는 코드의 가독성을 향상 시키고 예측을 가능하게 하며 디버깅을 쉽게 한다.

```
function sum(a: number, b: number) {
  return a + b;
}

sum('x', 'y'); // error TS2345: Argument of type '"x"' is not assignable to parameter of type 'number'.
```

### 2.2 도구의 지원

TypeScript를 사용하는 이유는 여러가지 있지만 가장 큰 장점은 IDE(통합개발환경)를 포함한 다양한 **도구의 지원**을 받을 수 있다는 것이다.

IDE: 애플리케이션을 만들 떄 개발환경이 있을 텐데 자바와 스프링으로 개발한다고 했을 때 둘 다 지원한다. 

에디터에게 타입 정보만 알려주어도 많은 일을 할 수 있다. 



### 2.3 강력한 OOP 지원

**인터페이스, 제네릭** 등과 같은 강력한 OOP 지원은 크고 복잡한 프로젝트의 코드 기반을 쉽게 구성할 수 있도록 돕는다. 

OOP: 클래스 기반 객체지향을 의미한다. 



### 2.4 ES6 / ES Next 지원

ES Next : 미래에 올 ES 버전.



### 2.5 Angular

TypeScript로 작성된 것이 대부분이어서 관련 정보 취득에 이점이 있으며 이러한 현상은 앞으로도 지속될 것으로 예상된다.



## 3. 개발환경 구축

TypeScript 파일(.ts)은 브라우저에서 동작하지 않으므로 TypeScript 컴파일러를 통해 자바스크립트 파일로 변환이 필요하다. 이를 컴파일 또는 트랜스파일링이라 한다.

트랜스파일링된 person.js의 자바스크립트 버전은 ES3이다. ( ES6 ES7을 지원한다는 의미이다. )

ES5 버전으로 트랜스파일링을 실행하려면 아래와 같이 옵션을 추가한다.

```
$ tsc person.ts -t ES5
```



Barbel 을 쓴 목적은 하위버전으로 트랜스파일링 하기 위해서 사용한다. 

webpack을 쓴 목적은 

1. 모듈 로더의 기능을 한다. 모듈을 이용한 라이브러리를 사용하여 인 아웃 하게 해준다. 
2. 싸스, 바벨 , 타입스크립트 모두 사용하면 매번 명령을 내려야하는데 알아서 하게 해준다. 
3. 여러개의 자바스크립트 파일, 여러개의 이미지, 여러개의 폰트로 애플리케이션으로 구성이 될 것인데 하나로 뭉쳐지게 만드는데 번들로의 역할이 도움이 된다. 



Typescript는 모듈로더의 기능이 있다. 하지만 브라우저에서 먹히지 않는다. 브라우저에는 그 개념이 없기 때문에 결국은 webpack을 사용해야 한다. 



모든 TypeScript 파일을 한꺼번에 트랜스파일링할 수도 있다.

```
$ tsc *.ts
$ node student
Hello, Lee
Lee is studying.
```

`--watch` 또는 `-w` 옵션을 사용하면 대상 파일이 변경되었을 때 이를 감지하여 자동으로 트랜스파일링이 실행된다.

```
$ tsc student.ts --watch
// 이 파일이 변경되면 자동적으로 트랜스파일링 하라는 뜻. 
21:23:30 - Compilation complete. Watching for file changes.
```



# 3. TypeScript - Typing

동적타입, 정적타입 모두 장 단점이 있다. 

단, 대규모 애플리케이션을 만든다면 정정타입이 훨씬 유리하다. 

## 1. 타입 선언 (Type Declaration)

```
let foo: string = 'hello';
```

foo라는 변수는 값으로 string 타입만 받을 수 있다. 안그러면 빨간 줄이 그어지고 컴파일이 되지 않는다.



```
// 함수선언식
function multiply1(x: number, y: number): number {
  return x * y;
}
// 마지막 number는 return 타입에 대한 지정. 꼭 써주지 않아도 된다. 왜내먄 추축이 가능하기 떄문에.

// 함수표현식
const multiply2 = (x: number, y: number): number => x * y;

console.log(multiply1(10, 2));
console.log(multiply2(10, 3));

console.log(multiply1(true, 1)); // error TS2345: Argument of type 'true' is not assignable to parameter of type 'number'.
```

 JavaScript의 타입 이외에도 TypeScript 고유의 타입이 추가로 제공된다.

| array |      | ◯    | 배열                                                         |
| ----- | ---- | ---- | ------------------------------------------------------------ |
| tuple |      | ◯    | 고정된 요소수 만큼의 자료형을 미리 선언후 배열을 표현        |
| enum  |      | ◯    | 열거형. 숫자값 집합에 이름을 지정한 것이다.                  |
| any   |      | ◯    | 타입 추론(type inference)할 수 없거나 타입 체크가 필요없는 변수는 any 타입으로 선언한다. |
| void  |      | ◯    | 일반적으로 함수에서 반환값이 없을 경우 사용한다.             |
| never |      | ◯    | 결코 발생하지 않는 값                                        |

```
// boolean
let isDone: boolean = false;
// 여기서는 타입 정의해줄 필요가 없다. 이미 할당을 다 했기 때문에.

// null
let n: null = null;

// undefined
let u: undefined = undefined;

// number
let decimal: number = 6;
let hex: number = 0xf00d; // 16진수
let binary: number = 0b1010;
let octal: number = 0o744; // 8진수 

// string
let color: string = "blue";
color = 'red';
let myName: string = `Lee`; // ES6 템플릿 문자열
let greeting: string = `Hello, my name is ${ myName }.`; // ES6 템플릿 대입문

// object
const obj: object = {};// 1년 이내에 추가된 것.

// array **중요** 
let list1: any[] = [1, 'two', true]; // 요소로 아무거나 다 된다. 
let list2: number[] = [1, 2, 3]; // 배열일 때는 이 방법을 사용하는 것이 좋다. 
let list3: Array<number> = [1, 2, 3]; // Generic array type. 꺽쇠가 Generic을 의미한다. 

// tuple : 고정된 요소수 만큼의 타입을 미리 선언후 배열을 표현. 사용할 일이 별로 없음. 
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ['hello', 10]; // OK
// Initialize it incorrectly
x = [10, 'hello']; // Error

console.log(x[0].substr(1)); // OK
console.log(x[1].substr(1)); // Error, 'number' does not have 'substr'

// enum : 열거형은 숫자값 집합에 이름을 지정한 것. 사용할 일이 있음. 
enum Color1 {Red, Green, Blue}; // 열거형이라는 것을 선언하고 있음. 
let c1: Color1 = Color1.Green;

console.log(c1); // 1

enum Color2 {Red = 1, Green, Blue}; // 초기값을 1로 주면 1,2,3 이순서대로 간다. 
let c2: Color2 = Color2.Green;

console.log(c2); // 2

enum Color3 {Red = 1, Green = 2, Blue = 4};
let c3: Color3 = Color3.Blue;

console.log(c3); // 4

// any : 타입 추론(type inference)할 수 없거나 타입 체크가 필요없는 변수는 any 타입으로 선언한다.
   우리는 any 타입을 사용하면 안된다. 이렇게 쓸꺼면 TypeScript 이유가 없다.
let notSure: any = 4;
notSure = 'maybe a string instead';
notSure = false; // okay, definitely a boolean

// void : 일반적으로 함수에서 반환값이 없을 경우 사용한다. return타입에 주로 사용하는데 주로 리턴값이 없을 떄 사용한다. 
function warnUser(): void {
  console.log("This is my warning message");
}

// never : 결코 발생하지 않는 값
function infiniteLoop(): never {
  while (true) {}
}
// 무한루프. 결코 함수를 빠져나오지 않는다. 

function error(message: string): never {
  throw new Error(message);
}
// 무조건 받은 메세지를 에러메세지 뜨게 만든다. 

```

## 2. 정적 타이핑 (Static Typing)

JavaScript는 동적 타입(dynamic typed) 언어 혹은 느슨한 타입(loosely typed) 언어이다. 이것은 변수의 타입 선언없이 값이 할당되는 과정에서 동적으로 타입이 추론**(타입추론 Type Inference)**될 것이라는 뜻이다.

TypeScript의 가장 독특한 특징은 **정적 타이핑**을 지원한다는 것이다.

만약 타입 선언을 생략하면 값이 할당되는 과정에서 동적으로 타입이 결정(타입추론: Type Inference)된다. 

```
let foo = 123; // let foo: number와 동치. 선언문이 있기 때문에 넘버타입으로 정해진 것.
foo = 'hi';    // error: Type '"hi"' is not assignable to type 'number'.
// 자바스크립트에서는 가능하지만 타입스크립트에서는 허용하지 않는다. 
```



정적 타이팅의 장점은 **코드 가독성, 예측성, 안정성의 향상**이라고 볼 수 있는데 이는 **대규모 프로젝트에 매우 적합하다.**

```
function add(x: number, y: number): number {
  return x + y;
}

console.log(add(10, 10)); // 20
console.log(add('10', '10'));
// error TS2345: Argument of type '"10"' is not assignable to parameter of type 'number'.
```



# 4. TypeScript - **Class**

TypeScript를 사용하면 모든 프로그래밍을 클래스화 해서 만들 가능성이 크다.

Angular는 모조리 다 class 이다.  

## 1. 클래스 정의 (Class Definition)

[ECMAScript 6 클래스](http://poiemaweb.com/es6-class#4-%EB%A9%A4%EB%B2%84-%EB%B3%80%EC%88%98)는 메소드만을 포함할 수 있다.

```
// person.js
class Person {
  constructor(name) {
    // 멤버 변수의 선언과 초기화
    this.name = name;
  }

  walk() {
    console.log(`${this.name} is walking.`);
  }
}
```

```
// person.ts
class Person {
  // 멤버 변수를 사전 선언하여야 한다.
  name: string; // 기본적으로 public이 된다. 

  constructor(name: string) {
    // 멤버 변수에 값을 할당
    this.name = name;
  }

  walk() {
    console.log(`${this.name} is walking.`);
  }
}

const person = new Foo('Lee');
person.walk(); // Lee is walking
```



## 2. 접근 제한자 (Access modifier)

Typescript의 경우, 접근 제한자를 생략한 멤버 변수와 메소드는 **암묵적으로 public이 선언**된다.

| 접근 가능성     | public | protected | private |
| --------------- | ------ | --------- | ------- |
| 클래스 내부     | ◯      | ◯         | ◯       |
| 자식 클래스     | ◯      | ◯         | ✕       |
| 클래스 인스턴스 | ◯      | ✕         | ✕       |

private 개인적인 것

protected 가족적인 것



```
class Bar extends Foo {
  constructor(x: string, y: string, z: string) {
    super(x, y, z);

    // public 접근 제한자는 자식 클래스에서 참조 가능하다.
    console.log(this.x);

    // protected 접근 제한자는 자식 클래스에서 참조 가능하다. 가족이니까. 
    console.log(this.y);

    // private 접근 제한자는 자식 클래스에서 참조할 수 없다.
    console.log(this.z); // error TS2341: Property 'z' is private and only accessible within class 'Foo'.
  }
}
```

**중요한 것은 왜 public, protected, private를 사용하는가?**

왜 공개할까? 외부에서 참조하고 사용해야하는 것들. 

굳이 외부에서 몰라도 되는 것. 아껴서 안보여주는 것이 아니라. 알 필요가 없으면 공개를 하지 않는다.

```
**중요**
class Foo {
  // 접근 제한자가 선언된 생성자 파라미터 x는 멤버 변수로 선언되고 초기화가 자동 수행된다.
  // public이 선언되었으므로 x는 클래스 외부에서도 참조가 가능하다.
  constructor(public x: string) { }
}

const foo = new Foo('Hello');
console.log(foo);   // Foo { x: 'Hello' }
console.log(foo.x); // Hello

class Bar {
  // 접근 제한자가 선언된 생성자 파라미터 x는 멤버 변수로 선언되고 초기화가 자동 수행된다
  // private이 선언되었으므로 x는 클래스 내부에서만 참조 가능하다
  constructor(private x: string) { }
}

const bar = new Bar('Hello');

console.log(bar); // Bar { x: 'Hello' }

// private이 선언된 bar.x는 클래스 내부에서만 참조 가능하다
console.log(bar.x); // Property 'x' is private and only accessible within class 'Bar'.
```

만일 생성자 파라미터에 접근 제한자를 선언하지 않으면 생성자 파라미터는 생성자 내부에서만 유효한 지역 변수가 되어 생성자 외부에서 참조가 불가능하게 된다.

```
class Foo {
  // x는 생성자 내부에서만 유효한 지역 변수이다.
  constructor(x: string) {
    console.log(x);
  }
}

const foo = new Foo('Hello');
console.log(foo); // Foo {}
```



## 4. readonly 키워드

Typescript는 `readonly` 키워드를 사용할 수 있다. readonly가 선언된 프로퍼티는 선언시 또는 생성자 내부에서만 값을 할당할 수 있다. 그 외의 경우에는 값을 할당할 수 없고 오직 읽기만 가능한 상태가 된다. 이를 이용하여 상수의 선언에 사용한다.

결국 const 키워드와 똑같다. 한 번만 선언하게 만들려고 사용함.

```
class Foo {
  private readonly MAX_LEN: number = 5;
  private readonly MSG: string;

  constructor() {
    this.MSG = 'hello';// 항상 내부에서는 멤버변수에 접근하려면 this를 사용해야 한다. 잊어버리지 말 것!
  }

  log() {
    // readonly가 선언된 프로퍼티는 재할당이 금지된다.
    this.MAX_LEN = 10; // Cannot assign to 'MAX_LEN' because it is a constant or a read-only property.
    this.MSG = 'Hi'; // Cannot assign to 'MSG' because it is a constant or a read-only property.

    console.log(`MAX_LEN: ${this.MAX_LEN}`); // MAX_LEN: 5
    console.log(`MSG: ${this.MSG}`); // MSG: hello
  }
}

new Foo().log();
```



## 5. static 키워드

```
class Foo {
  static instanceCounter = 0;
  constructor() {
    // 생성자가 호출될 때마다 카운터를 1씩 증가시킨다.
    Foo.instanceCounter++;
  }
}

var foo1 = new Foo();
var foo2 = new Foo();

console.log(Foo.instanceCounter);  // 2
console.log(foo2.instanceCounter); // error TS2339: Property 'instanceCounter' does not exist on type 'Foo'.
```



## 6. 추상 클래스 (Abstract class)

내가 관심이 있는 것을 부각시켜서 그리는 것? 

여기서 추상화란?  사람이라는 개념을 속성으로 나타내고 싶을 때 모든 것을 나열할 마음이 없고 내가 사람이라는 개념중에 중요하다고 생각하는 속성들만 뽑아서 관리한다. 

무조건 있어야 하는 메소드들을 넣어주는 틀을 만들어주고 협업을 할 때 사용한다. 이런 것들이 잘 되어있는 회사일 수록 기술력이  높다. 결국 코드로 강제 하는 것이다. 만약에 추상클래스에 들어있는 추상메소드가 자식 클래스에 없으면 에러가 난다. 상속되어지기 위해서 만든 클래스라 new를 사용하지 못한다. 

```
abstract class Animal {
  // 추상 메소드
  abstract makeSound(): void;
  // 일반 메소드
  move(): void {
    console.log('roaming the earth...');
  }
}

// new Animal();
// error TS2511: Cannot create an instance of the abstract class 'Animal'.

class Dog extends Animal {
  // 추상 클래스의 추상 메소드를 반드시 구현하여야 한다
  makeSound() {
    console.log('bowwow~~');
  }
}

const myDog = new Dog();
myDog.makeSound();
myDog.move();
```

**[인터페이스](http://poiemaweb.com/typescript-interface)는 모든 메소드가 추상 메소드이지만 추상 클래스는 추상 메소드와 구현이 되어 있는 일반 메소드를 포함할 수 있다.**



# 5. TypeScript - **Interface**

## 1. Introduction

인터페이스는 일반적으로 **타입 체크를 위해 사용되며 일반 변수, 함수, 클래스에 사용**할 수 있다.

ES6에서는 인터페이스가 없기 때문에 컴파일링하면 사라진다. 

## 2. 변수와 인터페이스

```
// 인터페이스의 정의
interface Todo {
  id: number;
  content: string;
  completed: boolean;
}

// 변수 todos의 타입으로 Todo 인터페이스를 선언하였다. 하나라도 오타가 나온다던지 타입이 다르다던지 하면 바로 에러. 실수를 원천봉쇄한다. 
let todos: Todo[];

// 변수 todos는 Todo 인터페이스를 준수하여야 한다.
todos = [
  { id: 1, content: 'typescript', completed: false }
];
```

결국 우리가 타입을 만드는 것이다. 여기서는 Todo 타입을 만들었다. 

```
// 인터페이스의 정의
interface Todo {
  id: number;
  content: string;
  completed: boolean;
}

// 파라미터 todo의 타입으로 Todo 인터페이스를 선언하였다.
function addTodo(todo: Todo) {
  console.log(todo.content);
}

// 파라미터 todo는 Todo 인터페이스를 준수하여야 한다.
const newTodo: Todo = { id: 1, content: 'typescript', completed: false };
addTodo(newTodo);
```



## 3. 함수와 인터페이스

사용빈도가 조금 떨어지긴 한다. 

```
// 함수 인터페이스의 정의
interface SquareFunc {
  (num: number): number;
  매개변수 선언부    리턴 선언부
}

// 함수 인테페이스를 구현하는 함수는 인터페이스를 준수하여야 한다.
const squareFunc: SquareFunc = function (num: number) {
  return num * num;
}

console.log(squareFunc(10)); // 100
```



## 4. 클래스와 인터페이스

```
// 인터페이스의 정의
interface ITodo {
  id: number;
  content: string;
  completed: boolean;
}

// Todo 클래스는 ITodo 인터페이스를 구현하여야 한다.
class Todo implements ITodo {
		   인터페이스를 구현한다. extends가 아닌 implemnents
  constructor (
    public id: number,
    public content: string,
    public completed: boolean
  ) { }
}

const todo = new Todo(1, 'Typescript', false);
// 여기서 todo의 type은 Todo type.

console.log(todo);
```

생성자 함수로 만드느냐 아니면 객체 리터럴로 만드느냐의 차이.



```
// 인터페이스의 정의
interface IPerson {
  name: string;
  sayHello(): void;
}

// 인터페이스를 구현하는 클래스는 인터페이스에서 정의한 멤버변수와 메소드를 반드시 구현하여야 한다.
class Person implements IPerson {
  // 인터페이스에서 정의한 멤버변수의 구현
  constructor(public name: string) {}

  // 인터페이스에서 정의한 메소드의 구현
  sayHello() {
    console.log(`Hello ${this.name}`);
  }
}

function greeter(person: IPerson): void {
  person.sayHello();
}

const me = new Person('Lee');
// 여기서 me는 Person 타입도 되고 IPerson 타입도 된다. 상속관계에 의해서 그렇게 된다. 
greeter(me); // Hello Lee
```



## 5. 덕 타이핑 (Duck typing)

주의해야 할 것은 인터페이스를 구현하였다는 것만이 타입 체크를 통과하는 유일한 방법은 아니다. 타입 체크에서 중요한 것은 값을 실제로 가지고 있는 것이다. 

```
interface IDuck { // 1
  quack(): void;
}

class MallardDuck implements IDuck { // 3
  quack() {
    console.log('Quack!');
  }
}

class RedheadDuck { // 4
  quack() {
    console.log('q~uack!');
  }
}
// IDuck으로 implements 하지 않았어도 같은 메소드를 가지고 있으므로 IDuck 타입으로 간주할 수 있다. 

function makeNoise(duck: IDuck): void { // 2
  duck.quack();
}

makeNoise(new MallardDuck()); // Quack!
makeNoise(new RedheadDuck()); // q~uack! // 5
```



```
interface IPerson {
  name: string;
}

function sayHello(person: IPerson): void {
  console.log(`Hello ${person.name}`);
}

const me = { name: 'Lee', age: 18 };
// 여기서도 결국 name을 가지고 있기 때문에 IPerson 타입으로 인정할 수 있다. 
sayHello(me); // Hello Lee
```



지금 이야기한 것들은 코드를 치면서 몸에 익혀야 한다. 문법을 잘 알고 있어야 한다. 



## 6. 선택적 프로퍼티 (Optional Property)

```
interface IUserInfo {
  username: string;
  password: string;
  age?    : number; // 선택적이기 때문에 안 넣어도 회원가입이 되는 경우 ?를 붙여준다. 이것이 선택적 프로퍼티.
  address?: string;
}

const userInfo: IUserInfo = {
  username: 'ungmo2@gmail.com',
  password: '123456'
}

console.log(userInfo);
```

코드를 이해하기 쉬워진다. 가독성이 높아진다. 



# 6. TypeScript - **Generic**

```
class Queue {
  protected data = []; // data: any[]

  push(item) {
    this.data.push(item);
  }

  pop() {
    return this.data.shift();
  }
}

const queue = new Queue();

queue.push(0);
queue.push('1'); // 의도하지 않은 실수!

console.log(queue.pop().toFixed()); // 0
console.log(queue.pop().toFixed()); // Runtime error
```



```
class Queue<T> {
  protected data = [];
  push(item: T) {
    this.data.push(item);
  }
  pop(): T {
    return this.data.shift();
  }
}

// number 전용 Queue
const numberQueue = new Queue<number>();

numberQueue.push(0);
// numberQueue.push('1'); // 의도하지 않은 실수를 사전 검출 가능
numberQueue.push(+'1');   // 실수를 사전 인지하고 수정할 수 있다

console.log(numberQueue.pop().toFixed()); // 0
console.log(numberQueue.pop().toFixed()); // 1
```

**제네릭은 선언 시점이 아니라 생성 시점에 타입을 명시하여 하나의 타입만이 아닌 다양한 타입을 사용할 수 있도록 하는 기법이다. 한번의 선언으로 다양한 타입에 재사용이 가능하다는 장점이 있다.**

**T는 제네릭을 선언할 때 관용적으로 사용되는 식별자로 <u>타입 파라미터(Type parameter)</u>라 한다.** T는 Type의 약자로 반드시 T를 사용하여야 하는 것은 아니다.

