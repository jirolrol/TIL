# 5. Angular Component - Template



## 1. 템플릿(Template)이란?

관심사가 다른 것은 분리한다.(이론)

하지만 이론과 현실은 다르다.

![template](/Users/mac/Documents/dev/TIL/template.png)



방향을 주의해서 살펴볼 것.

![databinding-changedetection-1](/Users/mac/Documents/dev/TIL/databinding-changedetection-1.png)



## 2. 템플릿 문법(Template Syntax)

총 12가지를 이용해서 템플릿을 만들어 낸다.  이중에 가장 중요한 것이 **프로퍼티 바인딩**

<u>컴포넌트와 컴포넌트 사이의 교환에도 프로퍼티 바인딩이 사용된다.</u> 

모든 컴포넌트의 아버지는 루트 컴포넌트. 루트 컴포넌트를 호출하는 것은 index.html 이다. 즉, 모든 컴포넌트들은 바디의 자식. 

| 템플릿 내 사용 금지 항목                                     | 비고                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| script 요소를 사용하지 못함.                                 | 보안 상 문제로 사용이 금지된다.                              |
| 대입연산자(=, +=, -=), 증감 연산자(++, --), 비트 연산자(\|, &), 객체 생성 연산자(new) | 템플릿 표현식 내에서 데이터를 변경할 수 있는 연산은 사용을 금지한다(Unidirectional data flow 정책) 예를 들어 {{ foo=bar }}는 에러를 발생시킨다. |
| 전역 스코프를 갖는 빌트인 객체                               | window, document, location, console 등                       |

# 6. Angular Component - Data Binding

## 1. 데이터 바인딩(Data binding)이란?

왜 데이터 바인딩을 사용하는가?

구조화된 웹 애플리케이션(유지보수성을 가만하여 여러 파일로 분리되어진 구조화된 웹 애플리케이션) 뷰와 모델의 분리가 필수적이다. 왜? 관심사가 다르기 때문에. 유지보수를 위해서. 하나의 수정사항을 얼만큼 빨리 대응하느냐가 중요하다.모든 것은 돈이다. 런칭되어 사용되어질 때 무수한 버그가 발생되고 개선사항 등등을 얼만큼 빨리 대응하느냐! 가장 중요.뷰와 모델도 원래는 협력해야할 아이들. 결국은 둘의 할일은 html을 만들어 내는 것.



![procedural-programming](/Users/mac/Documents/dev/TIL/procedural-programming.png)jQuery를 사용하는 웹 애플리케이션의 경우 로직이 돔을 조작한다. 이 말은 돔이 변경되어 지면 로직을 변경시켜야 한다. 



![declarative-programming](/Users/mac/Documents/dev/TIL/declarative-programming.png)

템플릿이 주어가 된다. 탬플릿이 컴포넌트 클래스에 와서 가져간다. 로직을 설명하지 않는다. {{}} 이것으로 선언하여 프로그래밍 한다. 

html은 필요한 것들을 배열 방식으로 쌓아서 사용한다. 이런식으로 프로그래밍 하는 것을 선언형 프로그래밍 이라고 한다. 이제는 템플릿이 주도를 한다. 

코드량 자체가 많이 줄고 의외로  간단하다. (if문을 삼항연산자로 만드는 것은 코드량이 주는 것이 아니다.)  자바스크립트의 상세한 문법을 몰라도 웹개발이 가능하다.

느슨한 결합. 서로 많이 알면 안된다. 프레임워크를 이용하면 전체적인 구조까지 파악해서 패턴을 제시한다. 



*하지만 너무 프레임워크만 사용하다 보면 기본 문법을 잊어버린다. 회사 입사후에도 자바스크립트 기본 문법책을 가지고 다니면서 전철에서 읽고 다니기. 월급 나오면 공부를 더 안하게 된다. 



## 2. 변화 감지(Change detection)

깊숙히 들어가면 어려운 주제이므로 개념은 이해해야 함.

변화 감지란 뷰와 모델의 동기화를 유지하기 위해 변화를 감지하고 이를 반영하는 것을 말한다. 

뷰는 왜 존재하는가? 유저와 인터랙션 하기 위해서 존재한다. 개발자 측면이 아니라 사용자 입장해서 만들어야 한다. 따라서 개발을 잘 모르는 디자이너가 만드는 것이 좋다. 

input text 요소는 유저가 문자를 넣거나 지울 수 있다. ---> 이러한 상태의 변화

