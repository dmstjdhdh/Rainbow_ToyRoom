### 반복문 사용 방법 예시

```javascript
const siblings = this.foo.children;

//노드별로 인덱스 관련계산이 필요한 경우
for(let idx = 0; i<siblings.length(): i++) {
  siblings.children[idx].foo = "Hello World";
}

for (const sibling of siblings) {
  sibling.foo = "Hello World";
}
```

코드 가독성을 위해서, 객체의 반복문을 사용할 때, of라는 키워드를 많이 사용한 경험이 있다. idx를 선언해주는 방식보다, 더 간편하고 의미가 명확하게 보였던 것 같아 사용을 자주했었다.

### 차이점에 대해서 알아보게된 계기

![](https://velog.velcdn.com/images/dmstjdhdh/post/b69a3821-40d8-4420-930f-b0faa21896ba/image.png)

for in은 왜 사용하고, for of와의 차이점을 물어본 친구가 있었다. 사실 for...in 루프구조는 별로 사용해본 적이 없어서, 그냥 of랑 똑같이 사용하면 되는 줄 알았다. (어리석음)


### 대표적 예시

```javascript
var arr = [3, 5, 7];
arr.foo = "hello";
    
for (var i in arr) {
  console.log(i); // logs "0", "1", "2", "foo"
}
    
for (var i of arr) {
  console.log(i); // logs "3", "5", "7"
  // it doesn't log "3", "5", "7", "hello"
}
```

코드를 보면, arr라는 배열에 iterable한 객체인 3, 5, 7이 할당되었고, arr에서 foo라는 속성에 "hello"라는 값이 할당되었다.
for...in


#### for...in

 - 객체의 속성을 반복하기 위해 사용한다.
 
 ```javascript
let human = {
        name: "수빈",
        age: 22,
        job: "developer",
      };

  for (key in human) {
     console.log(key, human[key]);
  }
 
 //출력1 name 수빈
 //출력2 age 22
 //출력3 job developer
 ```
 - key는 human의 속성인 name, age, job이 순서대로 출력되고, human[속성]은 각각 "수빈", 22 "developer"가 출력되는 것을 볼 수 있다.
  - 이러한 속성들을 stack overflow에서 enumerable하다고 한다.
 
#### for...of

 - for...of는 반복 가능한(iterable) 객체를 순회하기 위해서 사용된다.
 - 배열의 요소 값을 순회할 때 편리하며, 인덱스 값을 따로 선언할 필요가 없다.
 ```javascript
const arr = [1, 2, 3];
for (const value of arr) {
  console.log(value);
}
// 출력:
// 1
// 2
// 3
 ```
 
 
### 결론
배열을 순회하는 경우, for...of를 사용하는 것이 일반적으로 더 안전하고 직관적인 것 같다. 하지만, 객체의 속성에 접근해서 순회해야 하는 경우에는 for...in을 사용할 수 있을 듯 하다.

작성자: Subin