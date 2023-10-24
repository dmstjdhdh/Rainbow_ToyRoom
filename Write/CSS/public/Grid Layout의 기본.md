CSS의 Grid Layout은 페이지를 2차원적으로 여러 주요 영역으로 나누거나 위치와 크기, 문서 계층 구조의 관점에서 HTML 기본 요소로 작성된 컨트롤 간의 관계를 정의하는데 매우 용이하다.

테이블과 동일하게 세로 열과 가로 행을 기준으로 하여, 요소를 정렬할 수 있다.
그렇지만 테이블과는 다르게 CSS의 Grid는 다양한 레이아웃을 훨씬 더 쉽게 구현할 수 있게 한다.


Grid Layout을 만들기 위한 기본적인 HTML 틀은 
```HTML
<div class="container">
<div class="item">1</div>
<div class="item">2</div>
<div class="item">3</div>
<div class="item">4</div>
<div class="item">5</div>
<div class="item">6</div>
<div class="item">7</div>
<div class="item">8</div>
<div class="item">9</div>
</div>
```
위와 같은데, 부모 요소인 div.container를 Grid Container라고 부르고, 자식 요소인 div.item들을 Grid Item이라고 부른다.

컨테이너가 Grid의 영향을 받는 전체 공간이고, 각각 아이템들이 설정된 속성에 따라서 형태로 배치되는 것이다.

## 컨테이너의 기본 설정

- Grid는 컨테이너에 display: grid;를 설정하는 것으로 시작한다.

- 가로 설정하기
   grid-template-columns 속성을 사용해 행을 설정한다.

- 세로 설정하기
   grid-template-rows를 사용해 열을 설정한다.

- 그리드 구역 정하기
   웹디자인에는 header, main, side, footer로 구역이 나누어져 있다. 그리드 레이아웃에서는 이 공간들을 grid-template-areas를 사용해서 정하고 사용할 수 있다. 

예시를 들면
 ```css
   grid-template-areas: 
   "header header header header",
	"main main . sidebar", 
    "footer footer footer footer";
```
이런 식으로 구역을 정하여 알맞게 사용할 수 있다.


## 자녀 요소 설정

- 자녀 요소의 크기는 Grid Layout과 상관없이 따로 정할 수 있다.

- 자녀요소의 넓이와 높이 설정
   grid-column-start와 grid-column-end는 자녀 요소의 넓이를, 
   grid-row-start와 grid-row-end는 자녀 요소의 높이를 설정합니다.
   각각 grid-column과 grid-row로 한번에 설정할 수도 있다.

- grid-area로 설정하기
   grid-template-areas로 구역을 정한 곳을 사용하여 
   ```css
.header { grid-area: header; }
.main { grid-area: main; } 
.sidebar { grid-area: sidebar; } 
.footer { grid-area: footer; }
```
   이런 방식으로 각 자녀 요소에 구역을 설정해 주면 그 구역을 자동으로 채우게 된다.


---
## 용어정리

1. Grid Container
   display :grid를 적용하는 Grid의 전체 영역이다. Grid Container안의 요소들이 Grid 규칙의 영향을 받아 정렬된다.

2. Grid Item
   Grid 컨테이너의 자식 요소들로서, 이것들이 Grid 규칙에 의해 정렬된다.

3. Grid Track 
   Grid의 행 또는 열.

4. Grid Cell 
   Grid의 한 칸을 말하는 것으로, div 같은 실제 HTML 요소는 Grid Item이고, 이런 Grid 아이템 하나가 들어가는 가상의 칸이다.

5. Grid Line
   Grid 셀을 구분하는 선.

6. Grid Number
   Grid Line의 각 번호.

7. Grid Gap
   Grid 셀 사이의 간격.

8. Grid Aria
   Grid Line으로 둘러싸인 사각형 영역이자 Grid Cell의 집합이다.

***

작성자 - hyisu


