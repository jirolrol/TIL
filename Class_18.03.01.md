18.03.01(목)

# 9. Promise

## 1. Promise란?

하나의 패턴이라고 생각하면 된다. 코딩을 할 때 이런식으로 하자는 암묵적 약속.



## 2. 콜백 패턴의 단점

비동기 호출할 때 문제가 있다. 크게 2가지 문제!

- 에러처리가 안된다. (치명적이다.)
- 콜백 헬



### 2.1 콜백 헬(Callback Hell)

만일 비동기 함수의 처리 결과를 가지고 다른 비동기 함수를 호출해야 하는 경우, 함수의 호출이 nesting이 되어 복잡도가 높아지는 현상이 발생하는데 이를 **Callback Hell**이라 한다.

### 2.2 에러 처리의 한계

자신을 부른 caller가 불분명하기 때문에 에러처리가 안된다. 

```
try {
  setTimeout(() => { throw 'Error!'; }, 1000);
} catch (e) {
  console.log('에러를 캐치하지 못한다..');
  console.log(e);
}
```

setTimeout이 에러를 낸 것이 아니다. 



## 3. Promise의 상태(State)

A에게 일을 부탁하고 나는 다른 일을 한다. 하지만 A가 부탁한 일을 성공할 수도 실패할 수도 있다. 성공하면 어떤 것을 주고 실패하면 어떤것을 주기로 되어있는게 Promise.

Promise는 비동기 처리가 성공(fulfilled)하였는지 또는 실패(rejected)하였는지 등의 상태(state) 정보를 갖는다.

| 상태          | 의미                                       | 구현                                               |
| ------------- | ------------------------------------------ | -------------------------------------------------- |
| pending       | 비동기 처리가 아직 수행되지 않은 상태      | resolve 또는 reject 함수가 아직 호출되지 않은 상태 |
| **fulfilled** | 비동기 처리가 수행된 상태 (성공)           | resolve 함수가 호출된 상태                         |
| **rejected**  | 비동기 처리가 수행된 상태 (실패)           | reject 함수가 호출된 상태                          |
| settled       | 비동기 처리가 수행된 상태 (성공 또는 실패) | resolve 또는 reject 함수가 호출된 상태             |

## 4. Promise의 생성

Promise 생성자 함수로 객체를 생성하는 것을 의미한다. 

```
var promise = new Promise((resolve, reject) => {
  // 비동기 작업을 수행한다.

  if (/* 비동기 작업 수행 성공 */) {
    resolve('resolved!');
  }
  else { /* 비동기 작업 수행 실패 */
    reject(Error('rejected!'));
  }
});
```

여기서 인자로 들어간 resolve 도 reject도 모두 함수. 



## 5. Promise 후속 처리 함수 then, catch

```
// 비동기 함수
function asyncFunc(param) {
  // Promise 객체 선언과 반환
  return new Promise((resolve, reject) => {
    // 비동기 함수
    setTimeout(() => (param ? resolve('resolved!') : reject('rejected!')), 1000);
  });
}
```



# 8. Module

## 1. Introduction

자바스크립트의 태생적인 한계.

기본적으로 웹사이트에서 필요한 폼필드에 대한 검증에 주로 사용되었다.

대부분이 브라우저에서는 자바스크립트의 모듈 기능을 지원하지 않고 있다.

[CommonJS](http://www.commonjs.org/)와 [AMD(Asynchronous Module Definition)](https://github.com/amdjs/amdjs-api/wiki/AMD)—>이것은 스펙의 이름



현재 브라우저에서는 모듈을 지원하지 않으나 표준 스펙에는 들어있다. 

바벨이나 웹펙의 도움을 받아서 우리가 구현할 수는 있다.



모듈이란? 

레고블럭을 연상하면 좋다. 

프로그램을 만들 때 부품화 해서 만들고 싶다는 열망이 있다. 결국 그 부품들이 모여서 어떤 것을 만들어 내야 하는데 이상과는 좀 다른 점이 있다. 레고처럼 딱딱 끼워지지 않는다. 

모듈은 일반적으로 파일단위로 구분된다.

Node.js는 많은 부품들이 제공되어져서 굉장히 적은 코드로 쉽게 서버사이드 코딩이 가능하다.

npm이란 큰 서버에 자신들이 만든 오픈소스들을 버전들로 올려 놓는다.

우리가 npm을 통해서 다운로드 한다고 생각하면 된다. 

ex) npm install axios 

