## Form

사용자의 입력에 따라서 상태값이 반영되는 기능을 위해 Form태그를 사용한다.

```javascript
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

input태그에 사용자가 값을 입력할 경우, handleChange()를 통해서, 상태값이 반영된다.

### Form의 이벤트는 어떤 종류가 있을까?

onChange:
사용자의 입력으로 인해 입력요소가 변경될 때마다 시행이된다. React뿐만 아니라, 다른 개발 툴에서 사용되는 EditBox컴포넌트에서 자주 사용되는 메서드이다.

onSubmit:
폼 제출을 누르면, (위 코드에서는, submit type의 input태그가 될 것 같다.) 이벤트가 일어난다.

onInput:
요소의 값이 변경될 때마다 발생한다. onChange랑 뭐가 다르냐고 묻는다면, Focus에 집중하면 된다.



#### onChange와 onInput의 차이.
사용자가 input에 value를 입력하는 도중에는 해당 input에 Focus가 된 상태이고, 다른 곳을 눌러서 커서가 없어지면, Focus가 되지 않은 상황이다. 

onInput은 Focus가 되어있는 상태에서도 계속 이벤트가 일어나고, onChange는 Focus를 잃었을 때 이벤트가 작동된다. 안정성이나, 개발의도에 의해서 선택되겠지만, onChange를 사용하는것이 권장되는 것 같다.

## event.preventDefault()

```javascript
handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }
```
Form에대해서 이해는 되었고... handleSubmit에 있는 event.preventDafult는 뭘까?

우선 해당 기능은

|| _어떤 이벤트를 명시적으로 처리하지 않은 경우, 해당 이벤트에 대한 브라우저의 기본 동작을 실행하지 않도록 지정._

하기위해 사용한다고 한다.

a태그나 submit태그는 이벤트가 일어날 때 페이지를 이동시키는 속성을 가지고 있다. submit을 할 때마다, 개발자가 명시하지 않는다면, 브라우저의 기본동작을 시행하지 않는다고 하니, 명시하지 않은 동작들을 막아야할 필요가 있다면, 꼭 사용해야하는 메서드인 것 같다.

## event.stopPropagation();

위에서도 작성했듯이(onChange와 onInput), 나는 비슷한 기능을 하는 메서드가 있다면 꼭 같이 찾아보는 편이다. 

이는, 이벤트가 상위 Dom으로 전파되는 것을 막는 기능이다.
```javascript
return (
    <div onClick={() => console.log("부모버튼")}>

      <button onClick={() => console.log("자식버튼")}>눌러</button>

    </div>
  );
```

과 같은 컴포넌트 구조에서, 자식버튼을 누른다면, 상위 컴포넌트에 있는 이벤트도 발생하여

**부모버튼
자식버튼**

이런식으로 로그가 작성이 된다. 만약 "자식버튼"이라는 로그만 띄우고싶다면 콜백함수에 event.stopPagation()을 작성해주면 문제 없이 기능구현이 될 것이다.