# Express.js

Node.js환경에서 웹 응용 프로그램을 개발하기 위한 프레임워크 중 하나이다. 주요 특징과 사용 방법에는 다음과 같은 내용이 담길 수 있다.

## 미들웨어

어플리케이션끼리 통신할 수 있도록 하는 소프트웨어를 미들웨어라고 한다. Express js는 미들웨어 시스템이고, HTTP 요청과 응답 사이에서 동작하는 여러 함수의 체인으로 구성된다.

### 미들웨어 동작 방식

미들웨어는 구성 요소 간의 기본 통신 프로세스를 담당한다. 즉, 프런트엔드 애플리케이션은 미들웨어와만 통신하므로 다른 백엔드 소프트웨어 구성 요소의 언어를 배울 필요가 없다.

 - JSON(JavaScript Object Notation)
 - REST(Representational State Transfer) API
 - XML(Extensible Markup Language)
 - 웹 서비스
 - 단순 객체 접근 프로토콜(SOAP)
 
이러한 메시징 프레임워크들은 서로 다른 운영 체제 및 언어의 애플리케이션에 대해 공통 통신 인터페이스를 제공하고, 애플리케이션은 메시징 프레임워크에서 제공하는 표준 형식의 데이터를 쓰고 읽는 방식을 택한다. 

> 참고: AWS에서 설명하는 미들웨어 https://aws.amazon.com/ko/what-is/middleware/

## 라우팅

Express는 HTTP 요청 메서드 (GET, POST, PUT, DELETE 등) 및 URL 경로에 따른 라우팅을 쉽게 설정할 수 있다. 이를 통해 어플리케이션의 다양한 요청을 적절히 처리할 수 있도록 설정할 수 있다.

각 라우트는 하나 이상의 핸들러 함수를 가질 수 있으며, 이러한 함수는 라우트가 일치할 때 실행된다.

라우트 정의에는 다음과 같은 구조를 가진다.

```javascript
app.METHOD(PATH, HANDLER)
```

- app은 express의 인스턴스
- METHOD는 HTTP 요청 메소드이다.
- PATH는 서버에서의 경로
- HANDLER는 라우트가 일치할 때 실행되는 함수이다.

```javascript
//애플리케이션의 홈 페이지인 루트 라우트(/)에서 POST 요청에 응답하는 예시코드.
app.post('/', function (req, res) {
  res.send('Got a POST request');
});
```

이런식으로, app 인스턴스에서, http메서드인 post 요청 메소드를 사용할 수 있으며, 경로와 핸들러까지 간편하게 설정할 수 있다.

express 에서 지원하는 http 메서드는 이정도가 있다고 한다.

>get, post, put, head, delete, options, trace, copy, lock, mkcol, move, purge, propfind, proppatch, unlock, report, mkactivity, checkout, merge, m-search, notify, subscribe, unsubscribe, patch, search 및 connect... 중요한것만 알아보고 싶다는 생각이 든다...ㅋ


## RESTful API 지원

Express를 사용하여 RESTful API를 쉽게 개발할 수 있으며, JSON을 통해 데이터를 전달하고 요청 및 응답을 다룰 수 있다.

### 근데 RESTful API가 뭔지 아니?

REST API라고도 불리는데, 이는 웹 서비스를 설계하고 구현하는 데 사용되는 아키텍처 스타일이다. HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method중에 **GET, POST, PUT, DELETE** 메서드를 사용해서 상태(State)를 전달하는 원칙에 기반하는 아키텍처를 따르는 것을 원칙으로 한다. 이는 다음과 같은 특징을 가진다.

#### HTTP Method (자원)
- GET: 자원을 읽기 위해 사용한다.
- POST: 새로운 자원을 생성하기 위해 사용한다.
- PUT: 자원을 업데이트하기 위해 사용한다.
- DELETE: 자원을 삭제하기 위해 사용한다.

#### 상태
그리고 자원의 상태는 JSON이나, XML등과 같은 형태로 반환한다.

#### URL
또한, 각 자원은 고유한 URL을 가지고 있게 된다. 클라이언트는 이 URL을 사용해서 자원을 식별하고 액세스를 한다.

#### 무상태성
REST는 서버가 클라이언트의 이전 요청을 알고 있지 않는 무상태성을 가진다.

#### 응답 코드
REST에서는 HTTP 응답 코드를 사용하여 요청 처리 결과를 표현한다. 예를 들어, 200 OK은 성공, 404 Not Found는 자원을 찾을 수 없음 등을 나타낸다. 세세한건 나중에 더 공부해봐야겠다.

### 예시코드
```javascript
app.get('/api/items/:id', (req, res) => {
  const itemId = req.params.id;
  // 특정 아이템을 조회하는 로직 (itemId를 사용)
});
```

# RESTful API만드는 기본 단계

## Express 설치 및 프로젝트 설정
Node.js를 설치하고, 새로운 프로젝트를 만들어서 Express를 설치해주는 방법으로 시작을 한다.

