18.02.01(목)

2. for문을 사용하여 0부터 10미만의 정수 중에서 홀수만을 작은 수부터 문자열로 출력하시오.

var res='';

for(var i = 0; i < 10; i++){
	if(i % 2){
    // console.log(i);
    res += i + '';
    }
}

console.log(res);


10. 트리 출력하기

다음을 참고하여 *(별)로 트리를 문자열로 완성하라.
개행문자(‘\n’)를 사용하여 개행한다. 완성된 문자열의 마지막은 개행문자(‘\n’)로 끝나도 관게없다.

// 높이(line)가 3일때 + 높이(line)가 5일때

*
**
***
*
**
***
****
*****

var star= '';

for (var i = 0; i < 3; i++) {
	//i = 0 별이 1개 
    //i = 1 별이 2개 
    //i = 2 별이 3개 
    for (var j = 0; j < i + 1; j++) {
    	star += '*';
    }	
    star += '\n';
}

for (var i = 0; i < 5; i++) {
	//i = 0 별이 1개 
    //i = 1 별이 2개 
    //i = 2 별이 3개 
    //i = 3 별이 4개 
    //i = 4 별이 5개 
    for (var j = 0; j < i + 1; j++) {
    	star += '*';
    }	
    star += '\n';
}

console.log(star);

console.log는 자동 개행!

---------------------------------------------------------------

## 4. 평가(Evaluating)

논리적 참, 거짓을 구별한 후 평가 결과에 따라 의사결정을 하는 것이 일반적이다.


### 4.1 암묵적 강제 형 변환 (Type coercion)

    var num = 2;
    var str = '1';

    // Bad
    console.log(num - str);

    // Good
    console.log(num - parseInt(str));

    parserInt:정수형으로 바꿔줘라
    
    ------------------------------------------
    var x = false;

    // 변수 x의 값을 숫자 타입으로 변환
    console.log('Number : ' + Number(x));  // 0
    x라는 것을 new를 안붙이고 함수를 생성하면 컨버트 된다. 
    
    // 변수 x의 값을 문자열 타입으로 변환
    console.log('String : ' + String(x));  // 'false'
    
    // 변수 x의 값을 불리언 타입으로 변환
    console.log('Boolean: ' + Boolean(x)); // false
    
    
"+"단항 연산자는 대부분의 값을 숫자형으로 변환할 수 있다.
뒤에 있는 값을 양수화 하기 때문에 숫자로 conversion한다. 


1 --> +1 양의 1 

앞에 -를 붙이면 음수화, + 붙이면 양수화.

    예외
    
    console.log(+undefined); // NaN
    console.log(+NaN);    // NaN
    
    
### 4.3 Data type conversion

// sting -> number
val = +val; // "+": 단항 연산자(unary operator)
// val = parseInt(val);

// number -> sting
val = val + '';
// val = val.toString();



### 4.4 Truthy & Falsy values

### 4.5 Checking equality

### 4.6 Checking existence


    / DOM에서 특정 요소를 취득
    var elem = document.getElementById('header');
    --->
    html 상에 'header' 라는 id를 가지고 있는 것을 가져온다. 
    만약 진짜 있다면 'header' 값이 들어가고 만약 없다면 'null'을 반환한다.
    
    if (elem) {
      // 요소가 존재함(요소 취득 성공) : 필요한 작업을 수행
      --->
      elem 안에 객체가 존재하면 'true'
    } else {
      // 요소가 존재하지 않음(요소 취득 실패) : 에러 처리
    }

# 5.7 Javascript Object

## 1. 객체(Object)란?

ex)
컵
명사적 성격을 가지고 있다.= data
색깔, 무게, 깊이 등등 

ex)
사람
동사적 성경을 가지고 있다.= method


var 사람 = { 
	name: 'Lee',
    age: 20,
    speak(동작): function(){} 
}


