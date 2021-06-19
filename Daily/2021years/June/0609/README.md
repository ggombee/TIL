## 3. requestAnimationFrame (60Fps를 보장하는 API)
60Frame = 1ch 60fps = 16ms

16ms이 지나면 특정이벤트를 리턴하고 새로운 이벤트를 시작한다. 

사용하는 방법은 소괄호안에 반복할 함수를 넣으면 된다.

```jsx
window.onscroll(()=>{
    requestAnimationFrame(()=>{
        console.log("hello")
    })
})
```

이것을 사용하는 이유는 무엇일까?

- 백그라운드 동작 및 비활성화시 중지(성능 최적화)
- 최대 1ms(1/1000s)로 제한되며 1초에 60번 동작
- 다수의 애니메이션에도 각각 타이머 값을 생성 및 참조하지 않고 내부의 동일한 타이머 참조

실제로 애니메이션을 구현해보면 그 차이를 알 수 있다.

```jsx
const fire2() {
	setTimeout(() => {
		console.log(fire2)
	}, 0)
}
```

위와같이 setTimeout을 0ms뒤에 실행한다는 것은 지금실행시가 아닌 다음 컨텍스트때 콜스택을 실행한다는 의미를 갖는다.
