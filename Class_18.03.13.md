18.03.19(화)

## 1. 템플릿 참조 변수(Template reference variable)

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <div>
      <!-- 템플릿 참조 변수 email의 선언 -->
      <input #email type='email' placeholder="이메일을 입력하세요">
// 별도의 변수 없이도 사용할 수 있다. 템플릿 전역에서 사용할 수 있다. 남발하면 안된다. 이것이 나중에 객체화 될 것인데 email 변수를 참조하고 있다고 생각하면 된다. 
      <!-- 템플릿 참조 변수 email의 참조  -->
      <button (click)="checkEmail(email.value)">이메일 형식 체크</button>
    </div>
    <span *ngIf="result">{{ result }}</span>
  `
})
export class AppComponent {
  result: string;

  checkEmail(email: string) {
    const regexr = /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/;

    if (regexr.test(email)) {
      this.result = '';
    } else {
      this.result = '이메일 주소의 형식이 유효하지 않습니다.';
    }
  };
}
```



## 2. 세이프 내비게이션 연산자(Safe navigation operator)

세이프 내비게이션 연산자 `?`는 컴포넌트 클래스의 프로퍼티의 값이 null 또는 undefined일 때 발생하는 에러를 회피하기 위해 사용한다.

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <!-- obj가 null 또는 undefined일 때 아무것도 표시하지 않는다. -->
    {{ obj }}
    <!-- ERROR TypeError: Cannot read property 'id' of undefined -->
    {{ obj.id }}
// 치명적인 애러, 애플리케이션이 동작하지 않을 수도 있다. 
    <!-- 세이프 내비게이션 연산자는 null 또는 undefined의 프로퍼티를 만나면 처리를 종료하고 에러를 발생시키지 않는다. -->
    {{ obj?.id }}
// ? 는 obj가 있으면 이라는 뜻.
  `
})
export class AppComponent { }
```

function foo (obj) {

​	if ( !obj | obj.id )

​	// 방어코드

​	return obj.id;

}



# 9. Angular Component - Interaction

쓸데 없이 상태를 공유해야 하는 일을 어떻게 하면 줄일까? 이를 위해 서비스라는 것을 만들고 서비스한테 상태 변화를 알려주고 상태변화를 알고 있어야 하는 애가 서비스를 바라보고 있으면 된다. 애플리케이션이 커지면 서비스의 숫자가 늘어나고 그만큼 복잡해 진다. 그 때는 서비스만을 따로 관리하는 스토어를 만들어 준다. 

## 1. 컴포넌트의 계층적 트리 구조

트리구조 == 부자관계가 있다. 모든 컴포넌트들이 가족인데 단군이 루트 컴포넌트 이다. 관계속에서 서로의 상태를 주고받을 수 있다. 

![component-interaction](/Users/mac/Documents/dev/TIL/component-interaction.png)



서로 느슨한게 아는 것이 좋다. 파랑이 초록에 대해 알아야 하는 것은  초록의 셀렉터만 알면 된다. 

어떠한 관계 간에도 상태를 주고받을 수 있는데 내려갈 때는 프로퍼티 바인딩, 올라갈 때는 이벤트 바인딩을 사용한다. 