체크박스 요소는 유저가 체크를 하거나 풀거나 할 수 있다. ---> 이러한 상태의 변화 

즉 View에서 일어난 변화를 Model이 알아야 한다. 그러면 이 모델이 무언가를 하고 View에 알려야 하는 이 한 바퀴가 양방향 바인딩이라고 한다. 이것을 하기 위해서는 무한루프를 돌려야 한다. 하지만 변화가 한 두개가 아니므로 와쳐가 많아야 하고 성능은 당연히 떨어지게 되어있다. 개발은 편한데 성능이 좋지 않다. 이것을 해결하려고 나온게 React.

우리가 배우는 Angular는 단방향 바인딩만 지원한다. 



![change-detection](/Users/mac/Documents/dev/TIL/change-detection.png)



- DOM 이벤트(click, key press, mouse move 등)
- Timer(setTimeout, setInterval)의 tick 이벤트
- Ajax 통신 / Promise

**즉,  zone.js 는 이 3가지를 감시하고 이것이 일어나면 프로퍼티가 변화되었다고  템플릿에 알려준다.**  zone.js는 addEventListener, Timer 함수, XMLHttpRequest, Promise 등을 [몽키패치](https://en.wikipedia.org/wiki/Monkey_patch)한다. 몽키패치는 안티패턴. 

```
// node_modules/zone.js/dist/zone.js
function zoneAwareAddEventListener() {...}
function zoneAwareRemoveEventListener() {...}
function patchTimer() {...}
function zoneAwarePromise() {...}
...

window.prototype.addEventListener = zoneAwareAddEventListener;
window.prototype.removeEventListener = zoneAwareRemoveEventListener;
window.prototype.promise = zoneAwarePromise;
window.prototype.setTimeout = patchTimeout;
...
```



## 3. 데이터 바인딩

데이터 바인딩은 뷰와 모델을 하나로 연결하는 것을 의미한다. 

| 데이터 바인딩        | 데이터의 흐름            | 문법                               |
| -------------------- | ------------------------ | ---------------------------------- |
| 인터폴레이션         | 컴포넌트 클래스 ⟹ 템플릿 | {{ expression }}                   |
| 프로퍼티 바인딩      | 컴포넌트 클래스 ⟹ 템플릿 | [property]=”expression”            |
| 어트리뷰트 바인딩    | 컴포넌트 클래스 ⟹ 템플릿 | [attr.attribute-name]=”expression” |
| 클래스 바인딩        | 컴포넌트 클래스 ⟹ 템플릿 | [class.class-name]=”expression”    |
| 스타일 바인딩        | 컴포넌트 클래스 ⟹ 템플릿 | [style.style-name]=”expression”    |
| 이벤트 바인딩        | 컴포넌트 클래스 ⟸ 템플릿 | (event)=”statement”                |
| 양방향 데이터 바인딩 | 컴포넌트 클래스 ⟺ 템플릿 | [(ngModel)]=”variable”             |

### 3.1 인터폴레이션(Interpolation)

```
{{ expression }}
// 표현식이 안에 들어간다. 즉 하나의 값으로 수렴이 되어야 한다. 일괄적으로 문자열로 변환된다. 
```

```
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  template: `
    <p>name: {{ name }}</p>
    <p>age: {{ age }}</p>
    <p>admin: {{ admin }}</p>
    <p>address: {{ address.city }} {{ address.country }}</p>
    <p>gender: {{ gender }}</p>
    <p>sayHi(): {{ sayHi() }}</p> // 어떤걸 리턴하냐에 따라서 표현식이 될 수도 안될 수도 있다. 여기서는 문자열을 리턴하고 있으므로 
    <p>age * 10: {{ age * 10 }}</p>
    <p>age > 10: {{ age > 10 }}</p>
    <p>'stirng': {{ 'stirng' }}</p>
  `
})
export class AppComponent {
  name = 'Angular';
  age = 20;
  admin = true; // 불린값은 문자열로 변환되어야 하는 곳에선 true로 나온다. 
  address = {
    city: 'Seoul',
    country: 'Korea'
  };

  sayHi() {
    return `Hi! my name is ${ this.name }.`;
// 여기서 this는 AppComponent가 생성할 인스턴스의 name을 가르킨다. 즉, 'Angular'.
만약 여기서 this가 없으면 지역변수 name을 찾고 없으므로 레퍼런스 에러.
  }
}
```

### 3.2 프로퍼티 바인딩(Property binding) *중요*

엄연히 프로퍼티와 어트리뷰트는 다른 것이다.

- 프로퍼티란?

객체의 일원을 프로퍼티라고 한다. 객체는 프로퍼티명과 값으로 구성되어 있다. 여기서의 프로퍼티를 말한다. 

(로딩은 문자를 읽는 것이고 파싱은 앞으로 문자열을 가지고 브라우져에 표시를 해야하는데 브라우져의 로직에서 사용하기 편하도록 객체화 해야 한다. 즉, 랜더트리를 만든다. 돔으로 변환된 순간 어트리뷰트는 없다. 즉 어트리뷰트는 프로퍼티로 바뀌어야 하는데 일대일 매핑이 안된다. )

- 어트리뷰트란?



프로퍼티 바인딩은 컴포넌트 클래스의 프로퍼티와 템플릿 간의 단방향 바인딩(One-way binding)에 사용되는 템플릿 문법으로 표현식의 평가 결과를 HTML 요소의 DOM 프로퍼티에 바인딩한다.

```
<element [property]="expression">...</element>
```

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <!-- value 프로퍼티에 컴포넌트 클래스의 name을 프로퍼티 바인딩 -->
    <input type="text" [value]="name">
// 여기서 type은 어트리뷰트다.어트리뷰트의 값은 늘 문자열이다. 
   [value]는 나중에 input이 파싱을 통해 객체가 될 때 프로퍼티가 된다. 어트리뷰트가 아니다. 

    <!-- innerHTML 프로퍼티에 컴포넌트 클래스의 contents를 프로퍼티 바인딩 -->
    <p [innerHTML]="contents"></p>
// <p> 요소가 파싱을 통해 DOM 객체가 되면 innerHTML이라는 프로퍼티가 있다는 이야기. 
// 결국 인터폴레이션과 같은 일은 하는 것이다. 

    <!-- src 프로퍼티에 컴포넌트 클래스의 imageUrl을 프로퍼티 바인딩 -->
    <img [src]="imageUrl"><br>
// 나중에 DOM 객체가 되면 그 안에 src 속성이 있다. 그 안에 패스를 할당하고 있는 것. 
// 하지만 src는 innerHTML 과 다르게 어트리뷰트가 있다. 일대일 매핑이 되지 않는 다는 말이 바로 이것. 
   이름이 같지만 다른 것이다. 
   
    <!-- disabled 프로퍼티에 컴포넌트 클래스의 isUnchanged를 프로퍼티 바인딩 -->
    <button [disabled]="isDisabled">disabled button</button>
  `
})
export class AppComponent {
  name = 'ungmo2';
  contents = 'Lorem ipsum dolor sit amet, consectetur adipisicing elit.';
  imageUrl = 'https://via.placeholder.com/350x150';
  isDisabled = true;
}
```

프로퍼티의 값으로는 undefined 빼고 모두 줄 수 있다. 즉, undefined 빼고 모두 들어갈 수 있다. 



```
<p>{{ contents }}</p>
<input type="text" value="{{ name }}">
```

인터폴레이션은 문자열이 필요한 곳이면 아무 곳이나 사용할 수 있다. 문법적 설탕이다. 

```
<p [innerHTML]="contents"></p>
<input type="text" [value]="name">
```

위의 두가지는 도출되는 것은 같지만 다른 것이다. 



### 3.3 어트리뷰트 바인딩(Attribute binding)

왜 프로퍼티 바인딩과 어트리뷰터 바인딩을 따로 구분해야 하는가?

```
<element [attr.attribute-name]="expression">...</element>
```



HTML 객체들은 DOM 노드 객체의 프로퍼티 중 attributes 프로퍼티 안에 attribute를 가지고 오는데 이 안에 모든 어트리뷰트가 있는 것은 아니다. 



- id 어트리뷰트와 id 프로퍼티와 1:1 매핑한다.
- class 어트리뷰트는 **classList 프로퍼티**로 변환된다.
- td 요소의 colspan 어트리뷰트의 경우, 매핑하는 프로퍼티가 존재하지 않는다. 병합하는 것. 
- [textContent](https://developer.mozilla.org/ko/docs/Web/API/Node/textContent) 프로퍼티의 경우, 대응하는 어트리뷰트가 존재하지 않는다.
- input 요소의 value 어트리뷰트는 value 프로퍼티와 1:1 매핑하지만 서로 다르게 동작한다.

이외에도 정말 많은 케이스가 있다. 모든 케이스를 다 알 필요는 없고  DOM 노드 프로퍼티 안에다가 어떠한 값을 넣었을 때 에러가 발생할 경우 이 상황을 떠올릴 수 있으면 된다. 



```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <table>
      <tr>
        <!-- colspan 프로퍼티는 존재하지 않기 때문에 어튜리뷰트 바인딩을 사용한다. -->
        <td [attr.colspan]="length">A + B</td>
      </tr>
      <tr>
        <td>C</td><td>D</td>
      </tr>
    </table>
  `,
  styles: [`
    table, td {
      width: 200px;
      border: 1px solid black;
      text-align: center;
    }
  `]
})
export class AppComponent {
  length = 2;
}
```



### 3.4 클래스 바인딩(Class binding)

클래스를 만들어 놓고 그 클래스를 불러올 수 있거나 하는 것. 

```
<element [class.class-name]="booleanExpression">...</element>
// 클래스 하나만 적용할 때 사용하면 좋음.
<element [class]="class-name-list">...</element>
// 여러개의 클래스를 적용할 수 있지만 이 방법 보다는 ngClass를 사용하는 것이 좋다. 
```





```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <!-- 조건의 의한 클래스 바인딩
         우변의 표현식("isLarge")이 true이면 클래스를 추가한다 -->
    <div [class.text-large]="isLarge">text-large</div>
    <!-- 조건의 의한 클래스 바인딩
         우변의 표현식이 false이면 클래스를 삭제한다 -->
    <div class="text-small color-red" [class.color-red]="isRed">text-small</div>
