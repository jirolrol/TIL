18.02.28(수)

# 1. Sass Basics 

Sass는 CSS의 확장이다. 하지만 표준은 아니다. 

[Sass(Syntactically Awesome StyleSheets)](http://sass-lang.com/)는 CSS pre-processor(전처리기)이다. 

 pre-porecessor란??

foo.scss 이대로 브라우져에 내보내면 브라우저는 모른다. 

이것을  컴파일 or 트랜스파일링  해서 foo.css 로 만들어야 한다. 엄밀히 말하면 트랜스파일링이 맞다. 



일일히 트랜스파일링 하지 말고 한 번에 해주는 것이 webpack 이다. 



CSS 의 단점?

- CSS도 스코프가 있는데 기본적으로 전역이다. 상속과 캐스캐이딩에 의해서 결정된다.  심지어 캐스캐이딩 점수 따지는 것 까지 하면 직관적으로 이해하기 어렵다. 

- 코딩 레벨의 차이가 나는 사람들끼리 작업을 할 때 잘 하는 사람들 기준이 아니라 밑에 사람이 하는 레벨로 끝난다. 평균이 아니다. 어떤 방법을 선택해야 하는가? 잘 하는 사람들이 못하는 사람들을 가르쳐줘야 하는데 그것이 안된다. 따라서 약각의강제성의 툴을 대입해서 작업하는 것이 좋다. 

  —> 제일 잘 하는 사람들은 좀 어려운 부분을 맡아서 공통사용 부분을 만들어 준다. 

   	중간 레벨 사람들이 가장 많은 일들을 하게된다. 노가다성 일.

  ​	신입은 실수의 연속. 어떤식으로 작업하는게 좋을까? 잘 하는 사람들이 만든 모듈을 적극 사용하여서 작업한다. 

  어떤 작업이든 필요한 공통 부분은(잘 하는 사람들이 만들어야 하는 부분)??

  - 로그인 하는 부분

  - 데이터 베이스에 접근하는 기능

  - 데이터 베이스에서 가지고 오는 기능 

    Sass도 이런 공통 부분을 만드는 기능이 있다. (mixin)



Sass는 다음과 같은 추가 기능과 유용한 도구들을 제공한다.

- 변수의 사용
- 조건문과 반복문
- Import
- Nesting
- Mixin
- Extend/Inheritance



CSS와 비교하여 Sass는 아래와 같은 장점이 있다.

- CSS보다 심플한 표기법으로 CSS를 구조화하여 표현할 수 있다.
- **스킬 레벨이 다른 팀원들과의 작업 시 발생할 수 있는 구문의 수준 차이를 평준화할 수 있다.**
- CSS에는 존재하지 않는 Mixin 등의 강력한 기능을 활용하여 CSS 유지보수 편의성을 큰 폭으로 향상시킬 수 있다.



## 2. Install

Sass는 2006년 Ruby로 처음 개발되었고 이후 다양한 포팅 버전이 등장했다. 

mac은 기본적으로 Ruby가 깔려져 있지만 pc에는 Ruby가 깔려있지 않아서 node를 이용할 것.



node-sass	4.7.2 (major.minor.fix)

break-change: 맨 앞을 올린다. 바뀔 때 굉장히 신중해야 한다. 올리면 부작용 같은걸 고려해야 한다. 



### 2.3 GUI App

Sass작업을 많이 하는 사람들은 사용하면 좋다. 프론트엔드에서는 많이 사용하지 않음.



## 3. Command

### 3.1 version

```
$ node-sass -v
node-sass 4.7.2 (Wrapper) [JavaScript]
libsass   3.5.0.beta.2  (Sass Compiler) [C/C++]

-v shortcut
--v 
```

### 3.2 compile

```
$ cd my-project

## 특정 파일을 특정 파일 이름으로 컴파일

## Compile foo.scss to bar.css

$ node-sass foo.scss > bar.css

## 폴더 내의 모든 파일을 컴파일
## node-sass input-folder-path -o output-folder-path
$ node-sass src/sass --output dist/css
// src 내에는 sass ts도 있을 수 있다. 앞으로 모든 sass 파일은 src폴더에 넣어 놓아라. 
// 컴파일한 모든 파일은 dist폴더에 넣어 놓아라. 이곳에는 css 파일이 들어가게 된다. 
// 단점은 여기에 있는 파일 하나를 바꾸면 매번 해주어야 한다. 따라서 watch를 써준다. 

```

### 3.4 watch

watch command는 scss 파일의 변경을 감지하여 변경될 때마다 scss 파일을 컴파일하여 css 파일을 자동 업데이트한다.

**파일 단위의 watch**

```
$ cd my-project

## watch src/sass/foo.scss -> dist/css
$ node-sass --watch src/sass/foo.scss --output dist/css
```

**디렉터리 단위의 watch**

```
$ cd my-project

## watch src/sass -> dist/css
$ node-sass --watch src/sass --output dist/css
// 계속 watch 하고 있는 상태. 무언가 바뀌면 돌려줘야 하니까.
```



## 3.4 style

**expanded**

표준적인 스타일의 css 파일이 생성된다.

```
$ node-sass --output-style expanded src/sass --output dist/css
```



**compressed**

가능한 빈공간이 없는 압축된 스타일의 css 파일이 생성된다.

결국은 서버에 compressed로 올려 놓아야 한다. 

```
$ node-sass --output-style compressed src/sass --output dist/css
```



## 4. SASS vs. SCSS

Sass는 SASS 표기법(.sass)과 SCSS 표기법(.scss)이 있다. .scss 가 css와 조금 더 가깝다. 

|             | SCSS     | SASS                                           | CSS    |
| ----------- | -------- | ---------------------------------------------- | ------ |
| 중괄호 {}   | 필요     | 불필요（공백 2문자 들여쓰기가 코드블록을 의미) | 필요   |
| 세미콜론 ;  | 필요     | 불필요                                         | 필요   |
| : 뒤의 공백 | 불필요   | 필요                                           | 불필요 |
| Mixin       | @mixin   | =                                              | 없음   |
| Include     | @include | +                                              | 없음   |
| 확장자      | .scss    | .sass                                          | .css   |



