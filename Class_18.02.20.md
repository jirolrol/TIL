### 5.3 Array.prototype.co#ncat(item…)

concat 메소드의 인수로 넘어온 값들(배열 또는 값)을 자신의 복사본에 요소로 추가하고 반환한다. 이때 **원본 배열은 변경되지 않는다.**

```
var a = ['a', 'b', 'c'];
var b = ['x', 'y', 'z'];

var c = a.concat(b);
console.log(c); // ['a', 'b', 'c', 'x', 'y', 'z']

// a를 대상으로 해서 b를 concat 한다. 

var d = a.concat('String');
console.log(d); // ['a', 'b', 'c', 'String']

var e = a.concat(b, true);
console.log(e); // ['a', 'b', 'c', 'x', 'y', 'z', true]

//타 언어는 여러가지 데이터 타입을 혼용할 수 없는데 자바스크립트는 혼용할 수 있다. 
  될 수 있으면 데이터 타입을 맞춰주는 것이 좋다. 
  
// 원본 배열은 변하지 않는다.
console.log(a); // [ 'a', 'b', 'c' ]

```



### 5.4 Array.prototype.join()

배열 요소 전체를 연결하여 생성한 문자열을 반환한다. 기본구분자는 ‘,’이다.

Array.prototype.join() 메소드는 `+` 연산자보다 빠르다. (적극적으로 사용 대상이다.)

```
str = arr.join([separator = ','])
```

```
var arr = ['a', 'b', 'c', 'd'];

var x = arr.join();
console.log(x);  // 'a,b,c,d';

var y = arr.join('');
console.log(y);  // 'abcd'

var z = arr.join(':');
console.log(z);  // 'a:b:c:d'
```



![array-method](/Users/mac/Desktop/array-method.png)

### 5.6 Array.prototype.push(item…)

```
var a = ['a', 'b', 'c'];
var b = ['x', 'y', 'z'];

// push는 원본 배열을 직접 변경하고 변경된 배열의 length를 반환한다.
var c = a.push(b);
console.log(a); // a --> ['a', 'b', 'c', ['x', 'y', 'z']]
console.log(c); // c --> 4;

// concat은 원본 배열을 직접 변경하지 않고 복사본을 반환한다.
console.log([1, 2].concat([3, 4])); // [ 1, 2, 3, 4 ]
```

### 5.5 Array.prototype.pop()



### 5.7 Array.prototype.reverse()

배열 요소의 순서를 반대로 변경한다. 이때 원본 배열이 변경된다. 반환값은 변경된 배열이다.

```
var a = ['a', 'b', 'c'];
var b = a.reverse();

// 원본 배열이 변경된다
console.log(a); // [ 'c', 'b', 'a' ]
console.log(b); // [ 'c', 'b', 'a' ]
```



### 5.8 Array.prototype.shift()

`shift`는 `push`와 함께 배열을 큐(FIFO: First In First Out)처럼 동작하게 한다. 배열에서 첫요소를 제거하고 제거한 요소를 반환한다. 만약 빈 배열일 경우 `undefined`를 반환한다.



### 5.9 Array.prototype.slice(start, end)

일부분을 끄집어 내온다. 어디서부터 어디까지 일부분인지 정보를 주어야 한다. 

원본 배열을 수정하지 않는다. 

```
var items = ['a', 'b', 'c'];

// items[0]부터 items[1] 이전(items[1] 미포함)까지 반환
var res1 = items.slice(0, 1);
console.log(res1);  // [ 'a' ]

// items[1]부터 items[2] 이전(items[2] 미포함)까지 반환
var res2 = items.slice(1, 2);
console.log(res2);  // [ 'b' ]

// items[1]부터 이후의 모든 요소 반환
var res3 = items.slice(1);
console.log(res3);  // [ 'b', 'c' ]

// 인자가 음수인 경우 배열의 끝에서 2개의 요소를 반환
var res4 = items.slice(-2);
console.log(res4);  // [ 'b', 'c' ]
// 이렇게는 가독성이 떨어지는 사용하지 말 것.

// 모든 요소를 반환 (= 복사본 생성) **
var res5 = items.slice();
console.log(res5);  // [ 'a', 'b', 'c' ]

// 원본은 변경되지 않는다.
console.log(items); // [ 'a', 'b', 'c' ]
```