- @Input, @Output 데코레이터
- ViewChild와 ViewChildren, ContentChild와 ContentChildren 
- [서비스 중재자 패턴](http://poiemaweb.com/angular-service#7-%EC%84%9C%EB%B9%84%EC%8A%A4-%EC%A4%91%EC%9E%AC%EC%9E%90-%ED%8C%A8%ED%84%B4service-mediator-pattern)을 구현한 상태 공유 서비스 == 서비스 
- 상태 관리를 위한 외부 라이브러리([NgRx](https://github.com/ngrx/store), [Redux](http://redux.js.org/) 등) 사용 == 서비스를 모아놓은 스토어를 의미

```
component-interaction/
├── src/
│   ├── app/
│   │   ├── user-list/
│   │   │   └── user-list.component.ts
│   │   ├── app.component.ts
│   │   └── app.module.ts
...
```

컴퍼넌트 단위로 라우팅이 일어날 수 있기 때문에 폴더 하나 하나씩 관리하는 것이 좋다. 하지만 많아지면 곤란하기 때문에 컴포넌트 폴더를 따로 만들어 파일을 그 안에 넣어 관리한다. 



## 2. 부모 컴포넌트와 자식 컴포넌트의 상태 공유

### 2.1 부모 컴포넌트에서 자식 컴포넌트로 상태 전달

#### 2.1.1 @Input 데코레이터

데코레이터 안에는 컴퓨터에게 알려줄 정보 메타 데이터를 적는다. 

form 요소를 가지고 있는 부모 컴포넌트의 경우, (폼요소가 있어야 상태가 변화될 것이라서) 사용자에 의해 상태(state)가 변경되면 이를 자식 컴포넌트와 공유할 필요가 있다. 

![parenttochild](/Users/mac/Documents/dev/TIL/parenttochild.png)

<child [state] = "myState"></child>

state라는 이름으로 mystate의 값을 child 에게 보내겠다.는 뜻. 



@Input() state: string;

자식이 부모가 준 것을 받아야 하니까 @input 데코레이터로 받는다. 이 때 부모가 정한 프로퍼티 마음대로 쓰지 말고 이름을 맞춰줘야 한다.  내가 받아야 하는 데이터가 누가 줬는지는 알 필요가 없고 이름과 타입만 알고 있으면 된다. 

![@input-property-2](/Users/mac/Documents/dev/TIL/@input-property-2.png)만약에 부모 컴포넌트에서 실행한 프로퍼티 바인딩의 프로퍼티명과는 다른 프로퍼티명을 자식 컴포넌트에서 사용하려면 아래와 같이 @Input 데코레이터에 프로퍼티 바인딩의 프로퍼티명을 인자로 전달하고 사용하고자 하는 프로퍼티명을 선언한다.

#### 2.1.2 @Input 데코레이터와 setter를 이용한 입력 프로퍼티 조작



부모가 준 데이터를 받을 때  그냥 받는 것이 아니라 그것으로 무언가를 하고 싶을 때 setter를 사용한다. ES6 문법과 같다. 



지금까지 살펴본 예제에 사용자 역할(role)별로 사용자를 카운트하는 기능을 추가해 보자. user-list.component.ts를 아래와 같이 수정한다. ---> 다시 실습해보기.



### 2.2 자식 컴포넌트에서 부모 컴포넌트로 상태 전달

부모에게 보낼 때는 이벤트 바인딩으로 보낸다. 

#### 2.2.1 @Output 데코레이터와 EventEmitter

![childtoparent](/Users/mac/Documents/dev/TIL/childtoparent.png)

부모에게 보낼 때는 이벤트 바인딩으로 보낸다. 즉, 자식이 이벤트를 발생시킬 수 있어야 하는데 EventEmitter()를 사용한다. 여기서 파랑 글씨 myEvent는 우리가 정해야 하는 이벤트 이름. 인자에 상태를 담아서 부모에게 전달한다. 

부모는 자식한테 마이이벤트라는 것이 발생하면 ($event)안에 고스란히 담겨있다. 

```
// 부모 컴포넌트에게 상태 정보를 전달하기 위해 출력 프로퍼티를 EventEmitter 객체로 초기화한다.
  @Output() remove = new EventEmitter<User>();
// <User> 타입의 객체를 담아서 보낸다는 뜻.
```



```
<button
  class="btn btn-danger btn-sm"
  (click)="remove.emit(user)">
  // (user)는 button이 소속된 tr의 user 데이터. 
  <span class="glyphicon glyphicon-remove"></span>
</button>
```

## 3. Stateful 컴포넌트와 Stateless 컴포넌트

- **Stateful Component(순수)**

상태를 수정하고 삭제하고 모든 일을 하는 것.

- **Stateless Component(비순수- 일체의 side effect를 받지 않는다.)**

상태를 수정하지 않고 viewing만 하고 상태가 변화되면 이렇게 저렇게 해달라 부모한테 위임만 했다. 



왜 역할을 나눌까? 결국 유지보수가 힘들어진다. 변경할 일이 있으면 한 놈한테 몰아서 시켜라. 로직에 수정이 생기거나 했을 때 한 놈 한테만 가면 된다. 

가급적이면 Stateful component를 줄이는 것이 좋다. 현실적이진 않지만..

![component-state](/Users/mac/Documents/dev/TIL/component-state.png)

## 4. 원거리 컴포넌트 간의 상태 공유

![complex-component](/Users/mac/Documents/dev/TIL/complex-component.png)



A상태의 변경을 R 뿐만 아니라 C 한테도 알려야 한다면? @Input() @Output() 방식은 현실적이지 못하다. 

[서비스 중재자 패턴(Service Mediator Pattern)](http://poiemaweb.com/angular-service#7-%EC%84%9C%EB%B9%84%EC%8A%A4-%EC%A4%91%EC%9E%AC%EC%9E%90-%ED%8C%A8%ED%84%B4service-mediator-pattern) 사용해야 한다. 서비스를 공부할 때 배우게 된다. 우리의 todo-list의 마지막 버전이 이것까지 들어가는 것. 



# 10. Angular Component - Accessing Child

자바스크립트로 요소에 접근하는 방법을 말한다. DOM API 처럼...

- @ViewChild
- @ViewChildren
- @ContentChild
- @ContentChildren

## 1. @ViewChild와 @ViewChildren



```
@ViewChild(탐색대상 클래스명) 프로퍼티명: 탐색대상 클래스명;
```

![viewchild](/Users/mac/Documents/dev/TIL/viewchild.png)

```
import { Component, ViewChild } from '@angular/core';
import { ChildComponent } from './child/child.component';

@Component({
  selector: 'app-root',
  template: `
    <h3>Parent</h3>
    <button type="button" (click)="toggle()">Toggle Child</button>
    <button type="button" (click)="changeText()">Change Child's text</button>
// native 요소, 하나 하나를 view child라고 부른다. 
    <child></child>
  `
})
export class AppComponent {
  // myChild 프로퍼티에 자식 컴포넌트 ChildComponent의 인스턴스가 바인딩된다.
  @ViewChild(ChildComponent) myChild: ChildComponent;

  toggle() {
    // 자식 컴포넌트의 프로퍼티를 직접 변경할 수 있다.
    this.myChild.isShow = !this.myChild.isShow;
  }

  changeText() {
    // 자식 컴포넌트의 메소드를 직접 실행할 수 있다.
    this.myChild.changeText('Hello');
  }
}
```



## 2. @ContentChild와 @ContentChildren

요소 내부 안에 컨탠츠를 가지고 오는 것을 말한다. 복잡해서 수업 안함. 



# 11. Angular Component - Style

## 1. 컴포넌트 스타일

CSS를 캡슐화하여 다른 CSS에 영향을 주지 않고  지역화 해서 관리해야 한다. 

 @Component 데코레이터의 메타데이터 객체의 styles 프로퍼티에 직접 정의하는 방법과 styleUrls 프로퍼티에 외부 CSS 파일의 경로를 정의하는 방법이 있다.

 부모 컴포넌트의 스타일은 자식 컴포넌트에 어떠한 영향을 주지 않는다.



## 2. 뷰 캡슐화 (View Encapsulation)

shadow DOM의 표준을 따르지 않고 있다. 왜 표준을 따르지 않는가? 브라우저의 서포트가 제각각이라 그렇다. 

@Component 메타데이터 객체에 `encapsulation` 프로퍼티에 [ViewEncapsulation](https://angular.io/api/core/ViewEncapsulation) 옵션을 지정하여 컴포넌트 별로 뷰 캡슐화 전략을 설정할 수 있다. ViewEncapsulation은 열거형으로 아래의 3가지 캡슐화 전략을 제공한다.

| ViewEncapsulation | 의미                                                         |
| ----------------- | ------------------------------------------------------------ |
| Emulated          | 임의의 어트리뷰트를 추가하는 브라우저의 기본 Shadow DOM 구현 방식이다. 컴포넌트의 스타일은 해당 컴포넌트에만 적용된다. (기본 전략) |
| Native            | 웹 컴포넌트의 Shadow DOM를 사용하는 방식이다. 컴포넌트의 스타일은 해당 컴포넌트에만 적용된다. |
| None              | 스타일 캡슐화를 지원하지 않는다. 컴포넌트의 CSS는 전역에 지정되어 다른 다른 컴포넌트에 영향을 준다. |

## 3. 쉐도우 DOM 스타일 셀렉터 (Shadow DOM Style Selector) 중요

| 쉐도우 DOM 스타일 셀렉터 | 의미                                                         |
| ------------------------ | ------------------------------------------------------------ |
| :host (가상셀렉터)       | 호스트 요소(컴포넌트 자신)을 선택한다.                       |
| :host-context            | 호스트 요소의 외부(예를 들어 body)의 조건에 의해 컴포넌트의 요소를 선택한다. |
| /deep/                   | [폐지(deprecated)](https://angular.io/guide/component-styles#deprecated-deep--and-ng-deep) 자식 컴포넌트에 속한 요소를 선택한다. |

### 3.1 :host 셀렉터

:host 셀렉터는 호스트 요소(컴포넌트 자신)을 선택한다. 

테마를 설정해야할 때가 있다. html 유료 템플릿 같은 것을 샀을 때 간단한 설정으로 바탕을 바꿔줄 수 있다. 내 조상중에 어떤 변화 CSS 요소가 먹히면 난 이렇게 요소를 바꿔라 라는 것. 



### 3.2 :host-context 셀렉터

:host-context 셀렉터는 호스트 요소의 외부의 조건 즉 부모 요소를 포함하는 조상 요소의 클래스 선언 상태에 의해 컴포넌트의 요소를 선택하는 경우 사용한다. 



## 4. 글로벌 스타일

애플리케이션 전역에 적용되는 글로벌 스타일을 적용하려면 src/styles.css에 CSS 룰셋을 정의한다. 



## 5. Angular CLI로 Sass 적용 프로젝트 생성

```
{
  ...
  "apps": [
    ...
    "styles": [
      "styles.scss"
    ],
  ...
  "defaults": {
    "styleExt": "scss",
    "component": {}
  }
}
```



## 6. Angular Material

완전히 별도의 프로젝트로 움직인다. Material이라고 하는 디자인 스펙이 있는데 구글이 만들고 있고 구글은 이러한 디자인을 사용하고 있다. 심플해서 한국에선 인기 없음.

이것을 사용하면 굉장히 고생스럽다. 우리 입맛에 고치려고 들면 정말 힘들다. 왠만하면 사용하지 말 것. 그래로 사용하려면 OK. 일반적인 CSS 프레임 워크를 사용하는 것이 좋다. 