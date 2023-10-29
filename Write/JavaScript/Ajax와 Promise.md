
## Ajax란 무엇인가?

Ajax는 "Asynchronous JavaScript and XML"의 약자이다.

**Asynchronous**: 비동기

웹 페이지에서 비동기적으로 데이터를 교환하고 화면을 업데이트 하기 위한 웹 개발 기술이다. Ajax를 사용하면 웹 페이지를 새로 고치지 않아도 서버와 통신이 가능하며, 데이터를 가져오거나 보낼 수 있다.

비동기적으로 JS를 사용해서 데이터를 받아와 동적으로 DOM을 갱신 및 조작하는 방식이다.

## 동작하는 방식

 1. 사용자가 AJAX가 적용된 UI랑 상호작용을 함.
 2. 서버에 AJAX 요청을 보냄.
 3. 서버는 DataBase에서 데이터를 가져옴
 4. JS파일에 정의되어 있는 대로 DOM 객체를 업데이트함.

이 업데이트 방식은 페이지 전부 로딩이 아닌, 일부만 업데이트하는 방식이다.

>무한 스크롤, 자동 완성 검색 등의 기능 구현에 자주 사용되는 방식이다.


## 사용법

### XMLHttpRequest

XMLHttpRequest를 이용하면, 이를 통해 생성된 인스턴스의 open(), send() 등의 메소드를 이용할 수 있다.

```javascript
// XMLHttpRequest 객체 생성
var myRequest = new XMLHttpRequest();

//요청 설정: GET 요청
myRequest.open(
	"GET",
	"https://jsonplaceholder.typicode.com/posts/1",
);

//요청 보내기
myRequest.send();

//요청이 완료되면 실행되는 이벤트 핸들러
myRequest.onload = function() {
	//status가 200이면, 데이터가 성공적으로 돌아왔다는 것.
	if(myRequest.status == 200) {
		var response = JSON.parse(myRequest.responseText);
		var resultDiv = document.getElementById('result');
		resultDiv.innterHTML = 'UserID:'+response.userID+'<br>Title:'+response.title;
	} else {
		//오류 처리 로그
		console.log('Request failed with status' + myRequest.status);
	}
}
```

해당 예제에서는, XMLHttpRequest 객체를 생성하고, 서버로 GET요청을 보낸다. 그리고 서버로부터의 응답을 받을 때 'onload' 이벤트 핸들러가 실행된다. 응답이 성공적으로 돌아오면 JSON데이터를 파싱하고, 웹 페이지에 결과를 표시한다.

### Fetch API

fetch api를 사용해서 데이터 요청 또한 가능한데, XMLHttpRequest보다 직관적인 코드를 가지고 있으며, 사용법이 간단하다.

- 'fetch()'함수를 사용하여 서버로 요청을 보내고, 'then()' 메서드를 사용하여 응답을 처리한다.
- Fetch API는 Promise를 사용하여 비동기 작업을 처리한다. (코드가 더 간결해짐)
- 현대 웹 브라우저에서 잘 지원되나, 일부 IE(Internet Explorer) 버전에서 완전히 지원되지 않는 경우도 있다고 한다. 따라서 Fetch API를 사용할 때에는 IE를 고려해야 한다.

```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1")
	.then(response => {
		if(!response.ok) {
			throw new Error('Network response was not ok');
		}
		return response.json();
	})
	.then(data => {
		console.log(data);
	})
	.catch(error => {
		console.error('Fetch error:', error);
	})
```

fetch()함수로 서버에 GET요청을 보내고, 응답을 JSON으로 파싱하여 데이터를 얻는다. 그리고 Promise 체인을 사용해서 성공 및 실패 상황에 대한 처리를 정의할 수 있다.

#### Promise와 then()

_**내가 약속하지...! 너의 코드가 시행이 된다면...!**_

Promise는 JS에서 비동기 작업을 처리하고 조직하는 패턴 및 객체이다. 다음과 같은 특징을 가진다.

1. Promise는 상태 3가지를 가진다.
	- 대기(pending) : 초기 상태, 작업이 성공 또는 실패할 때까지 대기한다.
	- 이행(fulfilled): 작업이 성공적으로 완료되었을 때의 상태로, 결과 값이 존재한다.
	- 거부(rejected): 작업이 실패했을 때의 상태로, 에러 정보가 존재한다.
2. 비동기 작업의 결과: Promise 객체는 비동기 작업의 결과 값을 저장하고, 이후에 해당 결과를 사용할 수 있도록 한다.
3. '.then()' 메서드: Promise 객체는 '.then()' 메서드를 통해 비동기 작업의 성공 및 실패 처리를 정의할 수 있다. '.then()' 메서드는 두 개의 콜백 함수를 인수로 받아, 작업이 성공 했을 때와 실패했을 때 각각 실행된다.

```javascript
const myPromise = new Promise((resolve, reject) => {
	//비동기 작업 수행
	const success = true;

	if(success) {
		resolve("성공했습니다.");
	} else {
		reject("실패했습니다.");
	}
});

myPromise.then(
	result => {
		console.log("성공 메세지는?:", result);
	}
	error => {
		console.error("실패 메세지는?:", error);
	}
)
```

### 조심해야할 점

- 지원하지 않는 브라우저가 있다는 점.
- 페이지 전환 없이 서버와 통신하기 때문에 보안상 문제가 생길 수 있음.
- 무분별하게 사용하면, 서버의 부하가 늘어날 수 있음.