![](https://velog.velcdn.com/images/dmstjdhdh/post/1d7f1247-b716-429d-9c99-b2ee81e348e9/image.png)

내가 원하는 환경에, 프로젝트 폴더를 만들고 npm init -y, npm install express 명령어를 시행시켜준다.

```
mkdir my-rest-api // 파일 생성
cd my-rest-api // 파일 이동
npm init -y // npm 프로젝트
npm install express // express 설치
```

## Express 어플리케이션 설정

Express 기본 설정 코드를 작성해준다. 나는 루트 파일에 server.js라는 js파일을 생성해준 후, 코드를 작성해주었다.

```javascript
const express = require('express');
const app = express();
//process.env는 nodeJS에서 환경 변수를 가져올 때 사용된다.
const port = process.env.PORT || 3000;

// JSON 형태로
app.use(express.json());
```

 1. require는 nodeJS에서 다른 패키지를 불러올 때 사용하는 키워드이다. express라는 모듈을 활용하겠다는 뜻으로 이해하자.
 2. app이라는 변수에 express 함수의 변환 값을 저장.
 3. port 설정을 한 후
 4. JSON 파싱 미들웨어를 추가해준다.
 
 ![](https://velog.velcdn.com/images/dmstjdhdh/post/c0406981-7afb-4806-905b-c1796d52d9c5/image.png)

```javascript
app.listen(port, () => {
    console.log(`server is listening at localhost:${port}`);
})
```
app.listen(port, () => { ... });: Express 애플리케이션을 지정한 포트에서 실행하는 부분이다. 서버가 시작되면 콜백 함수가 호출되어 서버가 정상적으로 실행 중임을 알리기 때문에 콘솔을 사용해서 서버가 정상적으로 작동하는지 확인해볼 수 있다.

```
node server.js
```

라는 명령어를 사용하면, 서버가 실행된다.
 
 ## 라우트 설정
 
 이제, RESTful API를 정의하고, 요청 처리를 위해서 라우트 핸들러를 작성할 수 있다. URL은, 백엔드에서 REST API 디자인에 맞춰서 작성할 수 있다.
 
 ```javascript
// GET 요청을 처리하는 라우트
app.get('/api/items', (req, res) => {
  // 여기서 데이터를 조회하고 클라이언트에 반환
  res.json({ message: 'GET 요청: 모든 아이템을 조회합니다.' });
});

// POST 요청을 처리하는 라우트
app.post('/api/items', (req, res) => {
  // 클라이언트에서 POST로 전송한 데이터를 처리
  const newItem = req.body;
  res.json({ message: 'POST 요청: 새로운 아이템을 생성합니다.', item: newItem });
});

// PUT 요청을 처리하는 라우트
app.put('/api/items/:id', (req, res) => {
  // 클라이언트에서 PUT로 전송한 데이터를 처리
  const itemId = req.params.id;
  // 아이템 업데이트 로직
  res.json({ message: `PUT 요청: 아이템 ${itemId}을 업데이트합니다.` });
});

// DELETE 요청을 처리하는 라우트
app.delete('/api/items/:id', (req, res) => {
  const itemId = req.params.id;
  // 아이템 삭제 로직
  res.json({ message: `DELETE 요청: 아이템 ${itemId}을 삭제합니다.` });
});

 ```
 
이런식으로 코드를 작성한 후에, 문서화나 api docs를 작성하면, 프론트에서 어떤 url로 접근했을 때, json형식으로 자원을 요청할 수 있는지 확인할 수 있다.

## React 예시

React 프로젝트라면 다음과 같은 예시코드를 확인해볼 수 있을 것 같다.

```javascript
const [data, setData] = useState([]);
const [message, setMessage] = useState('');

//컴포넌트가 렌더링 될 때 시행되는 React Hook
useEffect(() => {
    // GET 요청 URL 예시
    fetch('/api/items')
      .then((response) => response.json())
      .then((result) => {
        setData(result);
      })
      .catch((error) => {
        setMessage('데이터를 불러오는 중 오류가 발생했습니다.');
      });
  }, []);

```

이러한 React Hook을 이용해서, 데이터를 받아올 수 있다. fetch 함수를 이용해서, GET요청인 url로 요청을 보내고, 데이터를 받아오는 형식이다.

```javascript
// POST 요청
  const postData = async () => {
    try {
      const response = await fetch('/api/items', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ itemName: '새로운 아이템' }),
      });
      const result = await response.json();
      setMessage(result.message);
    } catch (error) {
      setMessage('데이터를 전송하는 중 오류가 발생했습니다.');
    }
  };
```

이런식으로 비동기적으로 요청을 수행할 수도 있다.

## Api Docs 예시

https://gist.github.com/iros/3426278 에서의 오픈소스이다. MarkDown으로 작성된 api 문서인데, URL이랑 Method, 파라미터, 응답 코드를 깔끔하게 정리하여 문서화되어있는걸 볼 수 있다. 

![](https://velog.velcdn.com/images/dmstjdhdh/post/a6f1f0e8-e015-41d5-bacd-e9f6ded1cd88/image.png)

# 결론

1. REST API에 대해서 자세하게 공부해보려했는데, 생각보다 양이 많은 것 같아서, 이에 대해서는 글을 또 다시 적어야할 것 같더라. 

2. 깔끔하게 정리되어있는 Api Docs에서 데이터를 긁어와서 뿌려주는 코드를 작성하다가, express.js에서 서버를 구축하고 api를 만들면 어떤식으로 되는거지?라는 간단한 질문을 통해서 조금 맛보기를 한 것 같다.

3. 다음에는 REST Api에대해서 더 자세히 공부해보고 글로 정리해봐야겠다. 그리고, 실제로 FullStack 형식으로 간단한 웹 어플리케이션 제작하면서, 조금씩 더 이해도를 높여봐야겠다.