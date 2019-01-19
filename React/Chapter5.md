# 5장 ref:DOM에 이름달기

> 5.1 ref는 어떤 상황에서 사용해야 할까?
>
> 5.2 ref 사용법
>
> 5.3 컴포넌트에 ref 달기
>
> 5.4 정리



> ref란

DOM에 id를 통하여 css를 통한 스타일, javascript를 인한 동적 처리가 가능해집니다. 또한, src/index.js 파일 중에는 id가 root인 요소에 리액트 컴포넌트를 렌더링하라는 코드가 있습니다.

```javascript
ReactDOM.render(<App />, document.getElementById('root'));
```

html에서 id를 사용하여 DOM에 이름을 부여하는 것처럼 리액트 프로젝트 내부에서 DOM에 이름을 다는 방법이 바로 ref(reference) 입니다.

cf)

리액트 컴포넌트 안에서 id를 사용할 수 있지만 권장하지 않는 방법 입니다. 그 이유는 여러개의 컴포넌트를 사용했을 때 만약 중복 id를 가진 DOM이 생기면 **유일성**이 깨지기 때문입니다. 반면, ref는 전역적으로 동작하지 않고 컴포넌트 내부에서만 작동하기 때문에 문제가 생기지 않습니다.



### 5.1 ref는 어떤 상황에서 사용해야 할까?

> ref의 상황

ref를 사용하지 않고 state 만으로도 우리에게 필요한 기능을 구현할 수 있습니다. 그러나 state 만으로는 해결할 수 없는 문제가 있습니다. 이때는 ref를 사용해야 합니다.

**ref를 사용해야 하는 경우**

- 특정 input에 포커스 주기
- 스크롤 박스 조작하기
- Canvas 요소에 그림 그리기 등



### 5.2 ref 사용법

> ref 사용

```jsx
<input ref={(ref)=>{this.input=ref}}</input>
//this.input(ref의 이름)은 input 요소의 DOM을 가르킴
//ref의 이름은 자유롭게 설정가능 this.superman=ref 
```

```jsx
import React,{Component} from 'react'
import './ValidateSample.css'
class ValidateSample extends Component{

    state={
        password:'',
        clicked:false,
        validate:false   
    }

    handleOnchanged=(e)=>{
        const pw = e.target.value;
        this.setState({
            password:pw
        });
    }

    handleClicked=(e)=>{

        this.setState({
            clicked:true,
            validate:this.state.password==='0000'
        });
        this.input.focus();//특정 DOM에 focus를 주는 것은 ref만 가능
    }


    render(){
        return(

            <div>
                <input 
                    ref={(ref)=>{this.input=ref}}
                    type="password" 
                    value={this.state.password} 
                    className={this.state.clicked?(this.state.validate?'success':'fail'):''} 
                    onChange={this.handleOnchanged} />
                <button tpye="button"
                        onClick={this.handleClicked}
                >Validate</button>
            </div>   
        );
    }
}

export default ValidateSample;

/*

input 태그
1. 데이터 입력 =>onChanged event 발생하고 password값 변경시킨
2. click event 발생시=> 
                        0000 =>state 상태가 success true
                        !0000=>state 상태가 fail true

*/
```



### 5.3 컴포넌트에 ref 달기

> 컴포넌트 ref

컴포넌트 자체에도 ref를 등록할 수 있습니다. 보통, **컴포넌트 외부**에서 컴포넌트 내부에 있는 DOM을  사용할 때 쓰입니다.

```jsx
import React, { Component } from 'react';
import ScrollBox from './ScrollBox';
class App extends Component {
  render() {
    /*
    ScrollBox Component를 ref로 등록했기 때문에
    scrollToBottom을 호출할 수 있음

    onClick={this.scrollBox.scrollToBottom}
    이렇게 작성해도 되지만(문법적 오류는 없지만)
    "컴포넌트 처음 렌더링"
    this.scrollBox 값이 undefined이므로 
    this.scrollBox.scrollToBottom 값을 읽어오는 과정에서 오류 발생
    때문에, 아래와 같이 코드를 작성한다. button 누를때(onClick event)
    화살표 함수 문법을 사용하여 새로운 함수를 만들고 그 내부에서 
    this.scrollBox.scrollToBottom을 실행하기 때문에 오류가 발생하지 
    않음
    */
    return (
      <div className="App">
        <ScrollBox ref={(ref)=>this.scrollBox=ref}/>
            <button onClick={()=>{
              this.scrollBox.scrollToBottom()}}>  
            맨 아래로</button>
      </div>
    );
  }
}

export default App;

```

```jsx
import React,{Component} from 'react';

class ScrollBox extends Component{
    scrollToBottom=()=>{
    /*
        scrollTop:세로 스크롤바 위치(0~350)
        scrollHeight:스크롤 박스 내부의 높이(650)
        clientHeight:스크롤 박스 외부의 높이(300)
    */

    const {scrollHeight, clientHeight} = this.box;
    this.box.scrollTop = scrollHeight - clientHeight;

    }

    render(){

        const style ={
            border:'1px solid black',
            height:'300px',
            width:'300px',
            overflow:'auto',
            position:'relative'
        };

        const innerStyle={
            width:'100%',
            height:'650px',
            background:'linear-gradient(white,black)'
        }
        return(
            <div style={style}
                 ref={(ref)=>{this.box=ref}}>
              <div style={innerStyle}/>

            </div>
        )
    };

}

export default ScrollBox;
```



### 5.4 정리

> 정리

- 해당 기능을 구현할 때 ref를 사용하지 않고도 구현할 수 있는지르 고려한 후에 사용하게 좋다.

  서로 다른 컴포넌트끼리 데이터를 주고 받을 때 ref를 사용하는것은 잘못된 사용 입니다.

  문법적으로는 할 수 있지만, 컴포넌트에 ref를 달고 그 ref를 다른 컴포넌트에 전달하고  또 다른 컴포넌트에서 그 ref로 전달받는 메소드를 실행하게 되면 리액트 사상과 어긋나는 설계 입니다. 앱의 구조가 커지면 커질 수록 이러한 설계는 스파게티 구조가 되기 때문입니다.

- 데이틀 교류할 때는 부모와 자식 흐름으로 교류해야 합니다.