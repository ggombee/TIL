## 기존의 React-Redux

action, reducer, store 필요

- Flow : action 객체 정의 → 리듀서가 액션에 담긴대로 state생성 → store는 새로운 state 저장

🤷‍♀️ 개발 도중 state 이름을 변경하는 등의 수정사항이 발생했을 때 관련된 코드를 모두 수정해야 하는 문제 발생 ! ㅜㅜ

## 그래서 Ducks Pattern!🦆

(actionTypes, actions, reducer를 한곳에서!)

리액트에서 리덕스를 사용할 때 action과 리듀서를 하나의 파일에서 사용하는 것을 말한다. 

주의할 것은 리듀서는 export default로 내보내고, 액션함수는 export로 내보낸다는 것이다. 이런파일을 리덕스 모듈이라고 부른다.

다음 4가지 규칙을 따른다!

1. 항상 reducer()란 이름의 함수를 export default 해야한다.
2. 항상 모듈의 action 생성자들을 함수형태로 export 해야한다.
3. 항상 npm-module-or-app/reducer/ACTION_TYPE 형태의 action 타입을 가져야한다.
4. 어쩌면 action 타입들을 UPPER_SNAKE_CASE로 export 할 수 있다.

Ducks 구조가 관습적인 구조와 비교하여 갖는 차이는, 구조 중심이 아닌 기능 중심으로 파일을 나눈다는 것이다.

이 구조가 갖는 장점은, 단일 기능을 작성할 때나 바뀌었을 때에 하나의 파일만 다루면 되므로 좀 더 직관적인 코드 작성이 가능하다는 것이다.

## Redux- actions

redux-actions 패키지에는 리덕스의 액션들을 관리하기 위한 유용한 createAction과 handleAction가 있다.

### createAction을 통한 액션생성 자동화

```jsx
export const increment = createAction(types.INCREMENT);
export const decrement = createAction(types.DECREMENT);
```

### switch문 대신 handleActions 사용

```jsx
const reducer = handleActions({
  INCREMENT: (state, action) => ({
    counter: state.counter + action.payload
  }),

  DECREMENT: (state, action) => ({
    counter: state.counter - action.payload
  })
}, { counter: 0 });
```

Reducer에서 액션의 type에 따라 다른 작업을 하기 위해서 switch문을 사용했다. 하지만, 이 방식에는 scope가 reducer함수로 설정되어 있다. 

그렇기 때문에 서로 다른 case에서 let이나 const를 통하여 변수를 선언하려고 하다보면 같은 이름이 중첩될시엔 에러가 발생한다.

첫번째 파라미터로는 액션에 따라 실행할 함수들을 가지고 있는 객체, 두번째 파라미터로는 상태의 기본 값(initialState)를 넣어준다.