유사배열을 배열로 만들 때도 사용한다.

var res5 = items.slice();
console.log(res5);  // [ 'a', 'b', 'c' ]



### 5.10 Array.prototype.splice(start, deleteCount, item…)

 배열에서 요소를 삭제할 때다.

```
var items = ['one', 'two', 'three', 'four'];

// items[1]부터 2개의 요소를 제거하고 제거된 요소를 배열로 반환
var res = items.splice(1, 2);

// 원본 배열이 변경된다.
console.log(items); // [ 'one', 'four' ]
// 제거한 요소가 배열로 반환된다.
console.log(res);   // [ 'two', 'three' ]
```

배열에서 요소를 제거하고 제거한 위치에 다른 요소를 추가한다.

```
var items = ['one', 'two', 'three', 'four'];

// items[1]부터 2개의 요소를 제거하고 그자리에 새로운 요소를 추가한다. 제거된 요소가 반환된다.
var res = items.splice(1, 2, 'x', 'y');

// 원본 배열이 변경된다.
console.log(items); // [ 'one', 'x', 'y', 'four' ]
// 제거한 요소가 배열로 반환된다.
console.log(res);   // [ 'two', 'three' ]
```

배열 중간에 새로운 요소를 추가할 때도 사용된다.

```
var items = ['one', 'two', 'three', 'four'];

// items[1]부터 0개의 요소를 제거하고 그자리(items[1])에 새로운 요소를 추가한다. 제거된 요소가 반환된다.
var res = items.splice(1, 0, 'x');

// 원본 배열이 변경된다.
console.log(items); // [ 'one', 'x', 'two', 'three', 'four' ]
// 제거한 요소가 배열로 반환된다.
console.log(res);   // [ ]
```

```
var items = ['one', 'four'];

// items[1]부터 0개의 요소를 제거하고 그자리(items[1])에 새로운 배열를 추가한다. 제거된 요소가 반환된다.
// items.splice(1, 0, ['two', 'three']); // [ 'one', [ 'two', 'three' ], 'four' ]
Array.prototype.splice.apply(items, [1, 0].concat(['two', 'three']));
// ES6
// items.splice(1, 0, ...['two', 'three']);

console.log(items); // [ 'one', 'two', 'three', 'four' ]
```

배열을 풀 수 없기 때문에 이런 것을 사용한다. 따라서 ES6에서 ...이란 문법을 만들었다. 



### 5.11 Array.prototype.sort(comparefunc)

```
var fruits = ['Banana', 'Orange', 'Apple', 'Mango'];

// ascending(오름차순)
fruits.sort();
console.log(fruits); // [ 'Apple', 'Banana', 'Mango', 'Orange' ]

// descending(내림차순)
fruits.reverse();
console.log(fruits); // [ 'Orange', 'Mango', 'Banana', 'Apple' ]

// sort한 다음에 reverse 한다. 

---------다음에 나오는 것은 공식처럼 이해할 것!

var points = [40, 100, 1, 5, 25, 10];

points.sort();
console.log(points); // [ 1, 10, 100, 25, 40, 5 ]

// Syntax : array.sort(compareFunction)

// 숫자 배열 오름차순 정렬
// compareFunction의 반환값이 0보다 작은 경우, a를 우선한다.
points.sort(function (a, b) { return a - b; });
console.log(points); // [ 1, 5, 10, 25, 40, 100 ]

// 숫자 배열에서 최소값 취득
console.log(points[0]); // 1

// 숫자 배열 내림차순 정렬
// compareFunction의 반환값이 0보다 큰 경우, b를 우선한다.
points.sort(function (a, b) { return b - a; });
console.log(points); // [ 100, 40, 25, 10, 5, 1 ]

// 숫자 배열에서 최대값 취득
console.log(points[0]); // 100
```



### 5.12 Array.prototype.forEach()

