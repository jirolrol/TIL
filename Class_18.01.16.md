# CSS 기초 

HTML을 배치 용도로 사용하는 케이스가 있다.

	<Table>
      <tr><th></th></tr>
      <tr><td></td></tr>
      <tr><td></td></tr>
      <tr><td></td></tr>
     </Table>


스타일을 따로 미리 지정하고 필요할 때 원하는 스타일을 적용하면 매우 효율적으로 작업할 수 있다. _그래서 CSS 가 필요하다._ 

    
## Selector 선택방법

하나의 규칙에는 크게 선택자(selector)와 선언부(declaration block)

우선, 누구를 스타일링 할까? 여기서 누구가 selector.

    1. 태그의 이름으로 선택. 이 경우 여러개를 선택하게 될 가능성이 높아진다.
    2. class로 선택하려면 .brand(앞에 점 하나를 찍어 class를 선택)
    3. id로 선택하려면 #logo(앞에 #붙여 id를 선택)

Selector가 선택되면 어떻게 꾸밀지 정하게 된다. 

	selector { 안경:뿔테 }
    
	selector {속성 : 값 ; 속성 : 값}


*하나의 **선언**은 “속성:값”으로 이루어져 있음. 이 경우 안경이 속성, 뿔테가 값. 두가지 선언이 들어가는 경우는 ;로 구분.*


## 웹브라우져별 접두사 

	-webkit-border-radius : 10px ;

	--->webkit 엔진을 사용하고 있는 웹 브라우져에서 사용 가능.


모든 웹 브라우져에 다 적용하고 싶다면?? 
엔진 종류별로 다 적어 주어야 한다.
반복을 싫어하는 개발자들이 이를 편리하게 하기 위해 라이브러리를 사용하지만 성능이 떨어지게 된다. 


## 주석 및 단위

    /*CSS에서 사용할 수 있는 주석입니다.*/

## 상대 단위와 절대 단위

    * px(픽셀)
    * rm
    * rem 
   
    * vw
    * vh
    
    * deg(각도)
    

—> 수업시간에 주로 사용하는 단위.



**색상**

	RGB방식:
    -8진수 방식: rgb(255,0,0)
    -백분율 방식: rgb(100%,0%,0%) 
    -16진수 방식; rgb(FF0000)—> 이렇게 생략도 가능(FF00)
    ---> 모두 RED를 나타냄
    
    RGBA 방식: rgba(255,0,0,.5) 50% 투명도의 빨간색
    HSLA방식: hsla(0, 0%, 100%, 0.5) 색상, 채도, 명도, 투명도
    

**CSS 적용하기**

-External 방식(추천)
-Embedded 방식: 프로젝트에서 아주 일부만 수정해야할 때 사용. 추천 안함
-Inline 방식: 유지보수가 까다로움. 제일 추천 안함. 편해서 개발자들이 자주 사용. 

**CSS Font**

웹에서 기본 폰트 사이즈: 16px
모바일에서 기본 폰트 사이즈: 14px

**글꼴의 종류**

serif(글꼴군): 삐침이 있는 것. 궁서체
sans-serif(글꼴군): 반듯함. 굴림체, 고딕체

# Flexbox

justify-content
* flex-start: 요소들을 컨테이너의 왼쪽으로 정렬합니다.
* flex-end: 요소들을 컨테이너의 오른쪽으로 정렬합니다. 
* center: 요소들을 컨테이너 가운데로 정렬합니다. 
* space-between: 요소들 사이에 동일한 간격을 둡니다. 
* space-around: 요소들 주위에 동일한 간격을 둡니다. 

align-items
* flex-start: 요소들을 컨테이너의 꼭대기로 정렬합니다. 
* flex-end: 요소들을 컨테이너의 바닥으로 정렬합니다.
* center: 요소들을 컨테이너의 세로선 상의 가운데로 정렬합니다.
* baseline: 요소들을 컨테이너의 시작 위치에 정렬합니다.
* stretch: 요소들을 컨테이너에 맞도록 늘립니다. 

flex-direction
* row: 요소들을 텍스트의 방향과 동일하게 정렬합니다. 
* row-reverse: 요소들을 텍스트의 반대 방향으로 정렬합니다.
* column: 요소들을 위에서 아래로 정렬합니다.
* column-reverse: 요소들을 아래에서 위로 정렬합니다. 

*align-self는 개별 요소에 적용할 수 있는 또 다른 속성. 이 속성은 align-itmes가  사용하는 값들을 인자로 받으며, 그 값들은 지정한 요소에만 적용됩니다.*

flex-wrap
 * nowrap: 모든 요소들을 한 줄에 정렬합니다. 
 * wrap: 요소들을 여러 줄에 걸쳐 정렬합니다. 
 * wrap-reverse: 요소들을 여러 줄에 걸쳐 반대로 정렬합니다. 

align-content
 * flex-start: 여러 줄들을 컨테이너의 꼭대기에 정렬합니다.
 * flex-end: 여러 줄들을 컨테이너의 바닥에 정렬합니다. 
 * center: 여러 줄들을 세로선 상의 가운데에 정렬합니다.
 * space-between: 여러 줄들 사이에서 동일한 간격을 둡니다.
 * space-around: 여러 줄들 주위에 동일한 간격을 둡니다.
 * stratch: 여러 줄들을 컨테이너에 맞도록 늘립니다. 

*align-content는 여러 줄들 사이의 간격을 지정하며, align-items는 컨데이너 안에서 어떻게 모든 요소들이 정렬하는지를 지정합니다. 한 줄만 있는 경우, align-content는 효과를 보이지 않습니다. *

연습문제
[flexfroggy](http://flexboxfroggy.com/#ko)
[FlexboxDefense](http://www.flexboxdefense.com/)
[flexbox참고](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
