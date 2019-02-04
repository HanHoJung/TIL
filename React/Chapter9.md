# 9장 컴포넌트 스타일링

> 9.1 CSS Module
>
> 9.2 Sass
>
> 9.3 styled-components
>

cf)

https://velog.io/@velopert/react-component-styling //CRA 1.1.5버전으로 업데이트에 따른 style방식 변화

yarn이나 npm으로 설치한 패키지 내부 파일을 불러올 때는 ~문자를 사용해서 node_modules에 접근할 수 있다.

<컴포넌트 스타일ㄹ링>

> css module

- css를 모듈화하여 사용하는 방식
- css 클래스를 만들면 자동으로 고유한 클래스 네임을 생성하여 스코프를 지역적으로 제한하는 방식
- 모듈화한 css를 webpack으로 불러오면 **사용자가 정의한 클래스 네임**과 **고유한 클래스 네임**으로 구성된 객체가 반환됨

> sass

- 자주 사용되는 css 전처리기 중 하나
- 확장된 css 문법을 사용하며, css를 작성하게 편한게 해줌

> styped-components

- JS 코드 내부에서 스타일을 정의



`create-react-app` 명령으로 만든 프로젝트에서

`yarn eject` 명령을 실행하면 node_modules/react-scripts 내에 리액트 프로젝트 환경설정 파일들이 루트경로로 옮겨진다.



### 9.1 CSS Module

> CSS Module

- css를 모듈화하여 사용하는 방식

- css 클래스를 만들면 자동으로 고유한 클래스 네임을 생성하여 스코프를 지역적으로 제한하는 방식

- 모듈화한 css를 webpack으로 불러오면 **사용자가 정의한 클래스 네임**과 **고유한 클래스 네임**으로 구성된 객체가 반환됨

  ```json
  {
       box:'src-App_ _box-mjrNr'
  }
  ```

- 클래스를 적용할 때는 `className={styles.box}` 이런식으로 사용

- webpack 파일을 수정하여 적용

  - css를 불러올 때는 보통 세 가지 로더를 사용

    - https://ideveloper2.tistory.com/143

    - css-loader: css파일에서 import와 url(...)문을 webpack의 require 기능으로 처리

    - style-loader: 스타일을 불러와 웹 페이지에서 활성화하는 역할

    - postcss-loader:모든 웹 브라우저에서 입력한 css 구문이 잘 동작할 수 있도록 접두사(-webkit,-mos,-ms) 를 붙여줌

- css module을 적용하면 class명이 중복이 되서 충돌될일이 없습니다.
- classnames 모듈을 사용하면 더 편리하게 css 모듈을 사용할 수 있습니다.      
  - 조건부 스타일링할 때 매우 편리하다.



​      



### 9.2 Sass

> sass

- css 문법을 확장하여 css를 좀 더 편리하게 사용하게 도와줍니다.
- https://sass-guidelin.es/ko/ 
- webpack 파일을 수정하여 적용
  - node-sass: Sasss로 작성한 코드를 CSS로 변환한다.
  - sass-loader:webpack에서 Sass 파일을 읽어오도록 도와준다.
- nested 구조로 코드를 작성할 수 있어서 가독성과 편리함을 높여준다.
- sass Library
  - include-media:믹스인 라이브러리, 반응형 디자인을 도와준다.
  - open-color:변수 세트 라이브러리, 여러가지 색상을 쉽게 고를 수 있게 도와준다.
  - https://yeun.github.io/open-color/





### 9.3 Styled-components

> Styled-components

- 자바스크립트 파일 안에 스타일을 선언하는 방식(CSS in JS)

- styled-components 라이브러릴 제일 많이 사용

  https://github.com/MicheleBertoli/css-in-js