이 밖에도 무수한 property가 있지만 관심이 있는 속성만 표현한다. 이것을 '추상화'라고 한다. property가 동적인 것이 되면 이 값에는 함수가 들어가야 한다. 동사가 되는 property는 method 라고 한다. 
대부분의 function은 목적어(데이터)를 받는 술어의 역할을 한다. 

### 1.1 프로퍼티(Property)

- 프로퍼티 이름 : 빈 문자열을 포함하는 문자열과 숫자
- 프로퍼티 값 : undefined을 제외한 모든 값
문자열의 따옴표는 생략 가능한다. 


## 2. 객체 생성 방법

함수는 객체다. 객체는 함수일까? 아니다. 
둘 사이의 포함관계가 있다. 


객체를 만드는 방법에는 3가지가 있다.

### 2.1 객체 리터럴

### 2.2 Object() 생성자 함수

생성자 함수는 객체를 생성하는 것이다. 기본적으로 빈 객체를 만든다.
Object() 브라우져 안에 내장되어 있는 함수.
생성자 함수에는 앞에 'new'를 붙여줘야 한다.

객체 리터럴로 만드는 방식이 훨씬 더 쉽지만(문법적 설탕) 내부적으로는 Object()함수를 불러서 작업한다. 결국은 객체 리터럴 방식은 Object()함수를 쉽게 사용할 수 있는 축약법이다. prototype을 이해하려면 Object()함수를 알아야한다. 

### 2.3 생성자 함수

객체를 만들기 위해서 우리가 만드는 함수.

    var person1 = {
      name: 'Lee',
      gender: 'male',
      sayHello: function () {
        console.log('Hi! My name is ' + this.name);
      }
    };

    var person2 = {
      name: 'Kim',
      gender: 'female',
      sayHello: function () {
        console.log('Hi! My name is ' + this.name);
      }
    };
    
    값만 다르고 반복되는 상황. 컴퓨터에서는 반복을 싫어한다. 100사람을 만들려면         100개를 만들어야 한다. 데이터만 다른 객체를 생성해 낼 때.
    붕어빵 틀 같은 것만 있으면 찍어낼 수 있다.(factory pattern)
    즉, 객체 리터럴은 하나만 만들 때 사용하는 것이다. 
    
    // 생성자 함수
    
    function Person(name, gender) {
    this.name = name;
    this.gender = gender;
    this.sayHello = function(){
      console.log('Hi! My name is ' + this.name);
     };
  	}
    --->
    this 란 이 생성자 함수가 생성할 객체를 가르키는 포인터다.
    
    var person1 = new Person('Lee', 'male');
	var person2 = new Person('Kim', 'female');
    --->
    this는 person1, person2 가 된다. 
    
    
    this.sayHello = function(){
      console.log('Hi! My name is ' + this.name);
     };
        
    ----> 
    메모리상에 중복이 된다. 만약 person1, person2의 부모가 가지고 있으면
    이것은 상속되니까 해결이 된다. 이것이 우리가 prototype을 배우는 이유.
    
   
## 3. 객체 프로퍼티 접근

    var person = {
      'first-name': 'Ung-mo',
      'last-name': 'Lee',
      gender: 'male',
      1: 10,
      function: 1 // OK. 하지만 예약어는 사용하지 말아야 한다.
    };

프로퍼티에 접근하려면 person을 경유해야 한다.
따옴표 없이 first-name 이라고 쓰면 연산하려고 한다.
function라는 변수는 예약어라서 사용하지 않는 것이 좋다.

### 3.1 프로퍼티 이름

### 3.2 프로퍼티 값 읽기

- 마침표(.) 표기법
- 대괄호([]) 표기법

접근하는 방식 중 기본은 마침표로 접근하는 것이다. 

### 3.3 프로퍼티 값 갱신
### 3.4 프로퍼티 동적 생성

Object()프로퍼티로 생성한 빈 객체에 프로퍼티를 추가할 때 동적 생성을 한다.
동적으로 생성하는 것은 메모리의 Heap에서 관리한다.

