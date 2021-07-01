## Node.js (Batching 작업) or React

### setState 예제

```jsx
let nowState = {};
let started = false;
let called = false;

function setState(state){
    started=false;
    nowState = state;
    if(called){
        console.log(state);
        setTimeout(()=>{
            called = false;
            if(started){
                started = false;
                console.log(nowState);
            }
        },1000);
    }
    called = true;
};

setState({a:1});
setState({a:2});
setState({a:3});
setState({a:4});
setState({a:5});
setState({a:6});
setState({a:7});
```

위와같이 코드를 작성하고 함수 실행을 하면 순서대로 콘솔이 찍히는것을 확인할 수 있다.

### setState (실행중 배치)

이를 실행중 async와 await를 이용해서 실행중 배치작업으로 만들 수 있다.

```jsx
let nowState = {};
let started = false;
let called = false;

function setState(state){
    started=false;
    nowState = state;
    if(called){
        console.log(state);
        process.nextTick(()=>{
			called = false
			if(started){
				started = false
				console.log(nowState)
			}
		}, new TypeError(''))
    }
    called = true;
};

(async()=>{
    setState({a:1});
	setState({a:2});
	setState({a:3});
	setState({a:4});
	await setState({a:5});
	setState({a:6});
	await setState({a:7});
})();
```

### DataLoader 를 사용한 Batch

```jsx
const DataLoader = require('dataloader');
const something = new DataLoader(async (ids) => {
	console.log(ids)
	return ids
});
(async()=>{
	something.load(1);
	something.load(2);
	await something.load(3);
	something.load(5);
})();
```

---

[자바스크립트 비동기 핵심 이벤트 루프](https://medium.com/sjk5766/javascript-%EB%B9%84%EB%8F%99%EA%B8%B0-%ED%95%B5%EC%8B%AC-event-loop-%EC%A0%95%EB%A6%AC-422eb29231a8)

[스크롤 이벤트 최적화](https://developer.mozilla.org/ko/docs/Web/API/Intersection_Observer_API)
