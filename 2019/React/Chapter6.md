# 6장 컴포넌트 반복

> 6.1 데이터 배열을 컴포넌트 배열로 map 하기
>
> 6.2 key
>
> 6.3 정리





### 6.1 데이터 배열을 컴포넌트 배열로 map 하기

>map을 이용한 컴포넌트 반복

이렇게 작성하게 되면 화면에 보여지기는 하지만 **Warning: Each child in an array or iterator should have a unique "key" prop.~** 이라는 경고가 뜬다.

```jsx
import React,{Component} from 'react';

class IterationSample extends Component{

    render(){
        const names=['first','second','third'];
        const result=names.map(name=><li>{name}</li>);

        return(

            <div>
                <ul>
                    {result}
                </ul>
            </div>

        )
    };
}

export default IterationSample;
```



### 6.2 key

> key

리액트에서 어떤 원소에 변동이 있었는지 알아내기 위해서 key를 사용합니다. 예를 들어 유동적인 데이터를 다룰 때 원소를 생성, 제거, 수정 등의 작업을 할 수 있습니다. 만약, key가 없다면 가상 DOM을 비교하는 과정에서 리스트를 순차적으로 비교하면서 변화를 감지합니다. 하지만 key가 있다면 어떤 요소가 변했는지를 빠르게 알 수 있습니다.



> key 설정

- key의 값은 유일해야 합니다.
- props 설정하듯이 key를 설정하면 됩니다.

```jsx
import React,{Component} from 'react';


class IterationSample extends Component{

   render(){
    const names=['캡틴아메리카','타노스','아이언맨'];
    const nameList = names.map((name,index)=>
                    <li key={index}>{name}</li>);
        

    return(
            <div>
                <ul>
                {nameList}
                </ul>
            </div>

    );
   }

}

export default IterationSample;
```



> 응용

```jsx
class IterationSample extends Component{

    state={
        names:['눈사람','얼음','눈','바람'],
        name:''
    }

    handleChange=(e)=>{
        this.setState({
            name:e.target.value
        })
    }

    handleInsert=()=>{
        this.setState({
            names:this.state.names.concat(this.state.name),
            name:''
        })
    }
   render(){
    const nameList = this.state.names.map(
        (name,index) =>(<li key={index}>{name}</li> )
    )
        

    return(
            <div>
                <input
                    onChange={this.handleChange}
                    value={this.state.name}
                />

                <button
                    onClick={this.handleInsert}>추가</button>
                <ul>
                {nameList}
                </ul>
            </div>

    );
   }

}

```

- react에서는 배열에 값을 추가할 때 기존 배열과 새 값을 합친 새배열을 생성하는 concat 함수를 사용하여

  데이터를 추가합니다.

```jsx
class IterationSample extends Component{

    state={
        names:['눈사람','얼음','눈','바람'],
        name:''
    }

    handleChange=(e)=>{
        this.setState({
            name:e.target.value
        })
    }

    handleInsert=()=>{
        this.setState({
            names:this.state.names.concat(this.state.name),
            name:''
        })
    }

    handleRemove=(index)=>{
        //name의 레퍼런스
        const {names} = this.state;

        /*
            배열을 자르는 내장 함수 slice와 전개 연산자(...)를 사용하여 index번째 값을
            제외한 값들을 배열에 넣어 줍니다.
        */

        this.setState({
            names:[
                ...names.slice(0,index),
                ...names.slice(index+1,names.length)
            ]
        })
    }
   render(){
    const nameList = this.state.names.map(
        (name,index) =>(<li key={index} onDoubleClick={()=>this.handleRemove(index)}>{name}</li> )
    )
        

    return(
            <div>
                <input
                    onChange={this.handleChange}
                    value={this.state.name}
                />

                <button
                    onClick={this.handleInsert}>추가</button>
                <ul>
                {nameList}
                </ul>
            </div>

    );
   }

}


```

- ... 전개 연산자를 쓴 이유는 ES5로 만약 작성한 경우 코드가 길고 가독성이 떨어짐

  ```jsx
  this.state.names.slice(0,index).concat(this.state.names.slice,this.state.length)
  //가독성이 떨어짐
  ```

- filter 함수를 통해서도 제거할 수 있다.

  ```jsx
  import React,{Component} from 'react';
  
  
  class IterationSample extends Component{
  
      state={
          names:['눈사람','얼음','눈','바람'],
          name:''
      }
  
      handleChange=(e)=>{
          this.setState({
              name:e.target.value
          })
      }
  
      handleInsert=()=>{
          this.setState({
              names:this.state.names.concat(this.state.name),
              name:''
          })
      }
  
      handleRemove=(index)=>{
          //name의 레퍼런스
          const {names} = this.state;
  
          /*
              배열을 자르는 내장 함수 slice와 전개 연산자(...)를 사용하여 index번째 값을
              제외한 값들을 배열에 넣어 줍니다.
          */
  
          this.setState({
              names:[
                  ...names.slice(0,index),
                  ...names.slice(index+1,names.length)
              ]
          })
      }
  
      handleRemove2=(index)=>{
          const {names} = this.state;
          //filter로 index 번째를 제외한 원소만 있는 새 배열 생성
          this.setState({
              names:names.filter((item,i)=> i!==index)
          });
  
      }
     render(){
      const nameList = this.state.names.map(
          (name,index) =>(<li key={index} onDoubleClick={()=>this.handleRemove2(index)}>{name}</li> )
      )
          
  
      return(
              <div>
                  <input
                      onChange={this.handleChange}
                      value={this.state.name}
                  />
  
                  <button
                      onClick={this.handleInsert}>추가</button>
                  <ul>
                  {nameList}
                  </ul>
              </div>
  
      );
     }
  
  }
  
  
  ```


>6.3 정리

- 반복되는 데이터를 렌더링 하는 법을 알려주는 chapter 입니다.
- 컴포넌트 배열을 렌더링할 때는 key 값 설정에 주의해야 합니다. 
- key의 값을 언제나 유일해야하고 key 값이 중복이 되면 오류가 발생합니다.
- 상태 안에서 배열을 변형할 때는 배열에 직접 접근하여 수정하는 것이 아니라 concat, slice, 전개 연산자, filter함수 등을 사용해서 새 배열을 만든 후, setState 메서드를 적용해야 합니다.