# ES6 문법

> 1.1 Arrow Function
>
> 1.2 Dynamic Object Keys
>
> 1.3 Destructurning assignment
>
> 1.4 Map



### 1.1 Arrow Function

> arrow function 

- ES6 문법에서 함수를 표현하는 새로운 방법 입니다.

- 기존 function 이용한 함수 선언 방식을 완전히 대체하지는 않습니다.

  기존 function의 this는 자신이 종속된 객체를 this로 가리키며, 

  화살표 함수는 자신이 종속된 인스턴스를 가르킵니다.

- 주로 함수를 파라미터로 전달할 때 유용합니다.

- 값을 연산하여 바로 반환 해야할 때 사용하면 가독성이 높습니다.

```javascript
setTimeout(function(){
    	console.log('Hello Coding')
},1000);
    
setTimeout(()=>{
        console.log('Hello Coding')
    },1000);
```

```javascript
function BlackDog(){
    this.name = '흰둥이';
    return{
        name:'검둥이',
    	bark:function(){
        console.log(this.name + ': 멍멍!');
		 }
    }
}

const blackDog = new BlackDog();
blackDog.bark(); //검둥이:멍멍!


function WhiteDog(){
    this.name='흰둥이'
     return{
        name:'검둥이',
    	bark:()=>{
        console.log(this.name + ': 멍멍!');
		 }
    }
}

const whitekDog = new WhiteDog();
whitekDog.bark(); //흰둥이:멍멍!
```

```javascript
function twice(value){
    return value * 2;
}

const triple =(value) => value * 3;
//{}을 해주지 않으면 연산한 값을 그대로 반환한다는 의미를 가지고 있습니다.
```



### 1.2 Dynamic Object Keys(동적 객체 키)

- ES6에서는 [myKey] 대괄호 구문을 사용하여 계산된 값을 객체 리터럴 키로 사용할 수 있습니다.

```javascript
const chosenAnimal = 'cat'
const animals = {
  [`animal${chosenAnimal}`]: true,
}
console.log(animals.animalcat) // true
```

https://blog.wonhada.com/?p=3041





### 1.3  Destructurning assignment(비구조화 할당 문법)

- 비구조화 할당 문법은 **객체에서**  <u>특정 값을 추출</u>해서  따로 **레퍼런스**를 만들 때 효과적 입니다.

- 함수의 인자로도 전달할 수 있습니다.

  ```javascript
  const object = {
      foo:1,
      bar:2
  }
  
  const {foo, bar} = object;
  console.log(foo,bar); //1 2
  
  function print({foo, bar}){
      consolt.log(foo,bar);
  }
  ```

- 이 문법은 리액트 컴포넌트에서 state, props 값을 참조할 때 사용합니다. 코드 가독성과 편리함이 있기 때문입니다. 

  ```jsx
  render(){
      return(
      	<div>
      		<div>{this.props.name}</div>
      		<div>{this.props.number}</div>
      	</div>
      
      )
  }
  //비구조 문법 사용
  render(){
      const {name, number} = this.props;
      return{
         <div>
          <div>{name}</div>
          <div>{number}</div>
         </div>     
      }
  }
  ```





### 1.4 map()함수

자바스크립트 map(배열 객체 내장 함수) 을 이용하면 반복되는 컴포넌트를 렌더링 할 수 있습니다.

> 동작:parameter로 전달된 함수를 사용해서 배열 내 각 요소를 처리한 후, 그 결과로 새로운 배열을 생성함

> 문법

arr.map(callback,[thisArg])

- callback:새로운 배열의 요소를 생성하는 함수로 파라미터는 세가지
  - currentValue:현재 처리하고 있는 요소
  - index:현재 처리하고 있는 요소의 index 값
  - array:현재 처리하고 있는 원본 배열
- thisArg:callback 함수 내부에서 사용할 this 레퍼런스



```javascript
//ES5
var numbers = [1,3,4,5];
var processed = numbers.map(function(num){
   	return num * num; 
});
console.log(processed);


//ES6
const numbers = [1,3,4,5]
const processed = numbers.map(num=>num*num);
console.log(processed);

```

