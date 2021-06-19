# 7장 컴포넌트의 라이프사이클 메서드

> 7.1 컴포넌트 라이프 사이클
>
> 7.2  라이플사이클 메서드 사용
>
> 7.3 정리





### 7.1 컴포넌트 라이프 사이클

>lifeCycle

![](https://thebook.io/img/006946/140.jpg)



리액트의 컴포넌트는 LifeCycle이 존재합니다.

- 컴포넌트의 LifeCycle은 page에 렌더링되기 전 과정 부터 시작해서 페이지에서 사라질 때 끝이 납니다.

- 이때, LifeCycle 메소드를 이용하여 불필요한 업데이트 방지, 렌더링 전/후 어떤 작업을 수행할 수 있습니다.

- LifeCycle 메소드 종류는 총 10가지

  - Will접두사가 붙은 메소드(어떤 작업을 **작동하기 전**에 실행되는 메서드)
  - Did접두사가 붙은 메소드(어떤 작업을 **작동한 후**에 실행되는 메서드)

- LifeCycle의 카테고리

  - 마운트
  - 업데이트
  - 언마운트

  

> 마운트

DOM이 생성되고 웹 브라우저상에 나타나는 것을 mount(마운트)라고 합니다.

<마운트 수행시 호출하는 메서드 순서>

1. 컴포넌트 만들기
2. constructor(컴포넌트를 새로 만들 때마다 호출되는 클래스 생성자 메서드)
3. getDerivedStateFromProps(props에 있는 값을 state에 동기화하는 메서드)
4. render(UI를 렌더링하는 메서드)
5. componentDidMount(컴포넌트가 웹 브라우저상에 나타난 후 호출하는 메서드)



> 업데이트

컴포넌트를 업데이트 하는 경우

- props가 바뀔 때

- state가 바뀔 때

- 부모 컴포넌트가 리렌더링될 때

- this.forceUpdate로 강제로 렌더링을 트리거 할 때

<업데이트 할 때 호출하는 메서드>

![](https://thebook.io/img/006946/142_1.jpg)

- getDerivedStateFromProps:props가 바뀌어서 업데이트 할 때도 호출
- shouldComponentUpdate:컴포넌트가 리렌더링을 해야할지 말지 결정하는 메서드 입니다. false를 반환하면                     아래의 함수를 실행하지 않습니다.
- render:컴포넌트를 리렌더링합니다.
- getSnapshotBeforeUpdate:컴포넌트 변화를 DOM에 반영하기 바로 직전에 호출하는 메서드 입니다.
- componentDidUpdate:컴포넌트 업데이트 작업이 끝난 후 호출하는 메서드 입니다.



> 언마운트

컴포넌트를 DOM에서 제거하는 것을 언마운트(unmount)라 합니다.

<언마운트할 때 호출하는 메서드>

1. 언마운트 하기

2. componentWillUnmount:컴포넌트가 웹 브라우저상에서 사라지기 전에 호출하는 메서드 입니다.





### 7.2  라이플사이클 메서드 사용

> render() 함수

`render(){...}`

- 컴포넌트의 모양새를 결정

- 라이프사이클 메서드 중 유일한 필수 메서드

- 메서드 안에서 this.props와 this.state에 접근할 수 있음

- 리액트 요소(div같은 태그, 따로 선언한 컴포넌트)를 반환함

- 아무것도 보여주고 싶지 않을 때는 null값이나 false를 반환

- 이 메소드 안에서는 절대로 state 값을 변형하거나 웹 브라우저에 접근해서는 안 됩니다.

  DOM 정보를 가져오거나 변화를 줄 때는 componentDidMount에서 처리해야 합니다.

  

> constructor 메서드

`constructor(props){...}`

- 컴포넌트 생성자 메서드
- 컴포넌트를 만들 때 처음으로 실행됨
- 초기 state 정할 수 있음



> getDerivedStateFromProps 메서드

- props로 받아 온 값을 state에 동기화 시키는 용으로 사용
- 컴포넌트를 마운트 하거나 props를 변경할 때 호출

```jsx
static getDerivedStateFromProps(nextProps, prevState){
    if(nextProps.value != prevState.value){
   
        return {value:nextProps.value};
    }
    return null;//state를 변경할 필요가 없다면 null 반환
}
```



> componentDidMount 메서드

`componentDidMount(){...}`

- 컴포넌트를 만들고, 첫 렌더링을 다 마친 후 실행함
- 처리 작업
  - 다른 자바스크립 라이브러리
  - 프레임워크 함수 호출
  - 이벤트 등록
  - setTimeout, setInterval
  - 네트워크 요청(비동기 작업 처리)



> shouldComponentUpdate 메서드

`shouldComponentUpdate(nextProps,nextState){...}`

- props 또는 state를 변경했을 때, 리렌더링을 시작할지 여부를 지정하는 메서드

- 이 메서드는 반드시 true 또는 false 값을 return해야함

- 컴포넌트를 만들 때 이 메서드를 따로 생성하지 않으면 기본적으로 언제나 true를 반환

  false 반환시 아래 업데트 과정은 중지 됨

- 이 메서드 안에서 

  - 현재 props와 state는 this.props, this.state로 접근한다.
  - 새로 설정될 props 또는 state는 nextProps. nextState로 접근한다.

- 프로젝트 성능을 최적화 할 때 사용됨



> getSnapshotBeforeUpdate 메서드

- render 메서드를 호출한 후 DOM에 변화를 반영하기 바로 직전에 호출하는 메서드
- return 값은 componentDidUpdate에서 세 번째 파라미터인 snapshot 값으로 사용됨
- 업데하기 직전의 값을 참고할 일이 있을 때 활용됨(ex. 스크롤바 위치 유지)

```jsx
getSnapshotBeforeUpdate(prevProps, prevState){
    if(prevState.array !== this.state.array){
        const {scrollTop, scrollHeight} = this.list
        return {scrollTop, scrollHeight}
    };
}
```



> componentDidUpdate 메서드

`compnentDidUpdate(preveProps, prevState, snapshot){...}`

- 리렌더링을 완료한 후 실행 
- 업데이가 끝난 직후이기 때문에, DOM 관련 처리를 해동 무방함
- preveProps 또는 prevState를 사용하여 컴포넌트가 이전에 가졌던 데이터에 접근 가능
- getSnapshotBeforeUpdate에서 반환한 값이 있다면 여기서 snapshot 값을 전달받을 수 있음



> componentWillUnmount 메서드

`componentWillUnmount (){...}`

- 컴포넌트를 DOM에서 제거할 때 실행

- componentDidMount에서 등록한 이벤트, 타이머, 직접 생성한 DOM이 있다면 여기서 제거 작업을

  해야함





### 7.3 정리

> 정리



![img](https://thebook.io/img/006946/151_2.jpg)

라이프사이클 메소드는 컴포넌트의 상태가 변함에 따라서 실행되는 메소드 입니다. 

<이 경우에 유용합니다.>

- 서드파티 라이브러리 사용
- DOM을 직접 조작

더불어 컴포넌트 업데이트의 성능을 개선할 때는  shouldComponentUpdate 메소드가 중요하게 사용 됩니다.

