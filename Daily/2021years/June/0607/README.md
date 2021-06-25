# Event Loop

## 단일 스레드

자바스크립트는 단일 스레드 기반의 언어로 한순간 하나의 작업만을 처리할 수 있다. 

이는 동시에 아무것도 하지 못한다는 의미이며 콜스택이 하나라는 의미이기도 하다.

여기서 콜스택이란 무엇일까?

또한 비동기로 동작하기 때문에 단일 스레드에도 불구하고 많은 작업을 수행한다.

### 콜스택

콜스택은 data stucture로써 쉽게 말하면 코드가 실행되는 순서를 기억하는 부분이라고 생각하면 편하다.

![eeb](https://user-images.githubusercontent.com/58289110/123382070-77823a00-d5cc-11eb-9425-793187f340f9.png)

비동기로 작동하는 자바스크립트의 특성상 콜스택에 쌓인 작업은 하나씩 실행되는 순서를 기억해 놓았다가 하나씩 실행한다.

### 비동기

아래 예제를 한번 보면 이해를 하기 쉬울 것이다.

```jsx
function a(){
    console.log("astart")
    b()
    console.log("aend")
}

function b(){
    console.log("bstart")
    c()
    console.log("bend")
}

function c(){
    console.log("cend")
}

a()
```

이렇게 된 코드를 실행한다 했을때 아래와 같은 순서를 콜스택이 기억했다가 코드가 실행된다

> a
a - b
a - b - c
a - b
a

콘솔을 찍어보면

<img width="200" alt="_2021-06-23__11 16 02" src="https://user-images.githubusercontent.com/58289110/123382098-82d56580-d5cc-11eb-9aa4-1fdd8946f475.png">

이렇게 나오는 것을 확인할 수 있다.

이처럼 콜스택은 비동기 작업에 영향을 미치고 콜스택이 빈상태를 idle이라고 한다.

위와같은 순서로 작업되는 자바스크립트의 특성이 이벤트 큐 도입의 원인이 되었다.

## Event

```jsx
let queue = []

setInterval(()=>{
    console.log(queue)
}, 1000)

function enqueue (){
    queue.push(
        {Jobname:"hello"}
    )
}

enqueue()
```

위 코드를 실행하면 1초에 한번씩 콘솔이 찍히는것을 확인할 수 있다.

<img width="196" alt="_2021-06-24__11 52 56" src="https://user-images.githubusercontent.com/58289110/123382125-8a950a00-d5cc-11eb-9d9d-74df27818398.png">

그런데 아래와 같이 조건을 걸어준다면 ,

```jsx
let queue = []

setInterval(()=>{
    if(queue.length > 0) {
        console.log(queue[0].Jobname)
        queue.splice(0,1)
    }
}, 1000)

function enqueue (){
    queue.push(
        {Jobname:"hello"}
    )
}

enqueue()
```

<img width="205" alt="_2021-06-24__12 32 35" src="https://user-images.githubusercontent.com/58289110/123382160-9254ae80-d5cc-11eb-9534-b1ae883a15c1.png">

이렇게 한번만 실행되는것을 확인할 수 있다.

우리는 이런  방식을 활용해서 프론트에서의 최적화를 진행할수있다.

```jsx
window.onscroll(()=>{
a()
},1000)

function a() {
console.log('dddd')
}
```

위와같은 함수가 있다고 해보자.

함수의 실행시간이 짧을때는 문제가 없을수도 있겠지만 긴작업이 들어있으면 아래와 같이 이벤트큐가 계속 밀릴것이다.

> onscroll—onscroll—onscroll—
a——a
        a——a
                a——a
                        a——a

하지만 최적화를 통해 큐가 밀리는 시간을 조금 단축할 수 있다.
