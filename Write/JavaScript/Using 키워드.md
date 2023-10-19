
기존에 database를 await로 가져왔을 때

```javascript
const connection = await getDb();

try{
	//database 작업
} finally {
	await connection.close();
}
```

try catch문에서 finally를 모든 작업을 마친 후에, dispose해줬다.

```javascript
const getConnection = async () => {
	const connection = await getDb();
    
    return {
    	connection,
    	[Symbol.asyncDispose]: async () => {
        	await connection.close();	
        },
    };
};

{
	await using {connection} = getConnection();
	//connection으로 작업
}

//자동으로 dispose
```

원래는 C#에 있는 키워드라서 게임개발을 하면서 리로스 정리를 구현을 위해서 알고있었던 내용인데, javascript와 typescript에서도 using키워드가 새로 등장.

정상작동, 오류등의 몇 가지 상황에 모두 대응하기위해 try catch finnally를 사용하는 것도 좋지만, 이런 키워드도 알아놓으면 좀 더 코드의 의도가 명확해보이지 않을까 싶다.

작성자: Subin