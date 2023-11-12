React를 함수 컴포넌트 기반으로 개발하면, 훅을 사용하여 컴포넌트를 구성하게 된다.

lifecycle 메서드 대체 가능한 useEffect에 대해서 알아보려고 한다.

# 마운트와 언마운트

> 마운트(mount)
> 
> 마운트는 컴포넌트가 최초로 렌더 될 때 거치는 과정. 이후 props와 state가 변경될 때는 마운트 과정을 거치지 않는다.


> 언마운트(unmount)
> 
> 언마운트는 컴포넌트가 삭제될 때 거치는 과정이다.


# useEffect 기본 사용법

### 기본
useEffect를 사용하면, 컴포넌트 내에서, side effect를 수행할 수 있다.

```javascript
useEffect(() => {
	(이펙트 함수)
	return {
		(클린업 함수)
	};
}, [의존값]);
```

기본적으로 useEffect는 두 번째 인자로 배열 형태의 의존값을 필수로 가진다. 의존값이 처음으로 생성 됐을 때와 변경 될 때 이펙트 함수가 실행된다.

클린업 함수는 useEffect의 return값으로 정의하는데, 컴포넌트가 삭제될 경우 함수가 실행된다.

```javascript
const [count, setCount] = useState();

useEffect(() => {
	alert("count changed");
}, [count]);
```

위처럼 count라는 state값을 의존성 배열에 넣으면, count가 초기에 생성되었을 때와, count가 변경 됐을 때, alert가 뜨게 된다.

### 의존값을 넣지 않으면?

```javascript
const [count, setCount] = useState();
const [name, setName] = useState();

useEffect(( => {
	alert("count changed");
});
```

위 예제에서는 count와 name 두 개의 state를 넣었다. 앞서 봤던 예제에서는 count를 의존값으로 넣어 값이 변할 때마다 이펙트 함수를 실행시켰지만, 의존값을 넣지 않는다면, 위 예제는 매 렌더시마다 alert가 뜨게 된다.

name이 변경되어도 alert("count changed") 가 실행된다는 것이며, useEffect를 사용할 이유가 없어진다.

### 의존값에 빈 배열([])을 넣으면 어떻게 될까?

그렇다면 빈 배열을 넣는다면? -> 실제로 사용되는 패턴이다.

```javascript
useEffect(() => {
	alert("mount");
}, []);
```

의존값이 변경되거나,  처음으로 생성되었을 때 시행된다는 것을 알 수 있다.

빈 배열을 의존값으로 넣을 경우에도 마찬가지로, 처음으로 생성되었을 때 실행된다. 하지만 빈 배열은 처음 생성되었을 때 이후로 변경될 수 없기 때문에 처음 생성시에만 이펙트 함수가 실행된다.

따라서 useEffect에 빈 배열을 넣는 경우는 처음으로 변수가 생성될 때, 즉 컴포넌트가 최초로 렌더링되는 마운트(mount)시에 단 한번 실행될 때를 위해 사용한다.

이는 클래스 컴포넌트의 라이프사이클 메소드에서 componentDidMount()의 기능과 같다고 할 수 있다.

### 언마운트(unmount)는 어떻게 구현할까?

```javascript
useEffect(() => {
	return () => {
		alert("unmount");
	};
}, []);
```
언마운트는 빈 배열과 클린업 함수를 조합해서 구현할 수 있다. 이렇게 구현 할 경우 컴포넌트가 없어지는 순간 alert("unmount")가 실행되고, 그 이전엔 실행되지 않을 것이다.

이는 클래스 컴포넌트의 라이프사이클 메소드의 componentWillUnmount() 의 기능과 같다고 할 수 있다.

참고: https://jongminfire.dev/react-use-effect-%ED%9B%85-%EC%9D%B4%ED%8E%99%ED%8A%B8-%ED%95%A8%EC%88%98-%ED%81%B4%EB%A6%B0%EC%97%85-%ED%95%A8%EC%88%98