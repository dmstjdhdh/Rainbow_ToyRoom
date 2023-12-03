# React Native란? 📱

React 개발자, 안드로이드 개발자, ios 개발자에게 친숙한 React Native는 페이스북에서 만든 모바일 어플리케이션 개발 오픈소스 프레임워크입니다. 

(지금까지 뭔가 반말로 쭉 글을 써왔지만... 슬슬 누군가 글을 읽어줬으면 좋겠다는 생각이 들어서, 이번 글부터 존댓말을 써보려고 해요. 🙃

![](https://velog.velcdn.com/images/dmstjdhdh/post/ee66a1fe-5461-45be-8aac-1892058143df/image.png)

## 장점 단점 💻

### 장점
JavaScript 개발을 해왔던 사람, React 프로젝트에 익숙한 사람은 다른 언어를 학습할 필요 없이, 낮은 러닝커브로 진입장벽이 낮은 것 같습니다.

또한, 크로스플랫폼을 지원하기 때문에, ios, Andriod 모두 개발이 가능합니다! 
> 간단한 앱, 크로스 플랫폼 지원 앱, React 개발자의 앱 개발 경험, 웹 기술 통합 필요... 등등 의 상황에서 React Native를 채택할 수 있을 것 같아요. 😃

### 단점
앞서 말한 장점이 사실 단점이 될 수도 있는게, JavaScript를 다뤄보지 않은 사람들은 jsx나 다른 앱개발과 다른 형태의 개발 방식(pros, state 등등...)에 어려움을 느낄 수 있을 것 같아요. 

네이티브 앱 보다는 성능도 좋지 못하기도 하고요. 😥

# RN(React Native)를 경험하다. 🤩

최근에 좋은 기회가 생겨서, 어플리케이션 개발을 시도해볼 수 있게 되었습니다. React를 공부하면서 토이프로젝트를 진행하고 있던 저에게, React Native 개발은 꽤나 시도해보고 싶은 기회였습니다.

> "개발을 진행하면서, 기록할 수 있는 개발 방식을 기록해보자."

# 개발 🖥️

## 구현해야하는 것
![](https://velog.velcdn.com/images/dmstjdhdh/post/dd656834-4aea-49b2-9443-fc1c6986afbc/image.png)

사용자가, 클릭시에 날짜를 변경할 수 있는 팝업, 그리고 클라이언트 내에서 선택한 날짜를 반영하는 기능 개발이 필요했습니다.

React에서는 간단하게, react-calander 라이브러리를 설치하면 간단한 달력 모델을 사용할 수 있었는데요, RN에서도 해당 모델이 있을지 찾아보니 react-native-calendars 라는 좋은 라이브러리가 이미 존재했습니다.

```yarn
$ npm install --save react-native-calendars
```

바로 설치해주고, App 내에서 실행해주니,

![](https://velog.velcdn.com/images/dmstjdhdh/post/43a07afa-c379-4e22-98b0-33e136195115/image.png)

이런식으로, 그저 날짜가 보이는 달력 컨텐츠가 시뮬레이터에 비춰집니다. 선택해도 딱히 선택한 부분의 인터렉션 말고는 어떠한 변화도 없었습니다.

## 아이디어 🍿

>
1. 팝업 형태의 달력을 개발하자.
2. 애니메이션 간단한거를 넣어보자.
3. 컴포넌트 내에서, 팝업에서 선택한 날짜가 반영되도록 하자.
4. React Hook을 사용해서, 초기 상태나 날짜 지정에 대응해보자.

## 팝업 형태 컴포넌트

React Native 자체에서, Modal 이라는 팝업 형태의 컴포넌트를 지원해줍니다. props 또한 다양해서, 어떤식으로 팝업을 디자인할지 고민을 할 수 있었습니다.

```jsx
<Modal
	transparent={true}
	visible={isModalVisible}
	onRequestClose={() => {
		setModalVisible(false);
	}}
>
	<RNCalendar/>
</Modal>
```

### 애니메이션 Props 😺

![](https://velog.velcdn.com/images/dmstjdhdh/post/1b5d8f96-1e71-4895-8d13-79191fec9558/image.png)


React Native 에서 명시해준 animationType을 slide로 지정해주면서, 올라오는 듯한 애니메이션을 지정해줍니다.

또한, 팝업 내에서 날짜가 선택되었을 때, 날짜가 업데이트 되어야하므로, useState와 onDayPress에 전달될 액션 (달력 날짜가 눌렸을 때의 액션)을 정의해주면서, 달력을 이용한 날짜 선택 컨텐츠를 제작했습니다.

```jsx
// Modal이 켜져있는지 안켜져있는지 react-hook 사용
const [isModalVisible, setModalVisible] = useState(false);

// 며칠인지 확인하는 상태
const [selectedDate, setSelectedDate] = useState("");

// 팝업 내용이 눌렸을 때
const onDayPress = (day) => {
    setSelectedDate(day.dateString);
    setModalVisible(false);
};

// Modal 컴포넌트 작성.
<Modal
	animationType="slide"
	transparent={true}
	visible={isModalVisible}
	onRequestClose={() => {
		setModalVisible(false);
	}}
>
	<RNCalendar onDayPress={onDayPress} />
</Modal>
```

## 달력 스타일링 🗓️

React의 styledComponent와 비슷한 방식으로, 요소의 배치나 디자인을 결정할 수 있는 방식이 있습니다. 거대하게 올라오는 달력 팝업을 이런식으로 수정하여, 보기 더 편한 달력을 개발해보았습니다.

```jsx
//View, StyleSheet를 이용해서, 팝업 달력을 디자인.
<Modal
	animationType="slide"
	transparent={true}
	visible={isModalVisible}
	onRequestClose={() => {
		setModalVisible(false);
	}}
>
	<View style={styles.centeredView}>
        <View style={styles.modalView}>
            <RNCalendar onDayPress={onDayPress} />
        </View>
    </View>
</Modal>

//가운데에 둥근 모양의 팝업 디자인
const styles = StyleSheet.create({
  centeredView: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
    },
  
  modalView: {
        margin: 20,
        backgroundColor: 'white',
        borderRadius: 20,
        padding: 35,
        alignItems: 'center',
        shadowColor: '#000',
        shadowOffset: {
            width: 0,
            height: 2,
        },
        shadowOpacity: 0.25,
        shadowRadius: 4,
        elevation: 5,
    },
});
```
## 결과

![](https://velog.velcdn.com/images/dmstjdhdh/post/41cb81e8-6fb7-4d47-9aba-6effd6119889/image.gif)


>https://www.npmjs.com/package/react-calendar

다음 사이트에 접근하면, 해당 방식의 개발 말고도, 접근이 가능한 Props에 대해서 구체적으로 설명되어있으며, 예제 코드도 제공받을 수 있습니다.