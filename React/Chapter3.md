# 3장 컴포넌트

> 3.1 첫 컴포넌트 생성
>
> 3.2 props
>
> 3.3 state
>
> 3.4 정리



컴포넌트는 템플릿 보다 다양한 기능을 가지고 있습니다.

- 데이터가 주어지면 이에 따라서 UI를 만들어 줍니다.

- LiftCycle API를 이용하여 컴포턴트가 생성, 소멸 시 이에 따른 다양한 작업을 할 수 있습니다.

  또한, 메소드를 정의하여 특별한 기능을 붙일 수 있습니다.


### 3.1 첫 컴포넌트 생성

```jsx
import React, {Component} from 'react'

class MyComponent extends Component{
    render(){

        return (
            <div>
               첫 컴포넌트
            </div>
        )
    }
}
export default MyComponent;

```



### 3.2 props

> props

- props(properties)는  컴포넌트의 속성을 설정할 때 사용하는 요소 입니다.
- 부모 컴포넌트에서만 설정할 수 있습니다.



> props 설정 및 사용

```jsx
class App extends Component {
  render() {
    return (
        <div>
           <MyComponent name="홍길동"/> //props 설정
        </div>
    );
  }
}

class MyComponent extends Component{
    render(){
        return (
            <div>
                안녕하세요 제 이름은 {this.props.name} 입니다. //props 사용
            </div>
        )
    }

}

```



> defaultProps 설정 및 사용(1)

```jsx
class MyComponent extends Component{
    render(){

        return (
            <div>
                안녕하세요 제 이름은 {this.props.name} 입니다.
                제 나이는 {this.props.age} 입니다.
            </div>
        )
    }

}
MyComponent.defaultProps={
    age:"12",
}


```



> defaultProps 설정 및 사용(2)

- defaultProps를 설정하는 또 다른 방법이 있는데 이 방법은 클래스 내부에 정의하는 것 입니다.

  그러나 이 방법은 특별한 설정이 필요하지만 create-react-app으로 만들어진 프로젝트는 이 문법을 허용 합니다.
  
```jsx
class DefaultComponent extends Component{

    static defaultProps = {
        name:"홍길동",
        age:"20"
    }
    render(){
        return(
            <div>
                제 이름은 {this.props.name} 입니다.
                제 나이는 {this.props.age} 입니다.
            </div>
        )
    }

}
```



> propTypes 검증 및 필수 사용(1)

- 컴포넌트 **필수 props**를 지정하거나 props 타입을 지정하기 위해서 사용됩니다.
- 만약 type에 맞지 않는 props이면 오류를 발생시킵니다.
- 이 외에도 다양한 propTypes가 존재합니다. https://reactjs.org/docs/typechecking-with-proptypes.html

```jsx
import PropTypes from 'prop-types';
class MyComponent extends Component{
    render(){
        return (
            <div>
                안녕하세요 제 이름은 {this.props.name} 입니다.
                제 나이는 {this.props.age} 입니다.
            </div>
        );
    }
}

MyComponent.defaultProps={
    age:3
}

MyComponent.propTypes ={
    name : PropTypes.string, //name proptype을 string으로 설정
    age : PropTypes.number.isRequired //필수적으로 존재해야하며 숫자이어야 합니다.
}

```



>propTypes 검증 및 필수 사용(2)

```jsx
import PropTypes from 'prop-types';
class DefaultComponent extends Component{

    static propTypes = {
        name:PropTypes.string, //name proptype을 string으로 설정
        age : PropTypes.number.isRequired //필수적으로 존재해야하며 숫자이어야 합니다.
    }
    static defaultProps = {
        name:"홍길동",
        age:"20"
    }
    render(){
        return(
            <div>
                제 이름은 {this.props.name} 입니다.
            </div>
        )
    }

}
```



### 3.3 state

> state

- 해당 컴포넌트 내부에서 읽고 또 업데이트할 수 있는 값을 사용하기 위해서 사용하는 속성 입니다. 또한, default 값을 미리 설정해야 사용할 수 있습니다.
- this.setState() 메서드로만 값을 업데이할 수 있습니다.
- state 초깃값 설정->state 렌더링 하기->state 값 업데이트하기 



> constructor(컴포넌트의 생성자 메서드), state 초깃값 설정

- state의 초깃값은 컴포넌트 생성자 메서드 **constructor** 내부에서 설정할 수 있습니다. 
- 예를 들어 MyComponent라는 클래스가 있을 때 기본적으로 Component 클래스를 상속합니다. MyComponent에서 명시적으로 constructor 메서드를 작성하지 않으면 Componet 클래스의 constructor 메서드를 기본적으로 호출 됩니다.
- MyCompoent에서 constructor 메소드를 명시적으로 사용하려면 super 키워드를 사용하여 부모 클래스의 constructor를 미리 호출하고 컴포넌트 생성시 props 값을 사용하기 때문에 인자로 같이 넘겨줘야 합니다.

```jsx
class MyComponent extends Component{

    constructor(props){
        super(props);
        this.state ={
            number : 0
        }
    }

    render(){
        return(
            <div>Count: {this.state.number}</div>
        );
    }
}
```



> setState(state 값 업데이트)

- setState 값은 setState 함수를 통하여 업데이트를 할 수 있습니다.

```jsx
class MyComponent extends Component{

    constructor(props){
        super(props);
        this.state ={
            number : 0
        }
    }

    render(){ 
        return(
            <div>
               <h1>Number {this.state.number}</h1> 
               <button onClick={
                   ()=>{
                       this.setState({number:this.state.number + 1})
                   }
               }>Click Me</button>
            </div>
        );
    }
}

```



- setState도  defaultProps와 propTypes를 정의할 때 사용한 문법으로 constructor 바깥에서 정의할 수 있습니다.(원칙적으로는 state는 constructor 메소드 내에서만 정의해야 합니다.)

```javascript
class MyComponent extends Component{

    state = {
        number:0
    }

    render(){ 
        return(
            <div>
               <h1>Number {this.state.number}</h1> 
               <button onClick={
                   ()=>{
                       this.setState({number:this.state.number + 1})
                   }
               }>Click Me</button>
            </div>
        );
    }
}

```



> state 사용 주의사항

- state를 업데이트를 할 때에는 setState 메소드를 통해서만 업데이트 해야 합니다.

  ```javascript
  //잘못된 코드의 예 입니다.
  this.state.number = this.state.number + 1;
  this.state.someArray.push(3);
  this.state.someObject.value=3;
  ```

- setState 메서드의 역할은 파라미터로 전달받은 필드를 업데이트한 후 컴포넌트가 리렌더링 하도록 동작합니다. 위와 같이 state에 직접 접근하여 값을 수정하면 컴포넌트를 자동으로 리렌더링 하지 않습니다. 이때, this.forceUpdate() 메소드를 호출하여 강제로 렌더링을 할 수 있지만 이 방식은 비효율적이므로 사용을 피해야 합니다.



> 정리

props와 state

- 공통점: 둘 다 컴포넌트에서 렌더링할 데이터를 담고 있습니다.

- 차이점: props는 부모 컴포넌트가 설정

​             state는 컴포넌트 자체적으로 지닌 값으로 내부적으로 값을 업데이트

- props 값이 고정적이라고 볼 수 있지만 그렇지 않다. 자식 컴포넌트에서 특정 이벤트가 발생할 때 부모 컴포넌트의 메서드를 호출하면 props도 유동적으로 변경될 수 있기 때문입니다.

![state&props](./img/state&props.PNG)



