### 클라이언트에서는 꽤나 많은 양의 데이터가 변화한다.

데이터를 관리하는 방식에 있어, 좀 더 근원적인 존재가 있으면 편할 것이다.

Redux에서는 이러한 원칙을 지닌다.
> 1.동일한 데이터는 같은 곳에서 가지고 온다.
2.상태는 읽기 전용이다. (Action이라는 객체가 존재해야만 변경 가능)
3.상태 변경은 순수하게 함수로만 가능하다.

이를 이해하기 위해서, Action, Dispatch, Reducer, Store에 대해서 작성해보려고 한다. 이메일 인증을 예시로 들어서 설명하면 좋을 것 같아, 상태를 정해놓아보자.

```javascript
export const USER_REGISTER_REQUEST = 'USER_REGISTER_REQUEST'
export const USER_REGISTER_SUCCESS = 'USER_REGISTER_SUCCESS'
export const USER_REGISTER_FAIL = 'USER_REGISTER_FAIL'
```
유저가 회원가입을 했을 때, 가입요청을 한 상태인지, 성공했는지, 실패했는지에 대해서 작성.

### Action

어떤 동작을 할지에대해서, 객체 형식으로 정의된 형태이다.

```javascript
{
	type: USER_REGISTER_SUCCESS,
	payload: data,
}
```
type을 꼭 정의해서, 어떤 동작을 할 것인지 정해줘야하며, 전달해줘야할 값이 있다면 payload를 이용한다.

### Dispatch
Action을 Reducer로 전달해주는 함수이다.

```javascript
export const register = (userInput) => async (dispatch) => {
    try{
        dispatch({
            type: USER_REGISTER_REQUEST,
        })

        const {data, status} = await authApi.post("/signup", userInput);
        if(status === 201){
            dispatch({
                type: USER_REGISTER_SUCCESS,
                payload: data,
            })
        }

    } catch (e) {
        dispatch({
            type: USER_REGISTER_FAIL,
            payload:
                e.response && e.response.data.message
                    ? e.response.data.message
                    : e.message,
        })
    }
}
```
try catch문을 이용해서, 각각 정해진 type에 맞춰서 Reducer로 Action을 전달해주는 함수를 작성했다.

만약 authApi에서 201의 상태를 반환한다면, 성공과 관련된 상태를 관리해주면서, data를 전달할 수 있을것이다.

### Reducer

Dispatch에게서 전달받은 Action 객체의 type 값에 따라서 상태를 변경시키는 함수이다.

```javascript
export const userRegisterReducer = (state = {}, action) => {
    switch (action.type) {
        case USER_REGISTER_REQUEST:
            return {loading : true}
        case USER_REGISTER_SUCCESS:
            return {loading : false, success : true}
        case USER_REGISTER_FAIL:
            return {loading : false, err : action.payload}
        default:
            return state
    }
}
```

상태변경은 이 Reducer에서만 이루여져야만 한다.

### Store

Store는 상태가 관리되는 단 하나의 저장소이다.

```javascript
import {createStore} from "redux";

const reducer = {userRegister: userRegisterReducer};

const store = createStore(reducer);
```


## Redux 메서드

Action을 dispatch해서 Reducer에 전달, 상태를 Store에서 저장, 관리... 
결국에는 Component에서 이 메서드들을 사용할 수 있어야한다.

### useSelector()

```javascript
import { useSelector } from 'react-redux'

const userRegister = useSelector((state) => state.userRegister)
const {loading, success, error} = userRegister
```

컴포넌트와 State를 연결할 수 있는 메서드 useSelector()

상태를 관리하면서, 컴포넌트에서 useSelector를 이용해서 상태에 접근하면 된다.

작성자: Subin