# 6장 컴포넌트 반복

> 6.1 데이터 배열을 컴포넌트 배열로 map 하기
>
> 6.2 key
>
> 6.3 응용
>
> 6.4 정리





### 6.1 데이터 배열을 컴포넌트 배열로 map 하기

>

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

