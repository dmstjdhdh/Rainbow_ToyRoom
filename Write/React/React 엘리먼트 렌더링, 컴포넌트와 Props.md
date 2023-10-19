### Element

엘리먼트는 React 앱의 가장 작은 단위이며, 일반 객체 단위로 쉽게 생성이 가능하다.

```javascript
const element = <h1>Hello, world</h1>;
```

### Element 렌더링하기

React로 구현된 애플리케이션은 일반적으로 하나의 루트 DOM 노드가 있다. 

React 엘리먼트를 렌더링 하기 위해서는 우선 DOM 엘리먼트를 ReactDOM.createRoot()에 전달한 다음, React 엘리먼트를 root.render()에 전달해야 한다.

![](https://velog.velcdn.com/images/dmstjdhdh/post/7a69e1f5-b16f-449e-9e4d-bf1de21feb03/image.png)

평범하게 React Project를 생성한 후에, index.js를 확인하면, root를 생성하여 render해주는 코드를 확인해볼 수 있다.

## 컴포넌트와 props

엘리먼트와는 다르게, 컴포넌트는 JavaScript 함수의 형태를 가진다.


이 함수는 “props”라고 하는 임의의 입력을 받은 후, 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환한다.

```javascript
function HelloUser(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

상세하게 보자면, HelloUser라는 함수에, props라는 인자를 받아서, 엘리먼트를 return한다.

### 여기서 props는 무엇이냐...

React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면 "JSX 어트리뷰트"와 "자식"을 해당 컴포넌트에 단일 객체로 전달하고, 이 객체를 “props”라고 한다.

```javascript
function HelloUser(props) {
  return <h1>Hello, {props.name}</h1>;
}

const root = ReactDOM.createRoot(document.getElementById('root'));
const element = <HelloUser name="Subin" />;
root.render(element);
```

> 1. "HelloUser name="Subin"" 엘리먼트로 root.render()를 호출한다.
2. React는 {name: 'Subin'}를 props로 하여 HelloUser 컴포넌트를 호출한다.
3. HelloUser 컴포넌트는 결과적으로 Hello, Subin 엘리먼트를 반환한다.
4. React DOM은 Hello, Subin 엘리먼트와 일치하도록 DOM을 효율적으로 업데이트 한다.

일반적으로 React에서 컴포넌트는 자신의 출력에 다른 컴포넌트를 참조할 수 있다. 앱의 최상위에는 단일 App 컴포넌트를 가지고 있고, 

![](https://velog.velcdn.com/images/dmstjdhdh/post/3cbe3651-f1c9-4116-ae32-46c15b93053e/image.png)

리액트 프로젝트에서 App.js파일에서 App 컴포넌트에 다른 컴포넌트를 참조하는 방식으로, 상단 UI를 설정할 수 있다. 컴포넌트에 props를 전달하고싶다면 목적에 맞게 작성하면 된다.

주의할 점은, props는 읽기 전용으로만 사용해야하며, 전달받은 props 자체를 수정하는 방식의 개발은 불가능하며, 지양해야한다.

작성자: Subin