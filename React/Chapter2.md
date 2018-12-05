# 2장 JSX

> 2.1 코드 이해
>
> 2.2 JSX란?
>
> 2.3 JSX 장점
>
> 2.4 JSX 문법
>
> 2.5 정리



### 2.1 코드 이해

- 번들링 도구, 파일들을 묶듯이 연결하는 기능을 한다.(webpack, browserify)

- 브라우저에서는 require, import 같은 js 기능을 사용하지 못한다. 이러한 기능은 node.js 환경에서 가능하다.

  브라우저에서는 script 태그를 추가하여 js 파일을 추가한다. 그러나 webpack은 js의 require, import 기능을 사용할 수 있다. require, import 문을 통해 만들어진 모듈들을 하나의 파일로 만들어 준다. 

- 우리 프로젝트에서는 src/index.js를 시작으로 필요한 파일을 다 불러온 후에 파일 하나로 합쳐준다.

- 예를 들어 모듈 A, 모듈 B,  모듈 C가 있는데 연관 되는 파일을 하나로 합쳐서

  만들어 주는 역할을 한다.

- js 파일 뿐만 아니라 SVG, CSS 파일도 webpack으로 불러올 수 있다.  require, import 문은 js만 가능한데 이를 가능하게 하는것이 webpack loader 

- loader의 종류는 css-loader, file-loader, babel-loader 등 다양하다.

- create-react-app은 이러한 설정들을 다 맞춰줌

  ```javascript
  import logo from './logo-svg'
  import './App.css'
  ```



### 2.2  JSX란?

- js의 확장문법으로 xml과 비슷
- jsx로 작성된 코드는 webpack에 의해 번들링되면서  babel-loader를 통해 js로 변환된다.



### 2.3  JSX 장점

> 작성하기 편하다.

- js를 통해서도 작성할 수 있지만, jsx를 사용하여 코드를 만들면 간결하고 가독성이 높다.
- html을 작성하는것과 비슷하다.



> 오류 검사

- jsx에 오류가 있을때, 바벨이 코드를 변환(js) 하는 과정에서 이를 감지



### 2.4. JSX 문법

> 2.4.1 감싸인 요소

return 문 안에서,  각 태그 element는 부모 요소로 감싸야 한다. 그 이유는 Virtual DOM에서 컴포넌트 변화를 감지해 낼 때 효율적으로 비교할 수 있도록 컴포넌트 내부는 DOM 트리구조를 지켜야한는 규칙있기 때문이다.

```jsx
//error

import React, {Component} from 'react
class App extends Component{
  render(){
    return(
        <h1>안녕 리액트</h1>
        <h1>당신은 어썸하신가요?</h1>
    )
    };
  }
}

exprot default App


import React, {Component} from 'react'

class App extends Component{
  render(){
    return(
       <div>
        <h1>안녕 리액트</h1>
        <h1>당신은 어썸하신가요?</h1>
       </div>
    )
    };
  }
}

exprot default App
```



>  2.4.2 Fragment, 자바스크립트 표현

- div 태그를 감싸지 않고 싶을 때는 Fragment를 불러와서 사용한다.

  불필요한 div를 랜더링을 하는것을 막음

- js표현식을 쓸려면 jsx 내부에서 {코드} 형식으로 작성한다.

  ```jsx
  import React, {Component} from 'react'
  
  class App extends Component{
  
    render(){
        const name = "hojung";
      return(
      <fragment>
        <h1>Hello React</h1>
        <h1>{name}</h1>
      </fragment>
      )
      
    }
  }
  
  export default App
  ```



> 2.4.3 if문 대신 조건부 렌더링(삼항연산자 또는 &&)

- jsx 안 에서는 if문을 사용할 수 없다. 대신 삼항 연산자를 사용한다.

```jsx
import React,{Component} from 'react'

class App extends Component{
  
    render(){
      const first = "참"
      const second = "거짓"
      const check = true
      return(
        <div>
          {
            check ? first:second
          }
        </div>
      )
    }

}

export default App;
```

> 2.4.4 인라인 스타일링

- DOM 요소에 문자열 형태로 CSS 스타일 적용 가능
- CSS 스타일을 자바스크립트 객체 형식으로 만들어야 한다.
- className으로 작성

```jsx
import React, {Component} from 'react';

class App extends Component{

  render(){
    const text = "HanHoJung";
    const style ={
      backgroundColor: 'gray',
      border:'1px solid black',
      height:Math.round(Math.round()*300)+50,
      width:Math.round(Math.round()*300)+50,
      WebkitTransition:'all',
      MoZTransition:'all',
      MSTransition:'all'
    }
      return(
        <div>
          <h1 style={style}>
              {text}
          </h1>
        </div>
      )

    }
}

export default App
```



> 2.4.5 class 대신 className

- 객체의 Key는 camelCase로 작성한다.

```jsx
import React, {Component} from 'react';
import './App.css';

class App extends Component{
    render(){

      return(
        <div className='my-div'>
          <h1>리액트 안녕!</h1>
        </div>

    )

  }
}

export default App;
```



> 2.4.6 꼭 닫아야 하는 태그

- html에서는 태그 중에 input, br 태그는 닫지 않아도 문제가 생기지 않는다.

  그러나 jsx에서 이렇게 작성하면, Virtual Dom 트리 구조를 만들지 못하므로 무조건 닫아줘야 한다.

```jsx
import React, {Component} from 'react';
import './App.css';

class App extends Component{
    render(){

      return(
        <form>
          First name:<br/>
          <input type="text" name="firstname" /><br/>

          Last name:<br/>
          <input type="text" name="lastname" /><br/>
        </form>

    )

  }
}

export default App;
```



> 2.4.7 주석

- 주석 작성시 { /*  주석 내용  */} 이렇게 작성해야 한다.

```jsx
import React, {Component} from 'react';
import './App.css';

class App extends Component{
    render(){

      return(
        <form>
          First name:<br/>
          <input type="text" name="firstname" /><br/>
          {/*주석 */}
          /*주석 */
          Last name:<br/>
          <input type="text" name="lastname" /><br/>
        </form>

    )

  }
}

export default App;
```



참고)

https://velopert.com/3626

ReactDom.render(argv1, argv2)

argv1:페이지에 렌더링할 내용을 jsx로 작성

argv2:jsx를 렌더링 할때 document 내부 요소 결정

//public/index.html 파일안에 있음