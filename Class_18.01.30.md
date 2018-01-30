## 5.2 표현식 (Expression)

하나의 값으로 평가될 수 있는 하나의 식을 표현식이라고 한다. 

표현식은 구문이 될 수 있을까? 
구문은 표현식이 될 수 있을까?

    if (y >= 0) {  
      x = y;
    } else {
      x = -y;
    }

    (y >= 0)은 표현식

어떤 결과값을 어딘가에 저장시켜 놓는다면 유의미하다. 
어떤 결과값을 어딘가에 저장하지 않는다면 무의미하다.


## 5.3 변수 (Variable)

변수: 변하는 값
상수: 변하지 않는 값

프로그래밍에서 실수: 소수점이 있는 수 
프로그래밍에서 정수: 소수점이 없는 수
프로그래밍에서 =: 우항의 값을 좌항에 할당하라는 뜻.

변수는 위치(주소)를 기억하는 저장소이다. **메모리 상의 주소(address)** 의미한다. 

    var x; // 변수의 선언과 초기화
    x = 6; // 정수값의 할당
    
    6과 6.0은 매우 다르다. 컴퓨터에서 저장하는 방법이 다르다. 
    
## 5.4 값 (Value)


    JAVA 
    
    String str = "Hello World";
    < 1 > < 2 >      < 3 >
    
    str이라는 변수명은 문자열을 위한 변수다.
    그 생성된 str에 "Hello World"이라는 값을 담아라. 
    
    
    
JAVA는 정적(static) 타입 언어다. string 이라는 타입으로 묶어 버렸기 떄문에.
Javascript는 동적타입의 언어다. 



    리터럴(literal)
    문자열 값 == 문자열 literal 


    // literal : Number
    10.50
    1001

    // literal : String
    'Hello'
    "World"

    // literal : Object
    { name: 'Lee', gender: 'male' }

    // literal : Array
    [ 'Black', 'Gray', 'White' ];
    
    
자바스크립트는 7가지 데이터 타입을 제공한다. 

- 기본 자료형(pimitive data type)
  - Boolean
  - null
  - undefined
  - Number
  - String
  - Symbol (New in ECMAScript 6)

- Object

## 5.5 연산자 (Operator)

연산은 누가하나? CPU가 한다.

왜 0을 false 로 생각할까?
반도체: 전기를 흘릴수도 있고 안흘리수도 있는 도체와 부도체 모든 성격을 가진 것. 전기가 흐르면 1. 전기가 안흐르면 0. 그래서 컴퓨터는 0,1 밖에 모른다.

## 5.6 키워드 (keyword)

하나의 명령어.
var: 변수를 생성하라
function: 함수를 생성해라
while: 조건에 만족할 때 까지 반복해라

## 5.7 주석 (Comment)

이 코드는 이 코드를 읽는 사람한테 좀 어려울 것 같다고 생각되면 주석을 써줘야 한다. 하지만 이 코드를 읽는 사람의 실력에 맞게 써줘야 한다.
주석은 어디까지 써줘야하나? 주석은 없는게 좋다. 
즉 변수명, 함수명, 프로퍼티명 등을 작성할 때 의미를 잘 담아서 사용하는 것잊 좋다. 난해하게 써주면 안된다. 주어 + 목적어 + 서술어

# 4. Javascript Data type & Variable

1byte=8bit 

왜 하필 8bit 인가?

ASCII 코드: 알파벳, 특수기호, 숫자, 빈공간 를 표현할 수 있는 표현체계.
(총 95개) ASCII를 표현할 수 있는 데이터량은 2^8=256

**Javascript의 메모리 저방 방법**

	var x;

라고 선언하면 어떤 값이 들어올것이라고 예상하고 저장할 메모리를 준비해두어야 한다. x에 정수라는 타입이 들어올꺼라고 가정했을 때 OS에게 부탁해 8byte를 미리 메모리를 비워둔다. 

	x = 10;

x에 값을 할당해주면 메모리에 10이라고 써준다.

하지만 Javascript 동적타입 언어이기 때문에 어떤 데이터 타입이 들어올지 모르기 때문에 일단 undefined를 넣어 놓는다. 그 다음 할당문을 만나면 값을 보고 데이터 타입을 파악한 후 새롭게 자리를 다시 만들고 그 곳에 값을 넣는다.

