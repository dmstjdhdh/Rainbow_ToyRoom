BOM과 DOM은 웹 브라우저와 웹 페이지 구조 및 동작을 다루기 위한 중요한 개념이다.

## BOM (Browser Object Model)

BOM은 웹 브라우저의 창 또는 탭과 같은 브라우저의 요소에 접근하고 제어하기 위한 객체 모델이다. 이는 웹 페이지의 외부 요소와 상호 작용하는 데 사용된다. 다음과 같은 객체들이 있다.

 - window: 브라우저 창이나 탭을 나타내는 객체. 브라우저 창의 크기, 위치, 열고 닫기, 경고 메시지 표시 등을 제어할 수 있음. BOM의 최상위 객체이며, 전역 객체로 간주된다. 모든 BOM 객체는 window 객체의 프로퍼티로 포함이 된다.

```javascript
window.resizeTo(800, 600); //창의 너비와 높이 변경

window.alert("당장 이 웹사이트에서 나가!") // 경고 메시지를 브라우저 창에 표시

var newWindow = window.open("https:/www.github.com", "_blank"); // 새 창 열기

window.close(); // 현재 창 닫기
```

 - navigator: 브라우저 정보를 제공하는 객체로, 사용 중인 브라우저에 대한 정보를 얻을 수 있음. 예를 들어, 브라우저의 이름, 버전 및 플랫폼 정보 확인이 가능하다.

```javascript
//브라우저 이름
var browserName = navigator.appName;
//브라우저 버전
var browserName = navigator.appVersion
```

 - location: 현재 웹 페이지의 URL 정보를 다루는 객체이다.
 
```javascript
// 현재 페이지 URL
var currentURL = window.location.href;

// 다른 페이지로 이동
window.location.href = "https://www.example.com";
```

 - screen: 사용자의 화면 정보를 다루는 객체로, 화면 해상도 및 색상 깊이 등을 확인할 수 있다.
 
```javascript
//화면의 width와, height를 확인
var screenWidth = window.screen.width;
var screenHeight = window.screen.height;
```

 - history: 브라우저의 탐색 히스토리를 다루는 객체로, 앞으로 가기, 뒤로 가기 등을 통해 페이지를 제어할 수 있다.
 
```javascript
//뒤로 가기
window.history.back();
//앞으로 가기
window.history.forward();
```

 - document: document 객체는 DOM(Document Object Model)의 일부로, 현재 웹 페이지의 구조와 내용을 다룬다. 이 객체를 사용해서 HTML 요소에 접근이 가능하고, 조작이 가능하다.
 
```javascript
//DOM을 이용해서 HTML 요소에 접근하기
var headingElement = document.getElementById("my-heading");
headingElement.textContent = "새로운 제목";
```

## DOM(Document)

DOM은 웹 페이지의 구조와 내용을 다룰 수 있도록 하는 모델로, 웹 페이지의 HTML 또는 XML문서를 트리 구조로 표현할 수 있다. 각 HTML 요소는 DOM에서 노드로 나타내며, 이러한 노드를 조작해서 웹 페이지의 내용을 변경하거나 업데이트할 수 있다.

HTML 구조 예제:
```html
<html>
<head>
	<title>예제</title>
</head>
<body>
	<h1 id="h1-example"> 예제 h1 태그 </h1>
	<button id = "button-example">변경 버튼</button>
</body>
</html>
```

JavaScript 코드 예제:
```javascript
//문서 로드 이후 시행되는 코드
document.addEventListener("DOMContentLoaded", function() {
	//버튼 요소와 헤딩 요소에 대해서 참조를 얻는 방식
	var button = document.getElementById("button-example");
	var heading = document.getElementById("h1-example");

	//버튼 클릭시에 헤딩의 텍스트가 변경되는 이벤트 추가
	button.addEventListner("click", function() {
		heading.textContent = "텍스트가 변경되었습니다.";
	})
});
```