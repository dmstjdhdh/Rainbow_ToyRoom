# React와 트리 구조

React는 사용자 인터페이스를 구축하기 위해서, 가상 DOM을 사용한다. 이 때 React 요소들은 트리 구조로 구성된다.

## 가상 DOM?

DOM(Document Object Model)을 추상화한 가상 DOM은 트리 구조를 가지고 있으며, 효율적인 렌더링 및 업데이트가 가능하게 하는 개념이다.

### 동작 방식

1. 초기 랜더링 : UI의 초기 상태를 표현하는 가상 DOM트리가 생성된다. 이 때, React Element들이 가상 DOM의 노드로 변환이 된다.
2. 상태 변화: UI의 상태가 변경되면, React는 이 변경된 상태를 기반으로 새로운 가상 DOM 트리를 생성한다.
3. 가상 DOM과 비교: React가 이전 가상 DOM과 새로운 가상 DOM을 비교.
4. 차이 발견: 어떤 노드가 추가, 변경, 삭제되었는지 나타낸다.
5. 실제 DOM을 업데이트 한다.

이러한 가상 DOM 사용은, 효율적인 랜더링 방식을 제공하며, React처럼 컴포넌트 기반 개발을 촉진한다. 



## React 엘리먼트 구조

React 엘리먼트 구조는 부모와 자식 관계로 이루어져 있다. 각 엘리먼트는 props랑 children을 가질 수 있으며, 다음과 같은 예제를 확인해보자.

```jsx
<App>
	<Header/>
	<Hero>
		<Sidebar/>
		<Content/>
	</Hero>
</App>
```

이 코드에서 'App'컴포넌트는 루트 노드가 되며, 그 안에 'Header', 'Main', 'Sidebar', 'Content' 컴포넌트들이 자식 노드로 들어가게 된다.