// 뒤에 color-red 가 false이므로 앞에 color-red가 병합되워 지워진다.
    <!-- 여러개의 클래스를 한번에 지정할 수 있다 -->
    <div [class]="myClasses">text-large color-red</div>
    <!-- 클래스 바인딩은 기존 클래스 어트리뷰트보다 우선한다.
         따라서 기존 클래스 어트리뷰트는 클래스 바인딩에 의해 reset된다.
         클래스 바인딩의 위치는 관계없다. -->
    <div class="text-small color-blue" [class]="myClasses">text-large color-red</div>
// 앞에 싹 지우고 뒤에 쓴 것을 적용된다. 
  `,
  styles: [`
    .text-small { font-size: 18px;}
    .text-large { font-size: 36px;}
    .color-blue { color: blue;}
    .color-red { color: red;}
  `]
})
export class AppComponent {
  isLarge = true;
  isRed = false;
  // 클래스 바인딩은 문자열을 바인딩한다.
  myClasses = 'text-large color-red';
}
```



### 3.5 스타일 바인딩(Style binding)

```
element [style.style-property]="expression">...</element>
```

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <button class="btn"
      [style.background-color]="isActive ? '#4CAF50' : '#f44336'"
// 반드시 값을 주어야 한다. 주로 3항 연산자로 많이 사용된다.
      [style.font-size.em]="isActive ? 1.2 : 1"
      (click)="isActive=!isActive">Toggle</button>