### 3.5 프로퍼티 삭제

프로퍼티에서 delete를 사용할 일은 없다. 지울 수는 있지만 실무에서는 그냥 사용하지 않으면 된다. 

### 3.6 for-in 문
배우지 않음. ES6에서 for-of가 대신 나왔다.

## 4. Pass-by-reference

    // Pass-by-reference
    
    var foo = {
      val: 10
    }

    var bar = foo;
    console.log(foo.val, bar.val); // 10 10
    console.log(foo === bar);      // true

    bar.val = 20;
    console.log(foo.val, bar.val); // 20 20
    console.log(foo === bar);      // true
    
    side-effect(부수효과)
	한가지 값이 바뀌면 같은 포인트를 가르키는 변수도 바뀐다. 
    참조형으로 넘기지 않고 카피해서 넘기면 side-effect가 없다. 
    
    - side-effect가 없는 함수 순수함수(가급적 순수함수를 지양한다.)
	- side-effect가 있는 함수 비순수함수

## 6. 객체의 분류

 생성자 함수로 생성해낸 객체를 instance 라고 한다.
 객체인데 방금 바로 찍어낸 따끈따끈한 객체를 instance 라고 한다. 
 
 Host Object: 지금까지 배운 객체가 모두 Host Object
 Built-in Object: 이미 만들어 놓은 Object.
 
# 5.9 Javascript Function

유지보수가 힘들어지면 돈이 많이 나간다. 
효율적으로 만들기 위해 함수를 사용한다. 
코드해석을 잘 해야 한다.
오류가 발생되지 않게, 시간이 돈이다. 
가독성이 가장 중요하다. 

## 1. 함수 정의

- 함수선언식, 함수선언문(Function declaration)
- 함수표현식(Function expression)
- Function() 생성자 함수

결국은 다른 함수 생성 방식도 Function() 생성자 함수와 관련되어 있다. 

### 1.1 함수선언식(Function declaration)

    function square(number) {
     "방어코드가 들어가야 함. type이 어떤것이 올 지 모르니까!"
      return number * number;
    }

함수는 정의, 선언.

30개 이상의 매개변수를 전달해야 할 일이 있으면 그 때 객체를 사용한다. 
매개변수는 매개변수 자체가 선언한다는 뜻이다.
언어로 치면 매겨변수는 목적어다. 
return은 표현식의 값을 함수의 결과로 반환한다는 뜻이다. 
하나의 키워드이고 키워드는 명령을 가지고 있다. 

함수를 실제적으로 사용하려면 함수를 호출해야 한다. 함수를 호출하지 않으면 아무일도 일어나지 않는다. 반드시 호출 해야 한다.

	foo(10);
    
    이렇게 해서 튀어나온 값을 어디에다가 받아줘야 하니까 
    변수에 받아주면 된다.
    
    var result = foo(10);
    ---> 이것을 호출(call) 이라고 한다. 



### 1.2 함수표현식(Function expression)

일급 객체의 속성은 

- 무명의 리터럴로 표현이 가능한다. 
- 변수나 자료 구조(객체, 배열...)에 저장할 수 있다.
- 함수의 파라미터로 전달할 수 있다.
- 반환값으로 사용할 수 있다. 


     // 기명 함수표현식(named function expression)

     var foo = function multiply(a, b) {
        return a * b;
     };
      
     함수는 반드시 변수명으로 호출해야 한다. 
     

함수명이 변수명이 된다. 


    var square = function square(number) {
      return number * number;
    };
    
