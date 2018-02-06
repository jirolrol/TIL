# 5.18 Javascript Number

prototype객체가 있는 이유.

상속을 흉내네기 위함이다.
공유를 위함!

다 똑같은 메소드 이지만 호출 방법이 다르다.

일반 메소드는 생성자 함수의 this에 달려있다. 실체는 생성될 객체 내에 있다. 

프로토타입 메소드는 Number.prototype.toFixed()로 정의된다. 

function Person(name){
	var bar = function(){}
    this.getName = function(){}
    this.name = name;

}

1. new로 새로운 객체를 만들려고 하는 순간 빈 객체를 만들고 this는 윈도우를 가르킨다.

2. this가 새로운 객체를 가르킨다.
3. 리턴한다. 


static method
인스턴스를 생성하지 않아도 호출할 수 있다. 
왜 만들까?
인스턴스의 데이터와 무관한 것들을 static method로 만든다.

    var num = 1.5;
    console.log(num.toFixed()); // 2

toFixed를 함수로 만들었다면 1.5를 인자로 받을 수 밖에 없다. 위에서는 1.5를 직접 컨트롤 하게 만들 수 있다. 


## 1. Number Constructor

	new Number(value);
    
    var x = new Number(123);
    var y = new Number('123');
    var z = new Number('str');

    console.log(x); // 123
    console.log(y); // 123
    console.log(z); // NaN


## 2. Number Property

### 2.1 Number.EPSILON

생성될 인스턴스들이 모두 가지고 있을 필요가 없다. 늘 상수를 보여주기 때문에. 만약 프로토타입 메소드로 가져다 두려면 항상 새로운 객체를 생성해야 하기 때문에 불합리하다. 

어떤 임의의 수보다 큰 수가 있다. 큰 수에서 임의의 수를 뺀  수가 EPSILON. 다음 단계의 수로 넘어가기 위한 최소한의 수. 

    console.log(0.1 + 0.2);        
    // 0.30000000000000004
    
    console.log(0.1 + 0.2 == 0.3); // false!!!

    function isEqual(a, b){
    
      // Math.abs는 절댓값을 반환한다.
      // 즉 a와 b의 차이가 JavaScript에서 표현할 수 있는
      가장 작은 수인 Number.EPSILON보다 작으면 같은 수로 
      인정할 수 있다.
      
      return Math.abs(a - b) < Number.EPSILON;
      --->0.00000000000000004 < EPSILON 과 비교해서
      작다고 하면 true로 인정. abs는 절대값으로 바꿔준다.
    }

    console.log(isEqual(0.1 + 0.2, 0.3));
    
### 2.2 Number.MAX_VALUE

숫자는 8byte. 


### 2.4 Number.POSITIVE_INFINITY
상수

### 2.5 Number.NEGATIVE_INFINITY
상수

### 2.6 Number.NaN
window.NaN과 Number.NaN은 같은 것. 
같은 것을 가르키고 있다. 

**프로그램에서 상수는 모두 대문자로 쓴다. 스네티크 케이스를 사용한다.**

## 3. Number Method

### 3.1 Number.isFinite()

유한한가? 라고 물어보는 것. 
전역 메소드에 있는 isFinite()는 argument 값을 형변환하지만 Number.isFinite()는 하지 않는다. 

### 3.2 Number.isInteger()

매개변수에 전달된 값이 정수(Integer)인지 검사하여 그 결과를 Boolean으로 반환한다.

### 3.3 Number.isNaN()

NaN 아니면 다 false!

### 3.4 Number.isSafeInteger()

안전한 정수인지? 안전하다는건?

숫자가 한계 범위안에 있는 숫자이냐고 물어보는 것.
안전한 정수값은 (253 - 1)와 -(253 - 1) 사이의 정수값이다. 

### 3.5 Number.prototype.toExponential()

1234 = 1.234e+3
e+3 == 10의 3승이라는 뜻.

    var numObj = 77.1234;

    console.log(numObj.toExponential());  
    // logs 7.71234e+1
    console.log(numObj.toExponential(4)); 
    // logs 7.7123e+1
    --->소수점 뒷자리를 4개 확보라는 뜻 
    console.log(numObj.toExponential(2)); 
    // logs 7.71e+1
    console.log(77.1234.toExponential()); 
    // logs 7.71234e+1
    console.log(77.toExponential());     
    // SyntaxError: Invalid or unexpected token
    console.log(77 .toExponential());     
    // logs 7.7e+1
    
