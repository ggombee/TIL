
## eslint 에러 잭팟

![Untitled](https://user-images.githubusercontent.com/58289110/106535994-d6bab180-653a-11eb-9ccd-ba1e34530a6b.png)

왜왜왜왜 대체 왜 에러가 나는걸까 린트.....!?
하루종일 지웠다 깔았다 삽질 엄청했다...😂

![Untitled (2)](https://user-images.githubusercontent.com/58289110/106466743-12279280-64df-11eb-95da-e1e0d48760f9.png)

구글링 해본결과 yarn에서 일어난 에러같다....

어쨋든 해결은 했지만 에러가 yarn과 npm을 섞어써서 난것인지 정확히 모르기때문에 다시한번 초기화하고 린트 적용을 해봐야겠다..


## useState 의 Coupling 방지😂

다른분이 만들어놓은 소스를 분석하고 수정해야해서 항상 사무실이 이건뭘까? 저건뭘까? 토론한다...ㅋㅋㅋ~~(좋은건가..)~~

```jsx
export function ProductsUIProvider({ productsUIEvents, children }) {
  const [queryParams, setQueryParamsBase] = useState(initialFilter);
  const setQueryParams = useCallback((nextQueryParams) => {
    setQueryParamsBase((prevQueryParams) => {
      if (isFunction(nextQueryParams)) {
        nextQueryParams = nextQueryParams(prevQueryParams);
      }
      if (isEqual(prevQueryParams, nextQueryParams)) {
        return prevQueryParams;
      }
      return nextQueryParams;
    });
  }, []);
```

오늘의 주제는 위 코드에서 useState를 사용할때 setQueryParamsBase 속에 prev~가 어디서 정의된걸까? 였다..ㅋㅋ

결론은.. useState의 커플링을 방지하기 위한 방법인것 같다.

리액트에서 기존 상태를 사용할 때는 항상 커플링에 유의해야 한다고 한다.

커플링은 한 값을 동시에 수정하려고 할 때 의도치 않은 변화가 이루어지는 걸 뜻한다고 한다.

setState가 비동기적으로 작동하므로 이런 문제가 생긴다.

예를 들어,

```jsx
const onChange = useCallback((e) => {
	const { name, value } = e.target;
	setInput({
		…input,
		[name]: value
	})
},[setInput, input])
```

이 코드에 경우 onChange가 render되는 시점보다 이전 setInput값은 씹혀버려서 ID, PW를 동시에 변경할 경우 겹쳐버리는 현상 등이 발생한다.

그래서 이를 방지하기 위해 이전값을 useState에서 받아와서

```jsx
setInput(prevInput => ({
    ...prevInput,
    [name]: value
});
```

이런식으로 코드를 작성하면 커플링을 방지 할 수 있다.

결국 저 위에 prevQueryParams는 initialFilter인 셈이다..ㅎㅎ...