배열을 순회하며 배열의 각 요소에 대하여 인자로 주어진 콜백함수를 실행한다. 콜백함수의 매개변수를 통해 배열 **요소의 값, 요소 인덱스, 순회할 배열**을 전달 받을 수 있다. 반환값은 undefined이다.

forEach 메소드는 for 문과는 달리 break 문을 사용할 수 없다.(한 번 순회하면 끝까지 순회한다.)

순회! 각 요소를 순회하면서 콜백함수로 준 함수를 각 요소에 실행한다. 

이러한 것을 **고차함수** 라고 한다. 

```
var total = 0;
var testArray = [1, 3, 5, 7, 9];

// forEach 메소드는 원본 배열을 변경하지 않는다.
testArray.forEach(function (item, index, array) {
  console.log('[' + index + '] = ' + item);
  total += item;
});
// 무명함수 선언 

console.log(total); // 25
console.log(testArray); // [ 1, 3, 5, 7, 9 ]

---------------
testArray = [1, 2, 3, 4];

// 원본 배열을 변경하려면 콜백 함수의 3번째 인자를 사용한다.
testArray.forEach(function (item, index, array) {
  array[index] = Math.pow(item, 2);
});

// 매개변수 array는 결국 this 이다. 하지만 this는 window를 가르키기 때문에 쓰지 못한다. 
console.log(testArray); // [ 1, 4, 9, 16 ]

// forEach 메소드는 for 문과는 달리 break 문을 사용할 수 없다.
[1, 2, 3].forEach(function (item, index, array) {
  console.log('[' + index + '] = ' + item);
  if (item > 1) break; // SyntaxError: Illegal break statement
});
```



두번째 인자로 this를 전달할 수 있다. ** 중요 복습**

```
function Counter() {
  this.sum = 0;
  this.count = 0;
}

Counter.prototype.add = function (array) {
  // entry는 array의 배열 요소의 값
  array.forEach(function (entry) {
    this.sum += entry; // 2번째 인자 this를 전달하지 않으면 this === window
    this.count++;
  }, this);
};

var counter = new Counter();
counter.add([2, 5, 9]);
console.log(counter.count); // 3
console.log(counter.sum);   // 16
```



### 5.13 Array.prototype.map() 제일중요!!

배열을 순회하며 각 요소에 대하여 인자로 주어진 **콜백함수의 반환값(결과값)으로 새로운 배열을 생성하여 반환한다.** 

forEach()는 배열을 순회하며 요소 값을 참조하여 무언가를 하기 위한 함수이며 map()은 배열을 순회하며 요소 값을 다른 값으로 맵핑하기 위한 함수이다.



```
var numbers = [1, 4, 9];

// 배열을 순회하며 각 요소에 대하여 인자로 주어진 콜백함수를 실행. 반드시 return이 있어야 한다. 
   	return을 안주면 빈 배열이 나온다. []
var roots = numbers.map(function (item) {
  return Math.sqrt(item);
});

// 위 코드의 축약표현은 아래와 같다.
// var roots = numbers.map(Math.sqrt);

// map 메소드는 새로운 배열을 반환한다
console.log(roots);   // [ 1, 2, 3 ]
// map 메소드는 원본 배열은 변경하지 않는다
console.log(numbers); // [ 1, 4, 9 ]

-------------------------------------------------------------------------------
numbers = [1, 4, 9];

// 배열을 순회하며 각 요소에 대하여 인자로 주어진 콜백함수를 실행
roots = numbers.map(function (item) {
  return ++item;  // return하지 않으면 새로운 배열에 반영되지 않는다.
});

// map 메소드는 새로운 배열을 반환한다
console.log(roots);   // [ 2, 5, 10 ]
// map 메소드는 원본 배열은 변경하지 않는다
console.log(numbers); // [ 1, 4, 9 ]
```



### 5.14 Array.prototype.filter()

필터링 하는 것. 원본 배열에서 내가 원하는 것만 뽑아내는 것.

배열을 순회하면서 각각의 아이템에 대해서 콜백함수를 실행하지만  이것이 참인지 거짓인지를 얘기해줘야 한다. 

