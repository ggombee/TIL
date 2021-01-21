## Redux Toolkit

[https://redux-toolkit.js.org/](https://redux-toolkit.js.org/)

## React Hooks : useMemo 사용😊

### Memoization

기존의 수행한 연산의 결과값을 어딘가에 저장해두고 동일한 입력이 들어오면 재활용하는 프로그래밍 기법.

이를 적절히 적용하면 중복 연산을 피할 수 있기 때문에 메모리를 조금 더 쓰더라도 애플리케이션의 성능을 최적화 할 수 있다.

### 랜더링할때마다 호출되는 컴포넌트 함수

일반적으로 React의 함수형 컴포넌트는 다음과 같은 구조로 작성 된다.

```jsx
function MyComponent(props) {
  // 어떤 로직 (JavaScript)
  return /* 어떤 화면 (JSX) */
}
```

이렇게 작성된 컴포넌트 함수는 앱에서 랜더링이 일어날 때마다 호출이 된다. 컴포넌트 함수가 호출이 되면 그 안에 자바스크립트 로직들이 수행되고, 이를 기반으로 JSX로 마크업된 UI가 리턴되는 기본구조이다.

React에서 컴포넌트의 랜더링은 한 번 일어나고 끝이 아닌 수시로 계속 일어난다. 대표적인 예로 컴포넌트의 자신의 상태 변경이 일어날 수 있고, 아니면 부모 컴포넌트의 상태 변경이 일어나 덩달아 함께 랜더링되야 하는 경우도 있다. React에는 수동으로 다시 랜더링을 해주는 API도 있고,사용자가 브라우저에서 새로고침을 할 때도 컴포넌트의 재 랜더링은 불가피하다.

### 함수형 컴포넌트에 memoization 적용

랜더링이 일어날 때 마다, 비교하여 재랜더링을 한다면 UI가 지연되는 경험을 하게 될 것이다.

이때 필효한게 useMemo hook함수이다.

useMemo함수는 2개의 인자를 받는데, 첫번째는 결과값을 생성해주는 팩토리 함수이고, 두번째는 기존 결과값 재활용 여부의 기준이되는 입력값 배열이다. 

기존의 함수를 useMemo 함수의 첫번째 인자로 넘기고, 두 번째 인자로 prop이 든 배열을 넘긴다. 이렇게 해주면, 기존 함수는 두번째 prop이 달라졌을 때만 호출이 되고, 동일할 때는 최초 호출 결과가 계속해서 재사용된다.

이렇게 하면 입력 필드에 글자를 입력할때마다 지연이 발생하지 않는 것을 확인할 수 있다.

하지만 useMemo hook을 남용하면, 컴포넌트의 복잡도가 올라가기 때문에 코드를 읽기 어려워지고 유지보수성이 떨어질 수 있다. 또한 레퍼런스는 재활용을 위해서 가비지 컬렉션에서 제외되기 때문에 메모리를 더 쓰게 된다.

### create react app

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ef4e3af9-7ce4-4631-853a-665e1e2934c0/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ef4e3af9-7ce4-4631-853a-665e1e2934c0/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/275a2c0b-9611-4af4-b547-f9fe89714d78/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/275a2c0b-9611-4af4-b547-f9fe89714d78/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b52e67a2-d3e1-4419-bec6-b5e0fc1e22ed/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b52e67a2-d3e1-4419-bec6-b5e0fc1e22ed/Untitled.png)

### 타입스크립트 적용(이미 존재하는 프로젝트)

처음부터 아래명령어를 실행 시키면 타입스크립트로 적용된 프로젝트를 시작할 수 있다.

```jsx
npx create-react-app my-app --template typescript

#or

yarn create react-app my-app --template typescript
```

하지만 이미 존재하는 프로젝트에 타입스크립트를 적용시키려면 아래 명령어를 실행시켜주면 된다.

```jsx
npm install --save typescript @types.npde @types/react @types/react-dom @types/jest

#or

yarn add typescript @types/node @types/react @types/react-dom @types/jest
```

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/121a5a7a-b707-4985-9705-3250b4433de6/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/121a5a7a-b707-4985-9705-3250b4433de6/Untitled.png)

타입스크립트 코드를 작성하기 위해서는 typescript 패키지도 설치해야 한다.

```jsx
npm install --save-dev typescript
```

typescript 명령어를 이용하면 타입스크립트 설정 파일을 생성할 수 있다.

```jsx
npx typescript --init
```

tsconfig.json파일 자동 생성 후 compilorOptions에 jsx 속성에 'react'값을 추가해야 한다.

(기본으로 주석처리 되어 있으므로 풀고 추가한다)

```jsx
"compilorOptions": {
  "jsx": "react"
```

vscode는 이 tsconfig.json을 참고해서 타입스크립트 문법을 검사한다. 뿐만 아니라 웹팩에서 설정한 ts-loader가 이 파일을 참고해서 트랜스파일 작업을 하기 때문에 tsconfig.json 파일은 먼저 생성해야 한다.

이때 tsconfig.json파일에서 No inputs were found in config file Specified 'include' paths were '["**/*"]' and 'exclude' paths were '[]'.

비슷한 에러가 난다면 tsconfig.json과 같은 레벨에 typescript파일이 없는것이다.

ts파일 만들고 vsconde 껐다 키면 에러가 없어진다.

간단한 카운터 컴포넌트를 구현해보았다...ㅎㅎ

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0b750a26-7539-4497-b01a-e5b6eb430fef/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0b750a26-7539-4497-b01a-e5b6eb430fef/Untitled.png)

[https://medium.com/tapjoykorea/typescript-현업-적용-후기-caad266c8142](https://medium.com/tapjoykorea/typescript-%ED%98%84%EC%97%85-%EC%A0%81%EC%9A%A9-%ED%9B%84%EA%B8%B0-caad266c8142)

[https://musma.github.io/2019/03/05/typescript-getting-started.html](https://musma.github.io/2019/03/05/typescript-getting-started.html)
 
