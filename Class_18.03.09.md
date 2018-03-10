2018.03.09(금)

21,25,26  안할 예정이었으나 스케줄상 하루 남아서 21,25 할 수도.

원리를 깨우치려고 하면 안되고 프레임워크, 라이브라리는 어떻게 사용하면 되는지 알면 된다. 

Angular로 내가 만들고 싶은 걸 어떻게 만들어야 하는지 알아야 한다. 

closure, this, block level 은 신경쓸 일이 없다. Javascript 보다 쉬워보일 수 있음. 

리엑트, 뷰는 라이브러리로 취급. 뷰를 어떻게 효율적으로 만들것인가 하는데 중점.

앵귤러는 프레임워크. 



# 1. Angular **Basics**

## 1. Angular 소개

결국 Angular 는 HTML이 자바스크립트이다. 

로직이 네이티브돔을 직접 보지 않는다. 

우리가 todos만 변화시키면 변화를 스스로 감지하고 변화된 것만 바꿔준다. 



템플릿 문법을 잘 배워야 한다!

- 데이터 바인딩

- 이벤트 바인딩

  ​

[Angular](https://angular.io/)는 SPA(Single Page Application) 개발을 위한 구글의 오픈소스 자바스크립트 프레임워크이다.

SPA는 웹환경임에도 불구하고  애플리케이션처럼 보이고 싶은 열망을 담은 방법론이다. 

V3도 SPA. 하나의 페이지로 만들어진 애플리케이션. index.html을 한 번 호출하면 모든 리소스가 한 번에 다운되고 이후에는 필요한 데이터베이스만 서버에서 가져오고 클라이언트 쪽에서 가져온 데이터베이스로 일부만 갱신한다. 

화면이동이 생기기 시작하면 골치가 아파진다. Ajax 통신을 통해 호출하면 url이 바뀌지 않음. url이 바뀌어야 화면이  바뀌는 것. 모든 애플리케이션의 화면이 100개라고 해도 하나의 url인것이다. 그럼 어떨까? 99번째 화면을 즐겨찾기 하고싶은데 할 수 없다. 원하는 화변을 링크로도 보내줄 수 없다. url은 한 페이지당 유일한 하나의 url을 갖지만 Ajax는 하나의 url만 갖는다. 

이 말인 즉슥 첫 화면만 검색되어진다. (SEO 문제) 업무용이라면 첫 페이지만 검색되어도 되지만 아닌 경우에는 항상 걸림돌이 된다. 앵귤러 같은 경우에는 이것을 해결해 놓았다. 데이터 베이스에 접근할 때 액시오스와 유사한 라이브러리 같은 것을 내포하고 있다. 언어적 암묵적인 강제성을 지니고 있다. 이런 패턴은 이렇게 하라고 규칙을 다 정해놓은 상태이다. 유일한 하나의 패스만 주어지기 때문의 코딩의 세상에선 더 편하다. 그 규칙을 이해하고 어떻게 활용하면 되는지 아는 것이 앵귤러(프레임워크)를 공부하는 방법.

앵귤러도 의존 모듈을 사용하는데 1000개 정도를 사용한다. npm install 하면 1000번 해야한다는 뜻. 

모바일 애플리케이션을 만들 때는 아이오닉이라는 것을 사용한다. 

데스크탑 애플리케이션을 만들 때는 일렉트론을 사용한다. 

처음 나왔을 떄는 성능이슈가 있었고 너무 어려웠다. (AngularJS 1.0)  이쯤에 리액트가 등장하고 많은 사람들이 갈아 탐. 여기에 위협을 느낀 구글이 완전히 다른 것을 만들었다. 이전 문법을 완전히 버리고 Angular 2를 만들어냄. 하지만 버전업이 미친듯이 되어서 결국에는 리액트를 선택했음.  하지만 이제는 쓸만하다. 안정된 상태.

AngularJS도 여전히 살아있음. 우리가 배우는 것과 완전히 다른 것. 

디자이너들이 쉽게 접근할 수 있는 프레임워크를 만들고자 이것을 개발했다. --->말도 안되는...



## 2. Angular와 AngulaJS의 차이점

몰라도 됨. maybe interview?

- 모든 것 들이 component 이다. 이것을 CBD라고 한다.
- 뷰가 바뀌면 자바스크립트가 바뀌는 것을 답습 했었다. 
- two-way binding 때문에 성능이 떨어졌었다. 
- Decorator를 지원한다. (ES7)



## 3. Angular의 장점

### 3.1 개선된 개발 생산성

#### 3.1.1 컴포넌트 기반 개발

다른 것 안쓰고 컴포넌트만 가지고도 개발이 가능하다. 컴포넌트로 개발한다는 것은 중복을 제거하기 위함이다. 스무스하게 띄어지고 스무스하게 합쳐져야 하는 것이 포인트. 

#### 3.1.2 TypeScript의 도입

#### 3.1.3 개발 도구의 통합 및 개발 환경 구축 자동화

Angular CLI contributor인 Mike Brocchi‏의 보고에 따르면 개발 환경 구축이 Angular의 도입의 큰 장벽 중 하나로 조사되었다.

프레임워크들은 기존의 환경설정 하는데 하루가 걸린다. 하지만 앵귤러는 매우 간단하다. 



### 3.2 성능의 향상

#### 3.2.1 Digest Loop로 인한 성능저하 문제의 해결

Angular에서는 Digest Loop로 인한 성능저하가 개선되어 AngularJS에 비교할 때 첫 페이지 로딩시간은 2.5배, 리렌더링도 4.2배 정도 빨라졌다.(ng-conf 2016 기준)

#### 3.2.2 AoT 컴파일(ahead of time compilation)

ZiT 컴파일 (JUST IN TIME) : 코드가 실행되는 시점에서 컴파일 되는 것. 속도가 느림.

AoT 컴파일: 미리 모든 템플릿에 대해서 컴파일 해두는 것. 속도가 빨라짐. 

#### 3.2.3 Lazy Loading

모듈이 여러개 있는 데 미리 생성해 놓으면 메모리를 많이 잡아먹고 시작한다. 이것은 미리 안만들어 놓고 필요할 떄 만들어 성능에 도움이 된다. 

#### 3.2.4 코드 최적화

Angular 코드 자체도 지속적인 최적화가 수행되고 있어 45KB 정도의 크기로 축소되었다고 한다.(ng-conf 2016 기준) 

소스코드가 많아지면 처음 넘어올 때 엄청 커질 수 있음. 모바일 환경은 다르다. LTE로 진행되면 치명적이고 아예 돌아가지 않을 수도 있다. 최대한 코드를 줄이는 방법을 연구하고 있다. 



## 4. 브라우저 지원 범위

Angular는 대부분의 모던 브라우저를 지원한다. IE의 경우, 9 이상을 지원한다. 8버전을 지원하려면 엄청난 삽질이 필요하다.



# 2. Angular CLI

## 1. Angular CLI란?

[Angular CLI](https://cli.angular.io/)는 간단한 명령어를 사용하여 Angular 프로젝트 스캐폴딩( 뼈대, scaffolding)을 생성, 실행, 빌드(실제 서버에 올릴 파일들을 만들어내는 작업)할 수 있으며 다양한 구성 요소를 선별적으로 추가할 수 있는 커맨드-라인 인터페이스(command line interface)이다.

테스트 서버 환경에서 실행을 확인할 수 있는 환경을 지원하고 있다. 

Angular CLI가 지원하는 기능은 아래와 같다.

- Angular 프로젝트 생성
- Angular 프로젝트에 컴포넌트, 디렉티브, 파이프, 서비스, 클래스, 인터페이스 등의 구성 요소 추가
- LiveReload를 지원하는 내장 개발 서버를 사용한 Angular 프로젝트 실행 (자동리로드)
- Unit/E2E(end-to-end) 테스트 환경 지원
- 배포를 위한 Angular 프로젝트 패키징 (실제 서버에 갈 놈들만 추려내는 것)



```
my-app/
├── .git/ git에 관련된 것
├── e2e/ 테스트하는 것
├── node_modules/
├── src/ 우리가 작업해야 할 파일들은 모두 이 안에 있음.
├── `.angular-cli.json` 앵큘러가 사용하는 설정 파일.
├── .editorconfig 모든 에디터들이 설정들을 가지고 있는데 공유하려고 하는 것.
├── .gitignore
├── karma.conf.js 테스트할 때 사용하는 라이브러리
├── package.json
├── protractor.conf.js e2e test할 때 사용하는 라이브러리
├── README.md
├── tsconfig.json 타입스크립트에 대한 설정
└── tslint.json 

```

이미 포트 4200번을 사용하고 있다면 Angular CLI 내장 서버를 실행할 수 없다. 포트번호를 변경하고자는 경우에는 다음과 같이 `--port`(축약형 -p) 옵션을 추가한다. 혹시 포트 충돌이 나면!



## 5. 프로젝트 구성 요소 추가

프로젝트에 새로운 구성요소를 추가하기 위해서는 `ng generate` 명령어를 사용한다. `ng generate` 명령어는 축약형 `ng g`와 동일하게 동작한다.

| 추가 대상 구성요소 | 명령어                               | 축약형                |
| ------------------ | ------------------------------------ | --------------------- |
| 컴포넌트           | ng generate component component-name | ng g c component-name |
| 디렉티브           | ng generate directive directive-name | ng g d directive-name |
| 파이프             | ng generate pipe pipe-name           | ng g p pipe-name      |
| 서비스             | ng generate service service-name     | ng g s service-name   |
| 모듈               | ng generate module module-name       | ng g m module-name    |
| 가드               | ng generate guard guard-name         | ng g g guard-name     |
| 클래스             | ng generate class class-name         | ng g cl class-name    |
| 인터페이스         | ng generate interface interface-name | ng g i interface-name |
| Enum               | ng generate enum enum-name           | ng g e enum-name      |

컴포넌트가 대장이고 그 외에 요소들은 모두 컴포넌트를 위한 것들. 



컴포넌트는 항상 뷰를 가지고 있어야 한다. 

styleUrls: ['./home.component.css']

css 는 여러개가 있어야 하니까 배열에 담겨있다. 

앵귤러에서는 프로젝트 당 기본적으로 하나의 컴포넌트, 하나의 모듈을 가져야 한다. app.module.ts, app.component.ts 를 루트 모듈, 루트 컴포넌트 라고 한다. 



#### 5.1.1 파일명의 암묵적 변경

주의해야 할 것은 `ng generate component`명령어 다음에 지정한 컴포넌트명이 실제 생성된 파일명과 다를 수 있다는 것이다. 예를 들어 아래와 같이 새로운 컴포넌트를 추가해 보자.

**무조건 파일명은 캐밥 케이스로! 케밥 케이스로 주지 않아도 스스로 바꿔준다.** 

**CSS는 대문자로 시작하는 카멜 케이스** 



#### 5.1.2 selector 프로퍼티값의 접두사(prefix)와 컴포넌트 클래스 이름

```
// src/app/home/home.component.ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {

  constructor() { }

  ngOnInit() { }
}
```

왜 컴포넌트 이름을 home이라고 만들었는데 app-home 이라고 생성할까?

중복될 가능성이 있기 때문에 무조건 <프로젝트이름-내가 만든 컴포넌트 이름>

.angular-cli.json  파일 안에 보면 "prefix": "app" 로 되어있다. 

```
$ ng new my-app --prefix todos
```

위의 명령어를 사용하면 프리픽스도 미리 설정할 수 있다. 



#### 5.1.3 templateUrl, styleUrls 프로퍼티와 template, styles 프로퍼티

```
// src/app/home/home.component.ts
...
@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
...
```

@를 붙여주면 decorator 함수라는 뜻. 뒤에 올 클래스, 변수 등을 장식한다. 뒤에 클래스가 오면 이 클래스는 일반 클래스가 아니고 컴포넌트 라고 프레임워크에게 알려주는 것. 우리가 개별적으로 클래스 인스턴스를 생성하지 않느다. 이것은 앵귤러가 생성하는데 데코레이터 함수를 보고 생성하라고 알려준다. 우리가 알려주고 싶은 정보만 데코레이터 함수 안에 넣어 앵귤러에게 알려준다. 위에 3가지만 기본적인 정보. 더 넣어줄 수 있다. 



위 예제의 경우 컴포넌트는 같은 폴더 내의 외부 파일 `home.component.html`과 `home.component.css`를 HTML 템플릿과 CSS로 사용한다. 템플릿 또는 CSS가 간단한 경우에는 메타데이터 내부에 직접 기술할 수도 있다. 이때 `templateUrl`, `styleUrls` 프로퍼티 대신 `template`, `styles` 프로퍼티를 사용한다.

```
// src/app/home/home.component.ts
...
@Component({
  selector: 'app-home',
  template: `
    <p>home works!</p>
  `,
  styles: [`
    p { color: red; }
  `]
})
...
```



ng generate component 명령어를 사용하여 컴포넌트를 추가할 때 HTML 템플릿과 CSS를 외부 파일로 생성하지 않고 인라인 HTML 템플릿과 CSS를 사용하고자 하는 경우에는 아래의 명령어를 사용한다.

```
# 인라인 HTML 템플릿을 사용하는 경우
$ ng g c home --inline-template
# 인라인 CSS를 사용하는 경우
$ ng g c home --inline-style
# 인라인 HTML 템플릿과 인라인 CSS를 사용하는 경우
$ ng g c home --inline-template --inline-style // 축약 -i-t, -i-s
```



### 5.2 디렉티브 추가

### 5.3 모듈 추가

### 5.4 서비스 추가

추후 실습 때 그때 그때 설명!



## 6. 프로젝트 빌드

webpack을 사용하기 때문에 모듈 번들링 하고 

### 6.1 트랜스파일링과 의존 모듈 번들링



# 3. Angular Architecture

## 1. Angular 애플리케이션의 파일 구조

```
my-app/
├── .angular-cli.json ** 앵귤러 전반적인 설정을 기술하는 파일. 만질일이 있다. 팀내에서 단 한명만 고치게 한다. 여러사람이 고치면 문제가 생길 수 있다. 
├── .editorconfig
├── .git/
├── .gitignore
├── e2e/
│   ├── app.e2e-spec.ts
│   ├── app.po.ts
│   └── tsconfig.e2e.json
├── karma.conf.js
├── node_modules/
├── package.json
├── protractor.conf.js
├── README.md
├── src/
│   ├── app/
│   │   ├── app.component.css
│   │   ├── app.component.html
│   │   ├── app.component.spec.ts
│   │   ├── app.component.ts
│   │   └── app.module.ts
│   ├── assets/ /// 폰트 이미지 들은 여기에 넣어 두는 것이 좋다. 
│   ├── environments/ 
│   │   ├── environment.prod.ts // 파이널 빌드 할 때 사용한다. $ ng build -prod 환경 변수들을 저장하기도 한다. 
│   │   └── environment.ts
│   ├── favicon.ico
│   ├── index.html // 건드릴 일이 없다. 그대로 사용하게 됨.
│   ├── main.ts // 편집할 일은 없지만 앵귤러가 동작을 시작하면 가장 먼저 실행될 자바스크립트.
│   ├── polyfills.ts
│   ├── styles.css // 글로벌 css가 위치할 파일이다. 간단하면 여기에 다 가져다 놓는다. 
│   ├── test.ts
│   ├── tsconfig.app.json
│   ├── tsconfig.spec.json
│   └── typings.d.ts 타입 스크립트가 돌려면 여러개의 라이브러리가 있어야 하는데 예를들어 제이쿼리를 사용한다고 하면 타입정보를 기술해 놓은 이것을 사용한다. 
├── tsconfig.json
└── tslint.json
```

## 2. Angular 애플리케이션의 처리 흐름

알아두면 좋다. 뒤에서 다시 한 번 설명.

![angular-process](/Users/mac/Documents/dev/TIL/angular-process.png)

```
inline.bundle.js
Webpack 유틸리티가 포함된 Webpack loader

polifills.bundle.js
polyfill 의존성 모듈(core-js, zone.js)을 번들링한 파일
zone.js가 변화 감지하는 것. 

styles.bundle.js
스타일 정의를 번들링한 파일

vendor.bundle.js
Angular 의존성 모듈(@angular/*, RxJS 등)을 번들링한 파일

main.bundle.js
개발자가 작성한 컴포넌트, 디렉티브, 서비스 등 소스코드를 번들링한 파일
```

### 2.2 main.ts

프로젝트의 메인 진입점(main entry point)이다. platformBrowserDynamic()에 의해 JIT 컴파일러가 실행되고 루트 모듈(/src/app/app.module.ts)을 부트스트랩한다.

부트스트랩이란 발화시킨다. 실행시키게 만든다. 

모든 애플리케이션이 하는 일은 결국 html을 만드는 것이다. 



### 2.3 app.module.ts

모든 컴포넌트의 부모 역할을 담당하는 루트 컴포넌트이다.

어떠한 뷰를 생성하냐? 이아이가 생성한 뷰는 

app-home은 루트 컴포넌트의 템플렛에 기술했다. 홈 커포넌트는 루트 컴포넌트의 자식이다. 



## 3. Angular의 구성 요소

용어는 나중에 설명하기!



# 4. Angular Component - **Basics**

컴포넌트 기반이기 때문에 컴포넌트 이야기를 많이 할 수 밖에 없음. 

이중에서도 6번 Data Binding 을 알면 반을 아는 것이나 마찬가지다. 

프레임 워크의 사상이 있다. 이러한 형태로 만들자고 했을 때 다 이유가 있다. 이 사상의 동의를 하기 위해서는 뭔가 경험을 해봐야 한다. 

## 1. 컴포넌트 소개

컴퓨터 사이언스가 가장 관심있어 하는 부분. ---> 적은 돈 내가 많이 빨리 만들려고 한다는 것. 사업주의 이익증배. 이를 위해선 재사용, 유지보수성을 강조한다. 하지만 이것도 아니더라. 결국 새로운 개념이 나온것이 웹 컴포넌트.



### 1.1 웹 컴포넌트

결국 만들어 내는 것은 html css javascript 

정확히 한 부분을 들어내는 것이 어렵다. css 는 특히 그렇다. 들어내면 어떤 문제가 생길지 모르고 넣으면 어떻게 될지 모른다. 

하나의 부품처러 여기에 썼다가 저기에 썼다가 다른데 영향도 안주고 하면 얼마나 좋을까? 굉장히 도움이 될 것이다. 

W3C 표준인 [웹 컴포넌트(Web Component)](https://www.webcomponents.org/introduction)를 기반으로 한다.



독립적이고 완결된 뷰를 만들고 싶다는 방법으로 웹 컴포넌트가 나왔다. 그러려면 HTML CSS Javascript가 한 단위에서 움직여야 한다. 

1. 컴포넌트의 뷰를 생성할 수 있어야 하며(HTML Template)
2. 외부로부터의 간섭을 제어하기 위해 스코프(scope)를 분리하여 DOM을 캡슐화(Encapsulation)할 수 있어야 하며(Shadow DOM) --> DOM을 쪼갤 수 있어야 한다. 
3. 외부에서 컴포넌트를 호출할 수 있어야 하고(HTML import)
4. 컴포넌트를 명시적으로 호출하기 위한 명칭(alias)을 선언하여 마치 HTML 요소와 같이 사용할 수 있어야 한다(Custom Element).

—> 이런 4가지 조건을 충족시키면 웹 컴포넌트라고 부르자!



### 1.2 컴포넌트 트리

![building-structure](/Users/mac/Documents/dev/TIL/building-structure.png)

엄청나게 복잡한 뷰라도 하나의 컴포넌트로 만들 수 있다. 

일반적으로는 한 화면에 꽉차는 뷰를 구조에 따라 나눌 수 있다. 사진과 같은 예제의 경우 5개의 컴포넌트로 만들 수 있다.

![component-tree](/Users/mac/Documents/dev/TIL/component-tree.png)



상태와 이벤트가 위의 선을 따라서 왔다갔다 한다. 즉 트리 구조가 굉장히 중요한 역할을 갖는다. 

헤더의 이미지와 네비게이션으로 나눌 수 있는데 컴포넌트를 2개로 분류할 수 있다. 



## 2. 컴포넌트 기본 구조



### 2.2 컴포넌트의 기본 동작 구조

데이터 바인딩이란 결국 서로의 상태 변화를 알려준다는 것. 서로의 상태를 같이 묶어주기 위한 행위.

액션의 시작은 항상 뷰 == app.component.html 

![component](/Users/mac/Documents/dev/TIL/component.png)



## 3. 컴포넌트 작성 실습

### 3.1 네이밍 컨벤션

```
기능을 명확히 설명하는 구성요소의 이름.구성요소 타입.ts
```



이후에는 실습으로 익히기 

# 5. Angular Component - **Template**

![mvc-mvvm](/Users/mac/Documents/dev/TIL/mvc-mvvm.png)

View: 화면에 보여지는 것. 템플릿을 View라고 볼 수 있다. 

Model: 모든 데이터 로직을 컨트롤 하는 애. 모델의 직업처럼 나처럼 입으면 멋지게 보일꺼야. 항상 View를 위해 존재. 컴포넌트의 클래스가 Model이라고 할 수 있다.





![angular-view-model](/Users/mac/Documents/dev/TIL/angular-view-model.png)

Angular의 뷰와 모델은 다음 그림과 같다. 여기서 이렇게 가로로만 왔다갔다 하는 것이 아니라 컴포넌트들이 많이 때문에 위 아래로도 마구 왔다 갔다 한다. 



![databinding-changedetection](/Users/mac/Documents/dev/TIL/databinding-changedetection.png)

이벤트 바인딩만 템플리에서 컴포넌트 클래스로 간다. 모두 원웨이를 하지만 양방향 바인딩은 문법적 설탕. box in banana라고 불린다. 사실상 성능 때문에 지원하지 않는다. 실제로 안을 들여다보면 프로퍼티 바인딩, 이벤트 바인딩이 각각 반응하는 것이다. 