동시에 저장한 값의 메모리의 위치를 알아야 한다. 1byte마다 번호가 매겨져 있는데 그것을 address 라고 한다. 매번 기록할 수 없으니까 식별자를 만들어 식별자가 address를 기억할 수 있게 만드는데 그것이 변수명이다. 따라서 변수명을 통해 address를 쉽게 찾을 수 있다. 

식별자(identifier) ---> 위치를 식별하는자

같은 변수에 재할당을 하면 다른 위치에 저장한다. 

## 1. Data Type (자료형)

왜 Data Type이 있어야 하나?
적당한 메모리 공간을 확보해 두어야 하니까! 


### 1.1 기본자료형 (Primitive Data Type)

- 기본 자료형 (primitive data type)
데이터 값을 변경할 수 없다.(immutable value) 
값으로 전달한다.(pass-by-value)

var a = 1;
var b = a;

이 때 a가 b에게 준 1 값은 a의 값을 복사해서 준 값. 즉 메모리 안에서는 다른 위치에 저장되어 있다. 


#### 1.1.1 Boolean

논리적인 요소를 나타내며 true와 false 두가지 값을 가질 수 있다. 비어있는 문자열과 null, undefined, 숫자 0은 false로 간주된다.

true false 는 논리값이라고 한다. 

	문자열

    'Hello' == ture
    
    " == false

#### 1.1.2 null

	num = 10;
    메모리상의 포인터를 가르키고 있다. 
    
	num = null;
    메모리상의 포인터를 지운다. 
    변수가 가르키고 있는 참조를 지운다. 
    나중에 가비지 컬렉션에서 지워진다. 
    하지만 언제 지워질지는 모른다. 
    
#### 1.1.3 undefined

선언만 하고 할당은 하지 않은 변수

#### 1.1.4 Number
- 정수 
- 실수
- +/- Infinity
- NaN (not-a-number)

#### 1.1.5 String

유니코드=2byte
문자열은 작은 따옴표(‘’) 또는 큰 따옴표(“”) 안에 텍스트를 넣어 생성한다.

    var answer = "It's alright";
        answer = "He is called 'Jhon'";
        answer = 'He is called "Jhon"';
        
    큰 따옴표로 시작되면 큰 따옴표로 닫고 
    작은 따옴표로 시작하면 작은 따옴표로 닫는다.

다른 언어에서는 string 을 기본 자료형이 아닌 참조형으로 구분하고 있다.

배열과 유사하게 행동한다. index를 활용해서 배열처럼 순회할 수 있다.
=**유사배열**

#### 1.1.6 Symbol

ES6에서 추가된 것.
객체는 키와 value 로 이루어져있는데 애플리케이션 전역에서 프로퍼티가 중복되지 않도록 하는 것

### 1.2 객체형 (Object type, 참조형)

- 객체형 (Object type)
데이터 값을 변경할 수 있다.(mutable)
참조로 전달한다.(pass-by-reference)


## 2. 변수 (Variable)

변수를 만들 때 규칙
1. 반드시 영문자, 특수문자는 쓸 수 없다.
2. underscore ( _ ), 또는 달러 기호($)로 시작하여야 한다. 이어지는 문자에는 숫자(0~9)도 사용할 수 있다.
3. 대/소문자를 구별할 수 있다. 문자는 “A” ~ “Z” (대문자)와 “a” ~ “z” (소문자)이다

 Snake Case 
 first_name

 Camel Case
 fisrtName
 **추천**
       
 ### 2.1 변수의 중복 선언
 
 Javascript는 변수의 중복 선언을 허용한다. 
 
    var x = 1;
    console.log(x); // 1

    // 변수의 중복 선언
    
    var x = 100;
    console.log(x); // 100
    
    
Javascript의 큰 취약점. 여러개의 자바스크립트 파일을 만들어서 html에서 로딩을 한다고 해도 여러개의 파일이 한 파일처럼 돌아가기 때문에 문제가 발생한다. ES6에서는 사용하면 안된다. 

### 2.2 변수 선언 시 var 키워드 생략 허용

var 키워드를 생략한 변수는 **전역변수**가 된다. 


### 2.3 동적 타이핑 (Dynamic Typing)