### 3.6 Number.prototype.toFixed() **중요**

매개변수로 지정된 소숫점자리를 반올림하여 **문자열**로 반환한다.


    var numObj = 12345.6789;

    // 소숫점 이하 반올림
    console.log(numObj.toFixed());  
    // '12346'
    
    // 소숫점 이하 1자리수 유효, 나머지 반올림
    console.log(numObj.toFixed(1)); 
    // '12345.7'
    
    // 소숫점 이하 2자리수 유효, 나머지 반올림
    console.log(numObj.toFixed(2)); 
    // '12345.68'
    
    // 소숫점 이하 3자리수 유효, 나머지 반올림
    console.log(numObj.toFixed(3));  
    // '12345.679'
    
    // 소숫점 이하 6자리수 유효, 나머지 반올림
    console.log(numObj.toFixed(6));  
    // '12345.678900'
    
### 3.7 Number.prototype.toPrecision()


    var numObj = 15345.6789;

    // 전체자리수 유효
    console.log(numObj.toPrecision()); 
    // '12345.6789'

    // 전체 1자리수 유효, 나머지 반올림
    console.log(numObj.toPrecision(1)); 
    // '2e+4'
    -->5를 반올림하고 나머지를 지수 표기법으로 바꾼다.

    // 전체 2자리수 유효, 나머지 반올림
    console.log(numObj.toPrecision(2)); 
    // '1.5e+4'

    // 전체 3자리수 유효, 나머지 반올림
    console.log(numObj.toPrecision(3)); 
    // '1.53e+4'

    // 전체 6자리수 유효, 나머지 반올림
    console.log(numObj.toPrecision(6));
    // '12345.7'
    
    
### 3.8 Number.prototype.toString()

Num---> String 으로 바꾸는 방법

- var x = 1;
  x + ''
  
- x.toString()

- Stirng(x)--> 비추천

### 3.9 Number.prototype.valueOf()

Number 객체의 기본자료형 값(primitive value)을 반환한다.

# 5.19 Javascript Math

인스턴스가 필요 없다. 모두 static!
생성자가 없다. 

## 1. Math Property

### 1.1 Math.PI

PI 값(π ≈ 3.141592653589793)을 반환한다.

### 2.1 Math.abs()

반드시 0 또는 양수이어야하는 절댓값(absolute value)을 반환한다.
형변환을 한다.

### 2.2 Math.round()

숫자를 가장 인접한 정수로 올림/내림한다.

    var x;

    // Returns the value 20
    x = Math.round(20.49);

    // Returns the value 21
    x = Math.round(20.5);

    // Returns the value -20
    x = Math.round(-20.5);

    // Returns the value -21
    x = Math.round(-20.51);
    
    인자로 준다.
    
### 2.3 Math.sqrt()

양의 제곱근을 반환한다. 

	Math.sqrt(9); // 3
    
### 2.4 Math.ceil()

지정된 숫자를 자신보다 큰, 가장 가까운 정수로 올림한다.

	Math.ceil(1.4); // 2
    
### 2.5 Math.floor()

지정된 숫자를 자신보다 작은, 가장 가까운 정수로 내림한다. 즉 소숫점 이하의 값을 제거한 정수를 취득한다.

    Math.floor(1.9); // 1
    Math.floor(9.1); // 9

### 2.6 Math.random()

0과 1 사이의 임의의 숫자를 반환한다. 이때 0은 포함되지만 1은 포함되지 않는다.

    console.log(Math.random()); 
    // 0 ~ 1 미만의 소수 (0.8208720231391746)

    // 랜덤 정수 취득
    var randomNum = Math.floor((Math.random() * 10) + 1);
    // 1 ~ 10의 정수
    console.log(randomNum);
    
### 2.7 Math.pow()

첫번째 인수를 밑(base), 두번째 인수를 지수(exponent)로하여 거듭제곱을 반환한다.

### 2.8 Math.max() **중요**

인수 중 가장 큰 수를 반환한다.

    Math.max(1, 2, 3) ;  // 3

    var arr = [1, 2, 3];
    var max = Math.max.apply(null, arr); // 3
    ---> apply를 사용한다. apply는 max를 호출하는 것. Math의 this를
    null로 써라. 어차피 static이라 this를 보지 않는다. 

    // ES6
    var max = Math.max(...arr); // 3
    
### 2.9 Math.min()

