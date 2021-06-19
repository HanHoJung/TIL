# 8장 함수형 컴포넌트

> 8.1 함수형 컴포넌트 사용법





### 8.1 함수형 컴포넌트 사용법

> 함수용 컴포넌트

- 컴포넌트 라이프사키를 API 사용
- state 사용

위와 같은 조건인 경우 반드시 다음과 같이 Component를 선언해야 합니다.

```jsx
import React, {Component} from 'react'

class Test extends Component{
    render(){
        return(
           <div>Hi</div>
        )
    }
}
```

만약, props를 전달받아 뷰를 렌더링하는 경우 위의 경우보다 간단하게 컴포넌트를 선언할 수 있습니다.

```jsx
import React, {Component} from 'react'

function Test(props){
    return(
       <div>Hi</div>
    )
}
```

```jsx
import React, {Component} from 'react'

const Hello = ({name})=>{
      return(
       <div>Hi {name}</div>
    )
}
```

```jsx
import React, {Component} from 'react'

const Hello = ({name})=>(
      return(
       <div>Hi {name}</div>
    )

```



<함수형 컴포넌트를 사용하는 경우>

- 컴포넌트에서 라이프사이클, state 등 불필요한 기능을 제거한 상태이기 때문에 메모리 소모량이 적다.

- 리액트 v16이상에서는 함수형 컴포넌트가 성능이 클래스형 컴포넌트 보다 빠르다.

- 리액트 프로젝트에서는 state를 사용하는 컴포넌트 개수를 최소하는것이 성능상 좋다. 따라서, 컴포넌트를 

  만들 때 state나 라이프사이클 API를 꼭 써야 할 때만 클래스 형태로 변환하여 컴포넌트를 작성하고 그 외에는

  함수형 컴포넌트로 작성한다.