값을 할당할 때 동적으로 정해진다. 

    foo = null;
    console.log(typeof foo);  // object

    설계상 오류. 타입을 알고 싶으면 값을 보아야 한다. 
    
    
### 2.4 변수 호이스팅(Variable Hoisting)

변수 선언 이전에 창조할 수 있는 것.

    console.log(foo); // ① undefined
    var foo = 123;
    console.log(foo); // ② 123
    {
      var foo = 456; //지역에서 재할당이 이루어짐(중복선언)
    }
    console.log(foo); // ③ 456

{} 

다른언어에서는 코드 블럭을 하나의 지역으로 인신한다. 이 지역에서 선언한 변수를
**지역변수** 라고 한다. 
하지만 Javascript 에서는 함수에서만 지역변수로 인정한다. 
Javascript의 약점으로 본다.ES6로 넘어가면서 많이 해결되었다. 

# 5.5 Javascript Operator

## 1. 산술 연산자 (Arithmetic Operators)

    +	덧셈
    -	뺄셈
    *	곱셈
    /	나눗셈
    %	나머지(어떤것의 배수인지 알아볼 때 사용한다. 나누고 나머지 값.)
    ++	증가
    --	감소


++, -- 의 경우 뒤에 오면 할당이 먼저고 증가가 다음이다.

    ++i, i++, --i, i--
    
한쪽이라도 문자열이면 문자열 결합 연산자가 된다. 
숫자를 문자열로 casting 했다. 

    var str1 = '5' + 5;      // '55'
    var str2 = 5 + '5';      // '55'
    var str3 = 'Hello' + 5;  // 'Hello5'
    
   
## 2. 대입 연산자 (Assignment Operators)

    =	x = y	x = y
    +=	x += y	x = x + y
    -=	x -= y	x = x - y
    *=	x *= y	x = x * y
    /=	x /= y	x = x / y
    %=	x %= y	x = x % y
 
자신의 값과 새로운 값을 더해 재할당 하였다. 

    txt1 = 'What a very ';
    txt1 += 'nice day'; // What a very nice day 

## 3. 비교 연산자 (Comparison Operators)

 == 은 사용하지 않는 것이 좋다.
 === 은 값과 타입까지 비교한다.    
    
    var x = 5

    x == 5    // true
    x == '5'  // true
    x == 8    // false

    x === 5   // true
    x === '5' // false

 
**삼항연산자(ternary operator)**
    
    
    // 조건 ? 조건이 true일때 반환할 값 : 조건이 false일때 반환할 값
    var condition = true;
    var result = condition ? 'true' : 'false';
    console.log(result); // 'true'

  
    var result = condition ? 'true' : 'false';
    --->
    condition이 true 이면 'true' false 이면 'false'을 할당하라.
    위에서 condition은 true라고 할당했으므로 result는 true.
    
id의 길이가 INPUT_ID_MIN_LEN보다 작으면 에러 메시지를 출력한다.

  
    var id = 'lee';
    var INPUT_ID_MIN_LEN = 5;
    var errMsg = id.length < INPUT_ID_MIN_LEN ? '아이디는 5자리 이상으로
    입력하세요' : '성공';
    console.log(errMsg); // '아이디는 5자리 이상으로 입력하세요'
    --->
    id.length = 3.
    즉 INPUT_ID_MIN_LEN 보다 작으므로 true. 
    true 자리에 있는 '아이디는 5자리 이상으로 입력하세요'가 도출된다. 
    
    
## 4. 논리 연산자 (Logical Operators)

    ||	or
    &&	and
    !	not
    
    var n3 = !'Cat'; // false
    ---> 문자열은 true. 따라서 문자열이 아니니까 false. 
    
## 5. 단축 평가 (Short-Circuit Evaluation)


    true || anything	true
    false || anything	anything
    true && anything	anything
    false && anything	false
    
    
||(or)의 경우 앞에 true가 나오면 뒤는 안봐도 되니까 바로 true.
||(or)의 경우 앞에 false가 나오면 뒤를 꼭 보아야 하므로 anything.
&&(and)의 경우 앞에 true가 나오면 뒤를 꼭 확인해야해서 anything.
&&(and)의 경우 뒤에 false가 나오면 뒤를 확인할 필요가 없으므로 false.


	var foo = 'Cat' && 'Dog'  // t && t returns 'Dog'
    
    문자열이 있으면 true.
    && 이므로 뒤에 것도 봐야한다. 
    따라서 결과는 Dog.
    
    
