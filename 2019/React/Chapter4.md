# 4장 이벤트 핸들링

> 4.1 리액트의 이벤트 시스템
>
> 4.2 예제로 이벤트 핸들링 익히기
>
> 4.3 정리



**이벤트**

이벤트란 User가 웹 브라우저의 DOM 요소들과 상호작용하는 것을 의미합니다.




### 4.1 리액트의 이벤트 시스템

리액트이 event 처리는 html 이벤트 처리 방식과 유사합니다.

> 이벤트 사용 주의사항

- event 이름은 camelCase로 작성합니다.

  예를 들어, onclick event는 **onClick**으로 작성합니다.

- DOM 요소에만 이벤트를 설정할 수 있습니다.

  DOM의 요소 div, button, input, form 태그 등에는 다양한 이벤트를 설정할 수 있지만

  우리가 직접 만든 **컴포넌트** 자체에는 이벤트를 자체적으로 설정할 수 없습니다.

  ```jsx
  <MyComponent onClick={doSomething}/>
  /*
  MyComponent를 클릭할 때 doSomething 함수를 실행하는게 아니라 onCliCK 이라는 이름의 props를
  전달하는 의미를 가집니다.
  */
  ```

- event에 실행할 자바스크립트 코드가 아닌 함수 형태의 값을 전달합니다.


- 다양한 이벤트 종류(https://facebook.github.io/react/docs/events.html)



### 4.2 이벤트 핸들링

> event 등록 함수 작성방법(1) =>랜더링 함수 내에 event 처리 함수 작성

```jsx
class EventPractice extends Component{

    state={
        name:''
    }
    render(){
        
        return(
            <div>
                <h1>이벤트 연습</h1>
                <input
                    type="text"
                    name="message"
                    placeholder="입력해보세요"
                    onChange={
                        (e)=>{
                            console.log(e); 
                        /*
                          e 객체는 SyntheticEvent로 웹 브라우저의 native 이벤트를 감싸는 객체
                          이므로 순수 자바스크립트에서 사용하는 방식처럼 사용하면 됩니다.
                            */
                           this.setState({
                               name:e.target.value
                           })
                           console.log(this.state.name);
                        }
                    }
                />

                <button
                    onClick ={
                        (e)=>{
                            alert(this.state.name);
                            this.setState({
                                name:''
                            })
                        }
                    }
                
                    >확인</button>       
            </div>
        )
    }
}

export default EventPractice;
```



> event 등록 함수 작성방법(2)=> 임의 메서드 만들기

- 성능상의 차이는 없지만 이 방법이 가독성이 더 높다.

- 컴포넌트에 임의 메서드를 만들면, 메서드 내에서 this에 접근할 수 없습니다. 때문에 컴포넌트 생성자

  메서드 constructor에서 각 메서드를 this와 binding 해주는 작업이 필요합니다.

  ```jsx
   constructor(props){
          super(props);
          this.handleChange = this.handleChange.bind(this);
          this.handleClick = this.handleClick.bind(this);
      }
  
  ```

  ```jsx
  class EventPractice extends Component{
      state={
          name:''
      }
  
      constructor(props){
          super(props);
          this.handleChange = this.handleChange.bind(this);
          this.handleClick = this.handleClick.bind(this);
      }
  
      handleChange(e){
          
          this.setState({
              name:e.target.value
          })
      }
  
      handleClick(e){
          alert(this.state.name);
          this.setState({
              name:''
          });
      }
      
      render(){
          
          return(
              <div>
                  <h1>이벤트 연습</h1>
                  <input
                      type="text"
                      name="message"
                      placeholder="입력해보세요"
                      onChange={this.handleChange}
                      value={this.state.message}
                      />
  
                  <button onClick ={this.handleClick}>확인</button>    
              </div>
          )
      }
  }
  ```

- 원칙적으로는 bind를 constructor에서 해야하지만 props와 state에서 값 setting 쉽게 했던 것처럼 특정 문법을 사용하여 화살표 함수 형태로 메소드를 정의할 수 있다.(Property Initializer Syntax를 사용한 메소드 작성)

  ```jsx
  class EventPractice extends Component{
      state={
          name:''
      }
  
  
      handleChange=(e)=>{
          this.setState({
              name:e.target.value
          })
      }
  
      handleClick=(e)=>{
          alert(this.state.name);
          this.setState({
              name:''
          });
      }
      
      render(){
          
          return(
              <div>
                  <h1>이벤트 연습</h1>
                  <input
                      type="text"
                      name="message"
                      placeholder="입력해보세요"
                      onChange={this.handleChange}
                      value={this.state.message}
                      />
  
                  <button onClick ={this.handleClick}>확인</button>    
              </div>
          )
      }
  }
  ```



> input 여러 개의 핸들링

- input 태그가 여러개 존재하고 각 event가 발생할 때 마다 state 값을 변경한다고 하자

  그렇게 되면 각 input 태그마다 임의의 메소드를 만들어줘야 한다. 이 문제를 효율적으로 해결하는

  방법이 있다.

  임의의 하나의 메소드를 만들고 이러한 식으로 logic을 처리하는 것이다.

  ```jsx
  this.setSte({
      [e.target.name]:e.target.value
  })
  ```

  ```jsx
  class EventPractice extends Component{
      state={
          username:'',
          message:''
      }
  
  
      handleChange=(e)=>{
          this.setState({
              [e.target.name]:e.target.value
          })
      }
  
      handleClick=(e)=>{
          alert(this.state.username+":"+this.state.message);
          this.setState({
              username:'',
              message:''
          });
      }
  
      handleKeyPress=(e)=>{
          if(e.key==='Enter'){     
              this.handleClick();
          }
      }
      
      render(){
          
          return(
              <div>
                  <h1>이벤트 연습</h1>
                 
                  <input
                      type="text"
                      name="username"
                      placeholder="유저명"
                      onChange={this.handleChange}
                      value={this.state.username}
                      />
  
                  <input
                      type="text"
                      name="message"
                      placeholder="입력해보세요"
                      onChange={this.handleChange}
                      onKeyPress={this.handleKeyPress}
                      value={this.state.message}
                      />
  
                  <button onClick ={this.handleClick}>확인</button>    
              </div>
          )
      }
  }
  
  ```






