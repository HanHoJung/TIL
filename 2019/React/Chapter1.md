# 1장 리액트 시작

> 1.1 왜 리액트 인가?
>
> 1.2 리액트 특징
>
> 1.3 작업 환경 설정



### 1.1 왜 리액트 인가?

- Javascript 개발영역의 확장

- 순수 Javascript만으로는 규모가 큰 애플리케이션을 관리하기 어려움이 문제를 해결하기 위해 나온것이 다양한 라이브러리 또는 프레임워크

  ex)Vue.js, React.js, Angular.js

```json
{
    "title":"라이온킹",
    "contents":"시몬과 품바",
    "author":"vitamin",
    "likes":1
}//model

<div>
	<div class="title">라이온킹</div>
	<div class="contents">시몬과 품바</div>
	<div class="author">Vitamin</div>
	<div class="likes">1</div>
<div>//view

/*
model에 key인 likes 값이 2로 변하게 되면 class="likes" 요소를 찾아 수정해야한다.
이렇게 단일 요소 하나를 변경할 때는 작업이 간단하지만 애플리케이션 규모가 커지게 되면 
복잡해지게 된다. 때문에, 변경 요소에 대해서 제대로 관리하지 않으면 성능상에 문제가 있다.

face book개발자는 이 문제를 해결하기 위해서 이러한 고민을 하였다.
- 모델의 데이터가 변경
- 기본 view를 날려버리고 새롭게 렌더링
=>위와 같은 idea를 가지고 접근

장점
- 더 이상 view에 어떻게 변화를 줄지 신경 쓸 필요가 없다.
- 작성 코드량 감소

단점
- 웹브라우저가 이 방식을 사용시, cpu 점유율 높아짐
- DOM은 느림
- 메모리가 많이 사용됨
- USER INPUT박스 텍스트 입력시 기존 렌더링 사라지고, 새로 렌더링하면 끊김 현상

=>단점을 많이 가지고 있기 때문에 위와 같은 문제를 해결하기 위해 나온것이 React
*/

```

> 1.1.1 리액트에 이해

- View에만 초점을 둔 라이브러리

- component

  - view의 특정 부분이 어떻게 생길지 정의하는 선언체
  - 템플릿과 다른 개념, 더욱 복합적 개념
  - 재사용 가능한 API로 수많은 기능 내장

- 렌더링

  - 화면에 뷰를 보여주는 것

  > 1.1.1.1 초기 렌더링

  - render(){...} 함수를 통해 렌더링 할 수 있다.

  - component가 어떻게 생겼는 정의하는 역할

  - render함수는 html 형식의 문자열이 아닌 **view가 어떻게 작동하는지 정보를 지는 객체 반환**

  - 초기 렌더링 절차

    - 렌더링 한다.

    - 렌더링한 정보를 가지고 HTML 마크업을 생성한다.

    - 실제 페이지의 DOM 요소 안에 주입된다.
  > 1.1.1.2 조화 과정(reconciliation)

  - 뷰를 업데이트를 하는 과정을 "조화 과정"을 거친다 한다.
  - 컴포넌트의 데이터의 변화가 있을때, 데이터를 새로운 요소로 갈아 끼우게 된다.
  - render함수를 통해 조화 과정이 이루어진다. 
  - 그 후, 바로 DOM에 주입되지 않는다.
  - 이전에 render 함수가 만들었던 컴포넌트 정보와 현재 render함수가 만든 컴포넌트 정보를 비교한다. 
  - 이전 DOM 트리와 새로운 DOM트리를 root부터 비교한 후 변경 부분을 찾고 DOM 트리를 업데이트 한다.



### 1.2 리액트의 특징

- DOM(Document Object Model)

  - 객체로 문서 구조를 표현하는 방법(XML이나 HTML를 이용하여 작성)

  - 웹 브라우저는 DOM을 활용하여, JS와 CSS적용

  - 트리 형태 이므로 특정 NODE의 삽입/삭제/수정 가능

  - 동적 UI에 최적화 되지 않았다. 그 이유는 HTML 자체적으로 정적파일임 JS에 의해 동적으로 만들 수 있다.

    ex)

    페이스북,post 한개를 표시하는 div태그 약 100개

    기존의 방식:DOM에 직접 접근하여 변화를 줌, 성능 이슈

  - DOM 자체는 빠름 그러나 DOM에 변화가 일어나면 웹브라우저가 CSS 재연산, 레이아웃 재구성

    페이지를 다시 그림 이 과정에서 많은 시간이 허비

    =>해결법

    - DOM을 최소한으로 조작하여 작업을 처리

    - Virtual DOM 적용

    - 실제 DOM에 접근하여 조작하는 방법 대신, 이를 추상화한 자바스크립 객체를 구성하여 사용

    - 1.데이터를 업데이트하면 전체 UI를 Virtual DOM에 리렌더링

    - 2.이전 Virtual DOM에 있던 내용과 현재 내용을 비교

    - 3.바뀐 부분만 실제 DOM에 적용

    - Virtual DOM을 사용한다고 무조건 빠른것은 아니다. Virtual DOM을 사용하지 않고 코드 최적화를 이루면 그것이 대체 수단이 될 수 있다. 그러나 Virtual DOM은 UI 업데이트 과정을 쉽게 제공한다.


[참고자료]

 https://www.youtube.com/watch?v=muc2ZF0QIO4

https://velopert.com/3612

https://velopert.com/3236

https://d2.naver.com/helloworld/59361

```
To do
아직 React 개념에 대해서 간략하게 알지 깊게는 이해할 수 있는 수준은 아닌것 같다.
이를 이해하기 위해서는 브라우저의 동작원리에서 공부한 후 차후에 이해하도록 해야겠다.
```



### 1.3 작업 환경 설정(window)

패키지 관리자 install `yarn`

https://yarnpkg.com/en/docs/install#windows-stable

에디터 vscode 패키지

- ESLint

- Relative Path

- Guides

- React js code snippets

```bash
yarn global create-react-app
create-react-app hello-react
yarn start
```

