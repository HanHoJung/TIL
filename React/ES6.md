# ES6 문법

> 1.1 Arrow Function
>
> 1.2 Dynamic Object Keys



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