인수 중 가장 작은 수를 반환한다.
Math.max()와 같다. 


# 5.22 Javascript RegExp

## 1. 정규표현식(Regular Expression)

문자열에서 특정 내용을 찾거나 대체 또는 발췌하는데 사용한다.

    var tel = '0101234567팔';

    var myRegExp = /^[0-9]+$/;
    
    ^: 첫문자,
    +: 이규칙이 계속 이어진다.
    $: 끝
    첫 문자가 0~9의 값을 갖고 

    console.log(myRegExp.test(tel)); // false
    
### 1.1 플래그

i	Ignore Case	대소문자를 구별하지 않고 검색한다.
g	Global	문자열 내의 모든 패턴을 검색한다.
m	Multi Line	문자열의 행이 바뀌더라도 검색을 계속한다.


플래그는 옵션이므로 선택적으로 사용한다.플래그를 사용하지 않은 경우 문자열 내 검색 매칭 대상이 1개 이상이더라도 첫번째 매칭한 대상만을 검색하고 종료한다.

    var targetStr = 'Is this all there is?';
    var regexr = /is/;

    console.log(targetStr.match(regexr)); 
    // [ 'is', index: 5, input: 'Is this all there is?' ]

    regexr = /is/ig;

    console.log(targetStr.match(regexr)); 
    // [ 'Is', 'is', 'is' ]
    
### 1.2 패턴

    var targetStr = 'AA BB Aa Bb';
    // 임의의 문자 3개
    var regexr = /.../;

    //AA(space)


    var targetStr = 'AA BB Aa Bb';
    // 임의의 한문자를 반복 검색
    
    var regexr = /./g;
    console.log(targetStr.match(regexr));
    // [ 'A', 'A', ' ', 'B', 'B', ' ', 'A', 'a', ' ', 'B', 
    'b' ]
    
    
# 5.23 Javascript Array

html을 받으면 화면이 깜빡 거리게 되므로 html의 일부분만 받아서 갈아 끼우면 깜빡이지 않는다. html을 만들 수 있는 최소한의 데이터만 전해주면 된다. 그것이 최신 방법. 데이터를 많이 사용하지 않고 서버에서 하는 일이 적어진다. 

어떤 데이터 포멧으로 받아야 하나? JSON(더글라스)


ASCCI 코드가 늘 왔다갔다 한다.

## 1. 배열의 생성

### 1.1 배열 리터럴

개 이상의 값을 쉼표로 구분하여 대괄호([])로 묶는다.

index= 배열의 요소 
순회할 수 있다. 순서가 보장이 된다. length가 있다.
프로퍼티 없이 값만 있는데 순서에 의미가 있다는 소리.

Array.prototype.filter() Array.prototype.reduce()
== 고차함수

## 2. 배열 요소의 추가와 삭제

### 2.1 배열 요소의 추가

    var arr = [];
    console.log(arr[0]); // undefined

    arr[0] = 'one';
    arr[3] = 'three';
    arr[7] = 'seven';

    console.log(arr); // ["one", undefined × 2, "three", 
    undefined × 3, "seven"]
    
### 2.2 배열 요소의 삭제

## 3. 배열 요소의 열거

 배열 역시 객체이므로 for in 문을 사용할 수 있다

그러나 배열은 객체이기 때문에 프로퍼티를 가질 수 있다. for in 문을 사용하면 불필요한 프로퍼티까지 출력될 수 있고 요소들의 순서를 보장하지 않으므로 배열을 열거하는데 적합하지 않다.

## 4. Array Property

### 4.1 Array.length

length 프로퍼티는 요소의 갯수(배열의 길이)를 나타낸다.

## 5. Array Method

### 5.1 Array.isArray()

인자로 전달한 것이 배열인지 아닌지 구분한다. 

### 5.2 Array.prototype.indexOf()

    var arr = [1, 2, 2, 3];
    arr.indexOf(2); // 1
    arr.indexOf(4); // -1

### 5.3 Array.prototype.concat(item…)

요소를 뒤에 넣는 방법
push(제일 느림)
concat(원본을 건드리지 않는다.)
index-1 

### 5.4 Array.prototype.join()

    var arr = ['a', 'b', 'c', 'd'];

    var x = arr.join();
    console.log(x);  // 'a,b,c,d';

    var y = arr.join('');
    console.log(y);  // 'abcd'

    var z = arr.join(':');
    console.log(z);  // 'a:b:c:d'