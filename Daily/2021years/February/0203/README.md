### ESLint: 'React' is defined but never used. (no-unused-vars)

```jsx
rules: { 'no-unused-vars': 'off', 'react/react-in-jsx-scope': 'off' },
```

# Styled-Component

CSS in JS를 의미한다. 문구 그대로, CSS를 JS 안에 작성하는 것을 의믜합니다.

```jsx
$ yarn add styled-components
```

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

## TDZ

TDZ(Temporal Dead Zone)은 let, const, class 구문의 유효성을 관리한다. 자바스크립트에서 변수가 동작하는 방식은 중요하다.

TDZ 시맨틱은 선언 전에 변수에 접근하는 것을 금지한다. TDZ는 징계를 내린다: 변수 선언 전에 어떤 것도 사용하지 않는다.

const 변수는 선언 및 초기화 전 줄까지 TDZ에 있다.

let도 선언 전 줄까지 TDZ의 영향을 받는다.

머리말 부분에서 보았듯이, 선언 전에는 class를 사용할 수 없다.

부모 클래스를 상속받았다면, 생성자 안에서 super()를 호출하기 전까지 this 바인딩은 TDZ에 있다.

```jsx 
class MuscleCar extends Car {
  constructor(color, power) {
    this.power = power;
    super(color);
  }
}

// Does not work!
const myCar = new MuscleCar(‘blue’, ‘300HP’); // `ReferenceError`
```

이 코드를 보면 constructor() 안에서 super()가 호출되기 전까지 this를 사용할 수 없다.

TDZ는 인스턴스를 초기화하기 위해 부모 클래스의 생성자를 호출할 것을 제안한다. 부모 클래스의 생성자를 호출하고 인스턴스가 준비되면 자식 클래스에서 this 값을 변경할 수 있다.

```jsx
class MuscleCar extends Car {
  constructor(color, power) {
    super(color);
    this.power = power;
  }
}

// Works!
const myCar = new MuscleCar('blue', '300HP');
myCar.power; // => '300HP'
```

### 결론

TDZ는 `const`, `let`, `class` 구문의 유효성에 영향을 미치는 중요한 개념이다. TDZ는 선언 전에 변수를 사용하는 것을 허용하지 않는다.

반대로 `var` 변수는 선언 전에도 사용할 수 있기 때문에 `var` 사용은 피하는 것이 좋다.

TDZ는 언어 스펙에 맞도록 좋은 코딩 습관을 만들어주기 때문에 좋다고 생각한다.

참고 : [https://ui.toast.com/weekly-pick/ko_20191014](https://ui.toast.com/weekly-pick/ko_20191014)

## 절대경로 설정

[https://hoons-up.tistory.com/27](https://hoons-up.tistory.com/27)