// 할당하지 말아야 하지만 여기서는 된다. 이벤트 바인딩은 statement이기 때문에 가능하다. 
   누를때 마다 결과 반전. 컬러도 폰트 사이즈도 계속 바뀐다. 
  `,
  styles: [`
    .btn {
      background-color: #4CAF50;
      border: none;
      border-radius: 8px;
      color: white;
      padding: 10px;
      cursor: pointer;
      outline: none;
    }
  `]
})
export class AppComponent {
  isActive = false;
}
```



### 3.6 이벤트 바인딩(Event binding)

템플릿에서 컴포넌트 클래스로 넘어감.

```
<element (event)="statement">...</element>
```





```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <!-- (1) -->
    <input type="text" [value]="name" (input)="onInput($event)">
// "name"은 프로퍼티를 넣어주라는 것이지 문자열을 말하는 것이 아니다. onClick()에서 사용하려고 바인딩 해놓은 것이다. 글씨가 보이는 것만 원한다면 구지 바인딩해주지 않아도 된다. 
// ($event) 이것이 이밴트 객체. 자바스크립트에서 (e).
    <!-- (2) -->
    <button (click)="onClick()">clear</button>
    <!-- (3) -->
    <p>name: {{ name }}</p>
  `
})
export class AppComponent {
  name = '';
  선언과 동시에 할당이 이루어지므로 string이라고 따로 기입하지 않아도 된다. 