```
var result = [1, 2, 3, 4, 5].filter(function (item, index, array) {
  console.log('[' + index + '] = ' + item);
  return item % 2; // 홀수만을 필터링한다 (1은 true로 평가된다)
});

console.log(result); // [ 1, 3, 5 ]

// 결국 true인 것들만 만환된다. 
```

### 5.15 Array.prototype.reduce() 

많이 사용하진 않는다. 

결국 하나의 값을 만들어낸다. (배열 아님)

```
/*
previousValue: 이전 콜백의 반환값
currentValue : 배열 요소의 값
currentIndex : 인덱스
array        : 순회할 배열
*/
var result = [1, 2, 3, 4, 5].reduce(function (previousValue, currentValue, currentIndex, array) {
  console.log(previousValue + '+' + currentValue + '=' + (previousValue + currentValue));
  return previousValue + currentValue; // 결과는 다음 콜백의 첫번째 인자로 전달된다
});

console.log(result); // 15: 1~5까지의 합
/*
1: 1+2=3
2: 3+3=6
3: 6+4=10
4: 10+5=15
15
*/
```

### 5.16 Array.prototype.some()

배열 내 일부 요소가 콜백함수의 테스트를 통과하는지 확인하여 그 결과를 boolean으로 반환한다.

하나라도 통과하느냐?

```
// 배열 내 요소 중 10보다 큰 값이 1개 이상 존재하는지 확인
var res = [2, 5, 8, 1, 4].some(function (item) {
  return item > 10;
});
console.log(res); // false

res = [12, 5, 8, 1, 4].some(function (item) {
  return item > 10;
});
console.log(res); // true

// 배열 내 요소 중 특정 값이 1개 이상 존재하는지 확인
res = ['apple', 'banana', 'mango'].some(function (item) {
  return item === 'banana';
});
console.log(res); // true
```



### 5.17 Array.prototype.every()

배열 내 모든 요소가 콜백함수의 테스트를 통과하는지 확인하여 그 결과를 boolean으로 반환한다. 

모두 통과하느냐?

```
// 배열 내 모든 요소가 10보다 큰 값인지 확인
var res = [21, 15, 89, 1, 44].every(function (item) {
  return item > 10;
});
console.log(res); // false

res = [21, 15, 89, 100, 44].every(function (item) {
  return item > 10;
});
console.log(res); // true
```



### 5.18 Array.prototype.find()

ES6에서 새롭게 도입된 메소드로 <u>Internet Explorer에서는 지원하지 않는다.</u>

배열을 순회하며 각 요소에 대하여 인자로 주어진 **콜백함수를 실행하여 그 결과가 참인 첫번째 요소를 반환한다.**

```
var array = [
  { id: 1, name: 'Lee' },
  { id: 2, name: 'Kim' },
  { id: 2, name: 'Choi' },
  { id: 3, name: 'Park' }
];

// 콜백함수를 실행하여 그 결과가 참인 첫번째 요소를 반환한다.
var result = array.find(function (item) {
  return item.id === 2;
});

// filter는 콜백함수의 실행 결과가 true인 배열 요소의 값만을 추출한 새로운 배열을 반환한다.
result = array.filter(function (item) {
  return item.id === 2;
});
var array = [
  { id: 1, name: 'Lee' },
  { id: 2, name: 'Kim' },
  { id: 2, name: 'Choi' },
  { id: 3, name: 'Park' }
];

// 콜백함수를 실행하여 그 결과가 참인 첫번째 요소를 반환한다.
var result = array.find(function (item) {
  return item.id === 2;
});

// ES6
// const result = array.find(item => item.id === 2;);

console.log(result); // { id: 2, name: 'Kim' }

// filter는 콜백함수의 실행 결과가 true인 배열 요소의 값만을 추출한 새로운 배열을 반환한다.
result = array.filter(function (item) {
  return item.id === 2;
});

console.log(result); // [ { id: 2, name: 'Kim' },{ id: 2, name: 'Choi' } ]

console.log(result); // [ { id: 2, name: 'Kim' },{ id: 2, name: 'Choi' } ]
```





