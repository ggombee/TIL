# const, function 차이.. 대체뭐얏!

```jsx
export const Mainpage = () => {}
export function Mainpage(){}
```

## Hoisting

가장 큰 이유는 호이스팅 때문이다. 

아래 valid 코드를 참고하자.

```jsx
// 컴포넌트를 쓰기전에 선언한 경우

const MyComponent = () => {}

const AlsoMyComponent = () => {}

const App = () => (
    <>
      <MyComponent />
      <AlsoMyComponent />
    </>
)
```

그리고? invalid 코드를 보자.

```jsx
const App = () => (
    <>
      <MyComponent />
      <AlsoMyComponent />
    </>
)

// 컴포넌트 선언을 아래에 하고싶은 경우

const MyComponent = () => {}

const AlsoMyComponent = () => {}
```

☝ 이 경우는 components are used before they are declared 에러가 날 것이다.

그러므로 만약 아래부분에 선언을 하고 싶은 경우에는 function 함수를 쓰면된다. (아래코드 참고)

```jsx
const App = () => (
    <>
      <MyComponent />
      <AlsoMyComponent />
    </>
)
// 컴포넌트 선언을 아래에 하고싶은 경우

function MyComponent() {}

function AlsoMyComponent() {}
```