대체 얘는 어디다가 쓰는 것일까??---> 방어코드에 쓰인다. 

    // example
    function foo (str) {
      str = str || '';
      // do somethig with str
      console.log(str.length);
    }
    
    
    str();
    str('hi');
    
   
    // example
    
    var obj = {
      // foo: 'hi',
      bar(property): 'hey'(값)
    };

    console.log('obj.foo is ' + obj.foo); // obj.foo is undefined

    if (obj && obj.foo) {
      // do somethig with obj.foo
      console.log('obj.foo is ' + obj.foo);
    }
    
    obj가 있고 그 obj에 foo라는 프로퍼티가 있으면 
    
객체
{property: 값}

객체에는 undefined를 제외하고 모두 들어올 수 있다. Javascript에서 함수는 객체이다. 

## 6. 타입 연산자 (Type Operators)

    typeof	
    
    피연산자의 데이터 타입(자료형)을 문자열로 반환한다. null과 배열의 경우
    object, 함수의 경우 function를 반환하는 것에 유의하여야 한다.
    
    instanceof 
    
    객체가 동일 객체형의 인스턴스이면 true를 반환한다.

## 7. !! 

not이 2개 있으면?
논리연산자가 있으면 true 인지 false 답해야하는 것.
!! 부정을 2개 붙여서 true, false 값을 알아내야 한다.

# 5.6 제어문

## 1. 블록 구문(Block statement)

함수는 재사용의 의미가 있다. 우리가 만들 코딩도 결국 함수를 만드는 것

    // 함수 선언문
    function foo() {
      var x = 1, y = 2;
      console.log(x + y);
    }
    foo();
    
   
## 2. 조건문(Conditional statement)

### 2.1 if 문

if문은 주어진 조건식을 평가하여 논리적 참, 거짓을 구별하는 구문.
else를 안써주면 true 일때만 코드를 실행한다.

    var hour = 20;
    var greeting;

    // if 문
    if (hour < 18) {
      greeting = 'Good day';
    }

    console.log(greeting);
    ---->이 상황에서는 greeting의 값이 undefined. 
         개발자의 의도가 알 수 없는 코드는 나쁜 코드.
    
    // if-else 문
    if (hour < 18) {
      greeting = 'Good day';
    } else {
      greeting = 'Good evening';
    }

    console.log(greeting);
    ---->이 상황에서는 'Good evening'
    
    
    // if-else if 문
    if (hour < 10) {
      greeting = 'Good morning';
    } else if (hour < 20) {
      greeting = 'Good day';
    } else {
      greeting = 'Good evening';
    }

    console.log(greeting);
    ----> 이 상황에서는 'Good evening'
    
 ### 2.2 switch 문
 
     var color = 'red';

    switch (color) {
      case 'yellow':
        console.log('yellow color');
        break;
      case 'red':
        console.log('red color');
        break;---> 브레이크를 걸어주지 않으면 밑에 까지 모두 실행된다.
      case 'blue':
        console.log('blue color');
        break;
      default:
        console.log('unknown color');--->뭐라도 값을 줘라.
        ----> 여기에는 브레이크를 써주지 않아도 된다. 어차피 마지막.
    }
    
    
## 3. 반복문(Loop)

for, while, do while(무한루프 돌릴 때 사용)

### 3.1 for 문

    for ([초기문]; [조건문]; [증감문]) {
      구문;
    }
    
    
  ![for문의 실행 순서](./for문의 실행순서.png)

### 3.2 while 문

    var n = 0;
    var x = 0;

    // n이 3보다 작을 때까지 계속 반복한다.
    while (n < 3) { // n: 0 1 2
      n++;          // n: 1 2 3
      x += n;       // x: 1 3 6
      console.log(x);
    }
    
    조건식이 참일 때 계속 실행된다.
    
### 3.3 do while 문

while문은 조건에 맞지 않으면 한 번도 실행되지 않을 수 있지만 일단 한 번은 실행한다. 

### 3.4 continue

    for (var i = 0; i < 5; i++) {
      if (i % 2 == 0) continue;
      console.log(i);
    }

    0~5의 정수 중에 홀수만 실행된다. 