Box Model은 웹 페이지의 요소(Elements)가 어떻게 레이아웃되고 표현되는지 정의하는 중요한 개념이다. CSS 박스 모델은 각 HTML 요소를 상자로 취급하며, 이 상자는 여러 가지 속성에 의해서 정의된다.

## 구성요소

![[Pasted image 20231029185502.png]]
### Content

> 요소의 실제 내용이 위치하는 영역을 나타냄. 텍스트, 이미지, 또는 다른 요소의 내용이 이 부분에 들어감.

### Padding

> Content 주변의 내부 여백으로, Content와 Border 사이에 위치함. Padding은 요소의 내용과 Border 사이의 공간을 조절하며, 'padding'이라는 속성을 사용하여 조절할 수 있다.

### Border

> Padding 주변에 위치하며, 요소의 외곽을 둘러싸는 테두리이다. 테두리는 주로 'border'속성을 사용하여 스타일링하며, 두께, 스타일, 색상 등을 지정할 수 있다.

### Margin

>Border 주변의 외부 여백으로, 요소와 다른 요소 사이의 간격을 조절한다. 'margin'속성을 사용하여 마진 조절이 가능하며, 주로 요소 사이의 간격을 조절하는데 사용된다.


```css
div{
	width: 200px; /* 가로 너비*/
	height: 100px; /*세로 높이*/
	padding: 20px; /*내부 여백*/
	border: 2px solid #000 /* 테두리 */
	margin: 10px; /*외부 여백*/
}
```