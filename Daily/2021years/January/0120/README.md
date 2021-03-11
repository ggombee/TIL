# 프로젝트 폴더 구조 및 세팅 하기

## [React] DOM 전달

HTML 파일 어딘가에 <div> 속 모든 엘리먼트를 React DOM에서 관리하기 때문에 이것을 "루트" DOM노드라고 부른다. 

React 엘리먼트를 루트 DOM에 렌더링하려면 ReactDOM.render()를 사용한다.

![Untitled](https://user-images.githubusercontent.com/58289110/105181709-7f4a3800-5b6f-11eb-8ed7-0863855e078a.png)

### React.Element

타입스크립트일때 element의 리턴타입을 명시...(ㄱㅁㄴ..)

## Context API

## Helmet

## Provider

## Router
 
## Swiper

## [JS] export/exports/export default

자바스크립트에서 모듈화를 시켜 나누어져있는 파일의 필요한 값을 내보내고 가져올 때 export, import, require의 차이, 그리고 export의 종류와 사용법을 제대로 알아야 할 것 같다.

export 할 경우에는 import { 함수명 } from * 으로 사용하는데,

export default 하실 경우에는 import 함수명 from * 으로 사용하게 된다.

1. export - JS 모듈에서 함수, 객체, 원시값을 내보낼 때 사용
2. exports - 모듈에서 함수, 객체, 원시값을 객체의 형태로 내보낼 때 사용
3. export default - 분리되어 있는 파일 내 내보낼 하나의 고정된 값만 내보낼 때 사용

## NAS

Network Attached Storage 네트워크 결합 스토리지...

[참조]

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/export](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/export)

[https://enro2414-40667.medium.com/자바스크립트-export-import정리-137ac9e327d9https://enro2414-40667.medium.com/자바스크립트-export-import정리-137ac9e327d9](https://enro2414-40667.medium.com/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-export-import%EC%A0%95%EB%A6%AC-137ac9e327d9)

[https://velog.io/@jch9537/Javascript-export-default](https://velog.io/@jch9537/Javascript-export-default)

## 리액트 컴포넌트 스타일링 하기

### Sass

```jsx
$ yarn add node-sass
```

### CSS Module

```jsx
import styles from './CheckBox.module.css';
import classNames from 'classnames/bind';

const cx = classNames.bind(styles);
```

### styled-components

```jsx
$ yarn add styled-components
```

App 컴포넌트를 열어서 다음과 같이 styled-components 로 스타일링한 첫번째 컴포넌트를 만들어본다.

```jsx
import React from 'react';
import styled from 'styled-components';

const Circle = styled.div`
  width: 5rem;
  height: 5rem;
  background: black;
  border-radius: 50%;
`;
 
function App() {
  return <Circle />;
}

export default App;
```
 
[참조]

[https://react.vlpt.us/styling/03-styled-components.html](https://react.vlpt.us/styling/03-styled-components.html) - css
