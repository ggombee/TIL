

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