  onInput(event) {
    console.log(event);
    // event.target.value에는 사용자 입력 텍스트가 담겨있다.
    this.name = event.target.value;
// 이벤트를 일으킨 요소의 현재 값.
  }

  onClick() {
    this.name = '';
  }
}
```



### 3.7 양방향 데이터 바인딩(Two-way binding)

```
<element [(ngModel)]="property">...</element>
```

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <input type="text" [(ngModel)]="name">
// 뭔가 상태값을 가지고 있는 애들한테만 사용할 수 있다. 입력할 수 있는 것.
// 약간 위화감이 있는 독특한 문법. 
    <p>name: {{ name }}</p>
  `
})
export class AppComponent {
  name = '';
}
```





# 7. Angular Component - Built-in directive



## 1. 빌트인 디렉티브(Built-in directive)란?

디렉티브(Directive / 지시자)는 “DOM의 모든 것(모양이나 동작 등)을 관리하기 위한 지시(명령)”이다.

밑에 예제는 일단 만드는 방법. 나중에 만들게 된다. 

```
import { Directive, ElementRef, Renderer2 } from '@angular/core';

@Directive({
  selector: '[textBlue]'
})
export class TextBlueDirective {
  constructor(el: ElementRef, renderer: Renderer2) {
    renderer.setStyle(el.nativeElement, 'color', 'blue');
  }
}
```

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <div textBlue>textBlue directive</div>
// div에 텍스트 블루로 바꿔줘가. 왜 컴포넌트에서 안하고 디렉티브를 할까? 
예를 들어서 다른 컴포넌트 에서도 텍스트를 블루로 바꿔줘야 하는 일이 있다면 이 행위를 디렉티브로 빼서 관리하면 편리하다.
  `
})
export class AppComponent { }
```



## 2. 빌트인 어트리뷰트 디렉티브(Built-in attribute directive)

### 2.1 ngClass

이것을 얘기할 때는 학상 복수개 라고 떠올리면 된다. 

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <ul>
      <!-- 문자열에 의한 클래스 지정  -->
      <li [ngClass]="stringCssClasses">bold blue</li>
      <!-- 배열에 의한 클래스 지정  -->
      <li [ngClass]="ArrayCssClasses">italic red</li>
      <!-- 객체에 의한 클래스 지정  -->
      <li [ngClass]="ObjectCssClasses">bold red</li>
      <!-- 컴포넌트 메소드에 의한 클래스 지정 -->
      <li [ngClass]="getCSSClasses('italic-blue')">italic blue</li>
    </ul>
  `,
  styles: [`
    .text-bold   { font-weight: bold; }
    .text-italic { font-style: italic; }
    .color-blue  { color: blue; }
    .color-red   { color: red; }
  `]
})
export class AppComponent {
  state = true;

  // 문자열 클래스 목록
  stringCssClasses = 'text-bold color-blue';
  // 배열 클래스 목록
  ArrayCssClasses = ['text-italic', 'color-red'];
  // 객체 클래스 목록 (가장 일반적인 방법)
  ObjectCssClasses = {
    'text-bold': this.state,
    'text-italic': !this.state,
    'color-blue': !this.state,
    'color-red': this.state
  };

  // 클래스 목록을 반환하는 컴포넌트 메소드
  getCSSClasses(flag: string) {
    let classes;
    if (flag === 'italic-blue') {
      classes = {
        'text-bold': !this.state,
        'text-italic': this.state,
        'color-red': !this.state,
        'color-blue': this.state
      };
    } else {
      classes = {
        'text-bold': this.state,
        'text-italic': !this.state,
        'color-red': this.state,
        'color-blue': !this.state
      };
    }
    return classes;
  }
}
```



### 2.2 ngStyle



```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <div>
      Width: <input type="text" [(ngModel)]="width">
      <button (click)="increaseWidth()">+</button>
      <button (click)="decreaseWidth()">-</button>
    </div>
    <div>
      Height: <input type="text" [(ngModel)]="height">
      <button (click)="increaseHeight()">+</button>
      <button (click)="decreaseHeight()">-</button>
    </div>
    <button (click)="isShow=!isShow">{{ isShow ? 'Hide' : 'Show' }}</button>
    <!-- 스타일 지정  -->
    <div
      [ngStyle]="{
        'width.px': width,
        'height.px': height,
        'background-color': bgColor,
        'visibility': isShow ? 'visible' : 'hidden'
// true이면 visible이라는 버튼을 보여주게 해라.
      }">

