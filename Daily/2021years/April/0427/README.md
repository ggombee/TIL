# arrow function

기술면접을 보게 되면서 arrow function 과 기존의 function 의 차이점에 대한 질문을 받았는데 헷갈려서 대답을 잘 하지 못하였다.

이에대해 정리를 해보고자 한다.

### 1. 문법이 간단하다.

```
function add(a, b) {
 return a+b;
}

const add = (a, b) => a+b;
```

arrow function은 경우에 따라 { }를 생략하거나 return을 생략 하는것도 가능하다.

### 2. 'this' 바인딩 대상이 다르다.

```jsx
this.someFunction.bind(this)
```

this에 속한 메서드를 다시 this에 바인드 하는 경우가 있다.

리액트에서 이러한 코드가 빈번히 작성되는 이유를 알기 위해서는 bind()함수가 무슨 역할을 하는지 먼저 알아봐야 될 것이다.

자바스크립트는 함수 호출 시 this가 바인딩 할 객체가 동적으로 결정된다. this의 대상을 지정해주는 역할을 하는것이다.

함수 선언 시 this에 바인딩 할 객체가 정적으로 결정되는 것이 아니라, 함수를 호출 할 때함수가 어떻게 호출 되었는지에 따라서 this가 바인딩 할 객체를 동적으로 결정하게 된다.

따라서 일반 function은 메소드 내에 함수를 만드는게 어렵다.

```jsx
const objA = {
  name: 'a',
  aFunc: function() {
    console.log(this.name)
  },
}

const objB = {
  name: 'b',
}

objA.aFunc() // (1)
// a
objA.aFunc.bind(objB) // (2)
const foo = objA.aFunc.bind(objB) // (3)
foo()
4
// b
```

**`objA`**와 **`objB`**라는 객체가 있다. objA 객체는 **`name`**이라는 값과 **`aFunc`**라는 함수를 속성으로 가지고 있다. 반면 objB 객체는 **`name`**이라는 값만 가지고 있다.

(1) objA 의 aFunc 함수를 실행하면 예상대로 **`a`**가 출력된다.

(2) objA 객체의 aFunc 함수에서 bind(objB)를 호출한다. 함수가 호출되었지만, 아무것도 출력되지 않는다.

 다만, 원본 aFunc 함수와 동일한 기능을 하는 바인딩된 새로운 함수가 만들어진다. 이때, bind 메서드에 전해진 인자는 복사된 바인딩 함수의 this 로 전달된다. 즉, aFunc 함수내의 **`this`**가 **`objB`**가 되는 것이죠. 이게 **`bind()함수`**가 하는 일의 전부이다.

(3) 바인드 함수를 변수에 할당한다.

(4) 실행하면 **`b`**가 출력된다.

arrow function을 사용하면 arrow function안의 this는 **상위 scope의 this**를 가리킨다. 

일반 function과는 달리 선언시에 this가 바인딩 할 객체가 **정적으로 결정**되며,prototype이 없다.

상위 scope의 this를 가리키는 것을 "**Lexical this**"라고 한다.

### React에서의  bind()

```jsx
import React from 'react'

class BindTest extends React.Component {
  handleClick() {
    console.log(this)
  }
  render() {
    return (
      <button type="button" onClick={this.handleClick.bind(this)}>
        Goodbye bind
      </button>
    )
  }
}
export default BindTest
```

버튼 태그의 onClick 속성을 보면 bind() 함수가 사용되고 있는걸 알수 있다. 이상한 점은 this 의 handleClick 함수에다가 this 객체를 바인드시켰다는 것이다. 같은 this 인데 굳이 또 바인드해주는 이유가 뭘까? bind 함수를 빼보겠다.

```jsx
import React from 'react'

class WithoutBindTest extends React.Component {
  handleClick() {
    console.log(this)
  }
  render() {
    return (
      <button type="button" onClick={this.handleClick}>
        Goodbye bind without this
      </button>
    )
  }
}
export default WithoutBindTest
```

**`null`**이 출력되었습니다. 왜 null 이 출력되었을까?

이 내용을 이해하려면 자바스크립트에서의 **`this`**에 대해 어느정도 알고 있어야 한다.

### this

객체지향 언어에서의 일반적인 this 의 의미(현재 객체를 지칭)와는 달리 자바스크립트의 this 는 실행시의 context 를 말한다. 

아래 예제를 보면,

```jsx
const thisTest = function() {
  console.log(this.value)
}
thisTest.value = 'I am this'
thisTest()
```

**`"I am this"`**가 나올거라는 예상과는 달리 **`undefined`**가 출력된다. 왜냐하면 **`thisTest()`**가 출력될 때의 context 가 전역객체이기 때문이다. 

thisTest.value 는 thisTest 에 속성인데 전역객체에서 value 를 찾으려고 하니 undefined 가 나올수 밖에 없다(window 객체가 아니라 undefined 인 이유는 React 가 기본적으로 strict 모드에서 실행되기 때문이다).

"I am this"를 출력하려면, this 에 해당하는 객체의 메서드를 호출하면 this.value 값을 가져올 수 있다. 아래 예제를 보면,

```jsx
const thisTest = function() {
  console.log(this.value)
}
thisTest.value = 'I am this'
thisTest.func = function() {
  console.log(this.value)
}
thisTest.func()
```

**`thisTest.func`** 함수를 만들어서 그안에서 **`this.value`**를 출력한다. thisTest 객체의 func() 메서드를 호출하면 이 때는 **`this`**가 thisTest 가 되기 때문에 정상적으로 this.value 를 가져와 "I am this"를 출력한다.

이제, 리액트로 다시 돌아가자.

### Arrow Function

click, change 등의 이벤트 리스너를 붙여줄때마다 bind()함수를 작성하는건 귀찮은 일이다. ES6 의 화살표함수를 사용하면 이 문제를 간단히 해결할 수 있다. BindTest 를 화살표 함수를 이용해 새로 작성해보았다.

```jsx
import React from 'react'

class BindTest extends React.Component {
  handleClick = () => {
    console.log(this)
  }
  render() {
    return (
      <button type="button" onClick={this.handleClick}>
        Goodbye bind
      </button>
    )
  }
}
export default BindTest
```

이제는 this 가 무엇인지 걱정할 필요가 없다. 화살표 함수의 this 는 외부함수(부모함수)의 this 를 상속받기 때문에 this 는 항상 일정하다. 위 예제의 경우에는 BindTest 클래스가 되겠다.

### 결론 (React)

bind()함수는 전달된 인자를 this 로 보내는 바인딩 함수를 만든다. this 는 다른 언어와 달리 실행 문맥(context)에 따라 변한다. React 에서 이벤트 핸들러 함수를 바인드할때 화살표 함수를 사용한다.

function과 arrow function은 Javascript의 관점에서 보면 훨씬 더 많은 차이점이 있지만,리액트를 다룰 때 고려할 점의 가장 큰 부분은 **this가 결정되는 방법**이다.리액트에서 컴포넌트를 만드는 방식은 **class**형과 **function**형 으로 나뉘어 진다.이때 클래스형은 객체를 다루는 형태가 많으므로, this를 자주 사용 하게 된다.

함수형 컴포넌트를 사용해 컴포넌트를 만드는 경우에도 this를 사용 할 수도 있지만,일반 function과 arrow function을 언제 사용해야 하는지는**this를 어떻게 사용하고 싶은지** 먼저 생각 해 보고 적절하게 판단해야 하는 것을 알 수 있다.