### 1.3 Function() 생성자 함수

    new Function(arg1, arg2, ... argN, functionBody)
    
    마지막에는 함수 몸체(코드블럭)가 와야한다.
    
    var square = new Function('number', 'return number *
    number');
    console.log(square(10)); // 100
    
## 2. 함수 호이스팅(Function Hoisting)

**2.4 변수 호이스팅(Variable Hoisting)**

    console.log(foo); // ① undefined
    
    var foo = 123;
    
    console.log(foo); // ② 123
    {
      var foo = 456;
    }
    
    console.log(foo); // ③ 456
    
    ①에서 참조되는 것 자체가 이상한거임. 
    실행컨텍스트라는걸 알아야 이해가 된다. 
    일단은 싹 훑어서 선언문(var)들을 찾는다. 
    선언문들을 위해서 특별한 동작을 하는데 바로 선언들을 VO에다가 적어놓는다.
    이것을 선언단계라고 한다. 
    그 다음 초기화 단계가 있는데 이는 메모리로 가서 타입을 모르기 때문에 
    undefined로 일단 공간을 마련해 놓는다. 
    그 다음이 할당이다. 
    선언-->초기화-->할당 (3단계)


변수호이스팅은 변수의 1,2 단계를 한번에 하고 3번을 런타임을 만났을 때 한다.
함수호이스팅은 1,2,3 단계를 한번에 한다. **함수 선언식만 된다.** 
함수 표현식은 함수가 변수에 담겨있기 때문에 변수 호이스팅을 한다. 

   
    //함수 선언식
   
    var res = square(5);

    function square(number) {
      return number * number;
    }
    
## 4. 매개변수(Parameter, 인자)

### 4.1 매개변수(parameter, 인자) vs 인수(argument)

**매개변수 === 인자 === parameter** 

    var foo = function (p1, p2) {
      console.log(p1, p2);
    };

    foo(1); // 1 undefined
    
    p1을 매개변수,인자,parameter 라고 한다.---> 변수니까!!
    foo(1)의 1을 인수,argument 라고 한다.
    직접적으로 매개변수에 할당되어질 값.
    
  
### 4.2 Call-by-value


    function foo(primitive) {
      primitive += 1;
      return primitive;
    }

    var x = 0;

    console.log(foo(x)); // 1
    console.log(x);      // 0

## 5. 반환값 (return value)
## 6. 함수 객체의 프로퍼티

proto
__prototype__

당연히 다른 의미!
__prototype__ 도 객체이므로 프로퍼티가 있다. 


### 6.1 arguments 프로퍼티

    function multiply(x, y) {
      console.log(arguments);
      return x * y;
    }

    multiply();        // {}
    multiply(1);       // { '0': 1 }
    multiply(1, 2);    // { '0': 1, '1': 2 }
    multiply(1, 2, 3); // { '0': 1, '1': 2, '2': 3 }
    
    3개를 주면 마지막 하나는 무시한다. 
    arguments? 는 어디서 나온거지?
    매개변수의 수에 맞지 않는 인수를 할당 할 수 있으니까 argument를 만들어
    관리한다.
    
    **중요함**
    
### 6.2 caller 프로퍼티

caller: 나를 호출한 사람.

### 6.3 length 프로퍼티

매개변수의 갯수를 이야기 한다. 그것을 참고하고 싶을 때는 이걸 사용한다. 
유사배열객체는 length가 있다. 
    
### 6.4 name 프로퍼티

### 6.5 __ proto __ 프로퍼티

__ proto __ :함수객체를 포함한 모든 객체가 가지고 있는 property. 자신의 부모 역할을 할 객체를 가르킨다. 모든 객체들은 부모가 있다. 

prototype: __ proto __ 의 부모 역할을 하는 객체다. 이것이 프로토타입 체이닝이다. 이 아이의 부모도 있기 마련인데 이것이 바로 Object.prototype이다. 

prototype property는 함수 객체만 가지고 있는 것이다. 함수는 생성자 함수로 사용할 가능성이 있기 때문이다. 생성자 함수가 자신이 만들어낼 객체의 부모 역할을 하는 객체를 알고 있다. 이를 prototype 객체라고 한다. 

---> 이것은 크롬관점에서 설명한 것.

prototype property,__ proto __  둘 다 동일한 값을 가르킨다. 근데 왜 2개로 나누어 놨을까?


### 6.6 prototype 프로퍼티