// 항상 쌍 따옴표 안에 들어와야 한다. [ngStyle]로 묶어준 상태.
    </div>
  `
})
export class AppComponent {
  width = 200;
  height = 200;
  bgColor = '#4caf50';
  isShow = true;

  increaseWidth()  { this.width  += 10; }
  decreaseWidth()  { this.width  -= 10; }
  increaseHeight() { this.height += 10; }
  decreaseHeight() { this.height -= 10; }
}
```



## 3. 빌트인 구조 디렉티브(Built-in structural directive)

구조 디렉티브는 DOM 요소를 **반복 생성(ngFor)**, 조건에 의한 **추가 또는 제거를 수행(ngIf, ngSwitch)**을 통해 뷰의 구조를 변경한다.

- 구조 디렉티브에는 `*` 접두사를 추가하며 `[]`을 사용하지 않는다.

- 하나의 호스트 요소(디렉티브가 선언된 요소)에는 하나의 구조 디렉티브만을 사용할 수 있다.

  ngFor와 ngIf를 한꺼번에 사용하지 못한다. 



### 3.1 ngIf

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <!-- ngIf에 의한 show/hide -->
    <p *ngIf="isShow">Lorem ipsum dolor sit amet</p>
// isShow가 false인 경우 DOM요소에서 완전히 제거! 퍼포먼스에 훨씨 유리하다. 

    <!-- 스타일 바인딩에 의한 show/hide -->
    <p [style.display]="isShow ? 'block' : 'none'">Lorem ipsum dolor sit amet</p>
// 스타일 바인딩 구현: display: none이 되어도 DOM상에 남아있다. 

    <button (click)="isShow=!isShow">{{ isShow ? 'Hide' : 'Show' }}</button>
  `,
  styles: [`
    p { background-color: #CDDC39; }
  `]
})
export class AppComponent {
  isShow = true;
}
```

Angular 4부터 `ngIf else`가 추가되었다.

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <div>
      <input type="radio" id="one" name="skill"
            (click)="mySkill=$event.target.value" value="HTML">
      <label for="one"> HTML</label>
      <input type="radio" id="two" name="skill"
            (click)="mySkill=$event.target.value" value="CSS">
      <label for="two"> CSS</label>
    </div>

    <!-- 참인 경우, 별도의 ng-template를 사용하지 않는 방법  -->
    <div *ngIf="mySkill==='HTML'; else elseBlock">HTML</div>
    <ng-template #elseBlock><div>CSS</div></ng-template>

    <!-- 참인 경우, 별도의 ng-template를 사용하는 방법  -->
    <div *ngIf="mySkill==='HTML'; then thenBlock_1 else elseBlock_1"></div>
    <ng-template #thenBlock_1><div>HTML</div></ng-template>
    <ng-template #elseBlock_1><div>CSS</div></ng-template>
  `
})
```

### 3.2 ngFor



```
import { Component } from '@angular/core';

interface User {
  id: number;
  name: string
}

@Component({
  selector: 'app-root',
  template: `
    <!-- user를 추가한다 -->
    <input type="text" #name placeholder="이름을 입력하세요">
    <button (click)="addUser(name.value)">add user</button>
    <ul>
      <!-- users 배열의 length만큼 반복하며 li 요소와 하위 요소를 DOM에 추가한다 -->
      <li *ngFor="let user of users; let i=index">
      // 여기서 users는 밑에 배열 users 배열을 가르킨다. 
      // index는 반드시 변수에 담아서 사용해야 한다. 
        {{ i }}: {{ user.name }}
        <!-- 해당 user를 제거한다 -->
        <button (click)="removeUser(user.id)">X</button>
      </li>
    </ul>
    <pre>{{ users | json }}</pre>
  `
})
export class AppComponent {
  users: User[] = [
    { id: 1, name: 'Lee' },
    { id: 2, name: 'Kim' },
    { id: 3, name: 'Baek' }
  ];
  // DOM적으로 늘어나거나 줄어들 수 있다. 순회 가능한 배열. 

  // user를 추가한다
  addUser(name: string) {
    if (name) {
      this.users.push({ id: this.getNewUserId(), name });
    }
  }

  // 해당 user를 제거한다.
  removeUser(userid: number) {
    this.users = this.users.filter(({ id }) => id !== userid);
  }

  // 추가될 user의 id를 반환한다
  getNewUserId(): number {
    return this.users.length ? Math.max(...this.users.map(({ id }) => id)) + 1 : 1;
  }
}
```

### 3.3 ngSwitch

많이 사용하지 않는다. 