# 2. SassScript

## 1. Data Type

SassScript가 제공하는 자료형은 7가지가 있다.



숫자형

e.g) 1.2, 13, 10px

문자열

CSS는 2종류의 문자열을 사용할 수 있다. 따옴표를 사용하는 경우(“Lucida Grande”, ‘http://sass-lang.com’)와 사용하지 않는 경우(bold, sans-serif)가 있다. Sass는 2종류의 문자열 모두를 인식할 수 있으며 컴파일 후의 CSS에는 Sass에서 사용한 문자열이 그대로 출력된다. e.g. “Lucida Grande”, ‘http://sass-lang.com’, sans-serif

---> 폰트 이름 자체에 스페이스가 있으면 따옴표로 묶어줘야 한다. 

컬러

e.g. blue, #04a3f9, rgba(255, 0, 0, 0.5)

—> 대표적인 것이 키워드로 나타내기. 하지만 정교한 색으로 표현하기 어렵다. 

​       16진수의 rgb값을 주어 앞에 #을 붙여준다. 

​	rgba의 a 는 투명도(alpha)	

boolean

e.g. true, false

null

프로퍼티 값에 값이 null인 변수가 지정되면 해당 룰셋은 출력되지 않는다.

—> 출력을 아예 안한다. 

list

margin과 padding 프로퍼티값 지정에 사용되는 0 auto와 font-family 프로퍼티값 지정에 사용되는 Helvetica, Arial, sans-serif 등은 공백 또는 콤마 구분된 값의 list이다. e.g. 1.5em 1em 0 2em, Helvetica, Arial, sans-serif

—> 순서가 의미있는 것. 배열과 비슷하다고 생각하면된다.

map

JSON과 유사한 방식으로 `map-get` 함수를 사용하여 원하는 값은 추출할 수 있다. e.g. (key1: value1, key2: value2)

—> 객체와 비슷하다. 

```
// map
$foundation-palette: (
  primary: #E44347,
  mars: #D7525C,
  saturn: #E4B884,
  neptune: #5147D7
);

.mars {
  color: map-get($foundation-palette, mars);
}
```

Data type은 Built-in function [type-of](http://poiemaweb.com/sass-built-in-function#21-data-type-%EC%B7%A8%EB%93%9D)으로 취득할 수 있다.



## 2. 변수

변수명은 `$`로 시작한다.

```
$site_max_width: 960px; // 고정폭으로 갈 때
$font_color: #333;
$link_color: #00c;
$font_family: Arial, sans-serif;
$font_size: 16px;
$line_height: percentage(20px / $font_size); // 빌트인 함수. 퍼센트로 계산하는 것.

----- variable 파일

body {
  color: $font_color;

  // Property Nesting
  font: {
     size: $font_size;
     family: $font_family;
  }

  line-height: $line_height;
}

# main {

  width: 100%;
  max-width: $site_max_width;
}
----- 룰셋파일
원래는 variable 파일과 룰셋 파일은 따로 관리한다. 
```

```
body {
  color: #333;
  font-size: 16px;
  font-family: Arial, sans-serif;
  line-height: 125%;
}

# main {

  width: 100%;
  max-width: 960px;
}

// 이것이 더 쉬워보이지만 sass를 쓰면 유지 보수가 쉽다. 따라서 간단한 css는 sass 사용하지 않는 것이 좋다.
```



## 3. 변수의 Scope

```
변수에는 유효범위(scope)가 존재한다.

$width: 960px; // global variable

header {
  width: $width;
  margin: 0 auto;
}

# main {

  $color: #333; // local variable
  width: $width;
  margin: 20px auto;
  section {
    p {
      color: $color;

      a:link {
        color: $color;
      }
    }
  }
}

footer {
  width: $width;
  margin: 0 auto;
  color: $color; // 컴파일 에러
}
```

```
# main {

  $color: #333 !global; // global variable
  width: $width;
  ...
```

!global ---> 지역변수를 전역변수로 변환할 수 있다. 



## 4. 연산자(Operation)$width: 100px;

```
$width: 100px;

# foo {

  width: $width + 10; // 110px 
  // 항상 좌항이 기준. 따라서 
}

# bar {

  width: $width + 10in; // 1060px
}
```



```
$width: 100px;

# foo {

  width: $width + 10em; // NG: 100px + 10em
}

// sass는 계산하지 못한다. 브라우저는 계산할 수 있다. 
```

```
# foo {

  width: calc(25% - 5px);
}
// css 함수 calc()를 사용한다. 
```

```
p {
  /*
    font: font-style font-variant font-weight font-size/line-height font-family
  */
  font: italic bold 12px/30px Georgia, serif;
}
```

12px/30px를 나누면 안된다. 그럼 언제  '/' 를 나누기로 인식할까?

```
p {
  // font와 border-radius의 '/'는 CSS문법에 맞는 표현이므로 연산되지 않는다.
  font: italic bold 12px/30px Georgia, serif;
  // 타원형 둥근 모서리
  border-radius: 10px 20px/20px;
  /*
  border-top-left-radius: 10px 20px;
  border-top-right-radius: 20px;
  border-bottom-right-radius: 10px 20px;
  border-bottom-left-radius: 20px;
  */

  $width: 1000px;

  width: $width / 2;            // 변수에 대해 사용 →　width: 500px;
  height: (500px / 2);          // 괄호 내에서 사용 →　height: 250px;
  margin-left: 5px + 8px / 2px; // 다른 연산의 일부로서 사용 →　margin-left: 9px;
}
```

변수를 CSS의 /와 함께 사용하고자 하는 경우 `#{}`(Interpolation)를 사용한다.p {

```
  $font-size: 12px;
  $line-height: 30px;
  font: #{$Extra close brace or missing open bracefont-size}/#{$line-height};  // 12px/30px
}
```

### 4.2 컬러 연산자

모든 산술 연산자는 컬러 값에도 사용할 수 있다.

```
p {
  color: #010203 + #040506;
  // R: 01 + 04 = 05
  // G: 02 + 05 = 07
  // B: 03 + 06 = 09
  // => #050709
}

p {
  color: #010203 * 2;
  // R: 01 * 2 = 02
  // G: 02 * 2 = 04
  // B: 03 * 2 = 06
  // => #020406
}

p {
  color: rgba(255, 0, 0, 0.75) + rgba(0, 255, 0, 0.75);
  // alpha 값은 연산되지 않는다
  // color: rgba(255, 255, 0, 0.75);
}
```

alpha값을 계산하고 싶다면 함수를 사용한다. 

```
$translucent-red: rgba(255, 0, 0, 0.5);

p {
  color: opacify($translucent-red, 0.3);
  // => color: rgba(255, 0, 0, 0.8);

  background-color: transparentize($translucent-red, 0.25);
  // => background-color: rgba(255, 0, 0, 0.25);
}
```

### 4.3 문자열 연산자

따옴표가 있는 문자열과 없는 문자열을 함께 사용하는 경우, 좌항의 문자열을 기준으로 따옴표를 처리한다.

```
p:before {
  content: "Foo " + Bar;        // "Foo Bar" 항상 좌항 기준이다. 
  font-family: sans- + "serif"; // sans-serif
}
```



### 4.4 불린 연산자

대부분 if 문에서 사용한다. 



### 4.5 리스트 연산자



## 5. 함수

다 정리할 수 없으니 참고할 것!



## 6. Interpolation: #{}

인터폴레이션은 변수의 값을 문자열 그대로 삽입한다.



## 7. Ampersand(&) ** 중요

`&`는 부모요소를 참조하는 셀렉터이다.

```
a {
  color: #ccc;

  &.home {
    color: #f0f;
  }

  &:hover {
    text-decoration: none;
  }

  // & > span (X)

> span {
>   color: blue;
> }
// > 는 자식이라는 의미. 
  span {
    color: red;
  }
}
```



# 3. CSS Extensions

## 1. Nesting

Sass의 유용한 확장 기능으로 선언을 중첩(Nesting)하는 것이다.

```
css
# navbar {

  width: 80%;
  height: 23px;
}

# navbar ul {

  list-style-type: none;
}
// navbar id를 가지고 있는 요소이 후손 중에 ul 요소에 이 스타일을 적용하라는 뜻.

# navbar li {

  float: left;
}

# navbar li a {

  font-weight: bold;
}
```

```
Sass
# navbar {

  width: 80%;
  height: 23px;

  ul { list-style-type: none; }

  li {
     float: left;
     a { font-weight: bold; }
  }
}
```

하지만 중첩도 결국 한계가 있다. 가독성이 결국 더 떨어지게 되어있다. 다음의 예제 참고. 7단계가 들어간다. 

```
// Bad case
div#main {

# sidebar {

# navbar {

      width: 80%;
      height: 23px;

      aside {
        div {
          ul {
            list-style-type: none;

            li {
              float: left;

              a {
                font-weight: bold;
              }
            }
          }
        }
      }
    }
  }
}
```

부모요소의 참조가 필요한 경우 `&`를 사용한다. 예를들어 :hover 또는 ::before 등의 [가상 클래스 선택자 (Pseudo-Class Selector)](http://poiemaweb.com/css3-selector#7-%EA%B0%80%EC%83%81-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%85%80%EB%A0%89%ED%84%B0-pseudo-class-selector)를 지정하는 경우 부모요소의 참조가 필요하다.

```
.myAnchor {
  color: blue;

  // .myAnchor:hover
  &:hover {
     text-decoration: underline;
  }

  // .myAnchor:visited
  &:visited {
     color: purple;
  }
}
```

Nesting은 프로퍼티에도 사용할 수 있다.

```
.funky {
  font: {
    family: fantasy;
    size: 30em;
    weight: bold;
  }
}
// 결국 font 3번 쓰기 싫다는 소리.
```

위 코드의 컴파일 결과는 아래와 같다.

```
.funky {
  font-family: fantasy;
  font-size: 30em;
  font-weight: bold;
}
```



## 8. !default

이미 값이 할당되어 있는 변수에 !default flag를 사용하면 적용되지 않는다.

```
$content: "First content";
$content: "Second content?" !default; // 값이 없을 때에만 이것을 사용한다.
$new_content: "First time reference" !default;

#main {
  content: $content; // "First content"
  new-content: $new_content; // "First time reference"
}
```

이러한 특성은 [partial](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#Partials__partials)에 매우 유용하다. partial 은 파일을 쪼개는 방법. 

여기서 partial 정리!



![partial](/Users/mac/Documents/dev/TIL/partial.png)

partial 폴더 안 sass 파일은 반드시 앞에 언더바 '_' 를 붙인다. 묶어주는 @import 문만(순서가 유 의미) 있는 파일이 있어야 한다. 여기서는 style.scss 

style.scss를 컴파일 하면 해준다. 

이렇게 진행하면 분업도 쉬워진다. 찾아가기가 쉬워서 유지보수에도 좋다. 



```
// _font.scss
$font-size: 16px !default;
$line-height: 1.5 !default;
$font-family: "Helvetica Neue", "Helvetica", "Arial", sans-serif !default;

body {
  font: #{$font-size}/$line-height $font-family;
}

// main.scss
$font-family: "Lucida Grande", "Lucida Sans Unicode", sans-serif;

@import "font";
// 결국 밑에 적용한 font-family가 먹힌다. 
```



### 2.2 @extend

결론적으로 말하면 사용 금지.

합리적으로 맘대로 풀이한다. 우리의 예측과 다를 수 있다.



### 3.3 @for

```
@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}

```

컴파일 결과는 아래와 같다.

```
.item-1 {
  width: 2em;
}
.item-2 {
  width: 4em;
}
.item-3 {
  width: 6em;
}
```



## 4. Mixin

룰셋을 쏟아내는 함수와 같다고 생각하면 된다.

 `@mixin` 선언하고 `@include`로 불러들인다.

```
// 지름이 50px인 원
@mixin circle {
  width: 50px;
  height: 50px;
  border-radius: 50%;
}

// 지름이 50px인 원을 위한 mixin을 include한 후, 배경을 추가 지정
.box {
  @include circle;

  background: #f00;
}
```

@extend와 차이가 없어 보이나 Mixin은 함수와 같이 argument를 사용할 수 있다. (매개변수 주기)

```
@mixin circle($size) {
  width: $size;
  height: $size;
  border-radius: 50%;
}

.box {
  @include circle(100px);

  background: #f00;
}

.box {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  background: #f00;
}
```

Mixin을 사용한 유용한 예제를 살펴보자.

- vendor prefix

```
@mixin vendorPrefix($property, $value) {
  @each $prefix in -webkit-, -moz-, -ms-, -o-, '' {
    #{$prefix}#{$property}: $value;
  }
}

.border_radius {
  @include vendorPrefix(transition, 0.5s);
}

.border_radius {
  -webkit-transition: 0.5s;
  -moz-transition: 0.5s;
  -ms-transition: 0.5s;
  -o-transition: 0.5s;
  transition: 0.5s;
}
```

- position

```
@mixin position($position, $top: null, $right: null, $bottom: null, $left: null) {
  position: $position;
  top: $top;
  right: $right;
  bottom: $bottom;
  left: $left;
}

.box {
  @include position(absolute, $top: 10px, $left: 50%);
}

.box {
  position: absolute;
  top: 10px;
  left: 50%;
}
```