이런 기능들이 구현되려면 모듈이 있어야 한다. 

C언어는 #include, Java는 import 등 대부분의 언어는 모듈 기능을 가지고 있다. 하지만 Javascript는 없다. 



## 2. export & import

a 파일과 b파일이 있다면 a 파일은 b 파일을 볼 수없고 b 파일은 a 파일을 볼 수 없다. 

export를 해주면 export 해준 부분에 한해서만 볼 수 있다. 

```
// lib.js
const pi = Math.PI;

function square(x) {
  return x * x;
}

class Person {
  constructor(name) {
    this.name = name;
  }
}

export { pi, square, Person };
// 전체를 하나의 객체로 묶어서 export하겠다는 뜻. 
```

```
// main.js
import * as lib from './lib';
// './lib' 모듈의 경로.

console.log(lib.pi);         // 3.141592653589793
console.log(lib.square(10)); // 100
console.log(new lib.Person('Lee')); // Person { name: 'Lee' }

```

각각의 이름을 지정하지 않고 하나의 이름으로 한꺼번에 import할 수도 있다. 이때 import되는 항목은 as 뒤에 지정한 객체의 프로퍼티가 된다.

```
// main.js
import * as lib from './lib';
// 여기서 lib는 객체라고 생각하면 된다.

console.log(lib.pi);         // 3.141592653589793
console.log(lib.square(10)); // 100
console.log(new lib.Person('Lee')); // Person { name: 'Lee' }
```

모듈에서 하나만을 export하는 경우, default 키워드를 사용할 수 있다. default를 사용하는 경우, var, let, const는 사용할 수 없다.

```
// lib.js
function (x) {
  return x * x;
}

export default;
// 무기명 함수라 이름이 없어도 된다. 그냥 default라고 쓰면 된다.
```

default 키워드와 함께 export한 모듈은 {} 없이 임의의 이름으로 import한다.

```
// main.js
import square from './lib';

console.log(square(3)); // 9
```



# 15. Babel + Webpack

Babel은 **트랜스파일러(Transpiler)**로서 ES6를 ES5 이하의 버전으로 트랜스파일링한다.

- npm install babel-cli --save-dev

  --save-dave란 개발할 때만 필요한 패키지라는 뜻.  따로 관리한다는 뜻. 

- node_modules는 npm을 이용해서 다운받은 모든 모듈들이 다 이 폴더로 들어간다. 이 폴더 안을 보면 굉장히 많은 것들이 있는데 내가 사용하고자 하는 모듈이 필요로하는 수많은 모듈들도 함께 다운된다. 



```
// node.js에서 돌고 있음.

const path = require('path');

module.exports = {
  entry: {
    entry: './src/js/entry.js'
  }, 
  // entry point: 진입점. 가장 먼저 실행되는 것.
     './src/js/entry.js'이름으로 가장 먼저 실행하라. 
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist/js')
  },
  / /filename: 산출물에 대한 설정. 그 파일에 대한 이름을 지정해 주는 것.
  	path: 이 파일을 어디에다 떨궈줄까 라는걸 정해주는 것. 
  module: {
    rules: [{
      test: /\.js$/,
  // 모든 js 파이를 가지고 밑에 써놓은 작업을 실행시켜라. 
      include: [
        path.resolve(__dirname, 'src/js')
      ],
      exclude: /node_modules/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['env']
        }
      }
    }]
  },
  devtool: 'source-map', // source-map 이라는 것도 만들어 달라는 뜻. 뭉치기 전 정보를 보여준다. 
  mode: 'development' // Webpack V4에서 추가
};
```

