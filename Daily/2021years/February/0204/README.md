# React TypeScript Tab 만들기

## Router로 만들기

```jsx
<Router>
      <Switch>
        <Route path='/' component={HomePage} exact />
        <Route path='/note' component={NoteListPage} exact />
        <Route path='/note/:id' component={NotePage} />
      </Switch>
    </Router>
```

[https://velog.io/@mandariin/Typescript환경에서-Route-사용하기](https://velog.io/@mandariin/Typescript%ED%99%98%EA%B2%BD%EC%97%90%EC%84%9C-Route-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)[https://wooooooak.github.io/frontend/2018/11/02/Typescript와-React에서-match-사용하기/](https://wooooooak.github.io/frontend/2018/11/02/Typescript%EC%99%80-React%EC%97%90%EC%84%9C-match-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0/)

## queryParams 이용해서 만들기

그냥 했을 때 인덱스의 값을(?1) 파싱하지 못하므로 [query-string](https://yarnpkg.com/package/query-string) 라이브러리를 설치하면 인덱스의 숫자 값을 뽑아낼 수 있다.

```jsx
$ yarn add query-string
```

캡만들기👇

```jsx
function Main(): React.ReactElement {
  const history = useHistory();
  const location = useLocation();

  const queryParams = queryString.parse(location.search);
  queryParams.index = queryParams.index || '0';

  const move = (e: any, index: number) => {
    history.push({
      pathname: '/',
      search: '?index=' + index,
    });
  };

  return (
    <>
      <MainImageBanner />
      <div>
        <ul>
          <li>
            <a onClick={e => move(e, 0)}>
              <button>구매하기</button>
            </a>
            <a onClick={e => move(e, 1)}>
              <button>판매하기</button>
            </a>
          </li>
        </ul>
      </div>
    </>
  );
}

export default Main;
```

query-string 으로 뽑아내기 (콘솔 👇)

![Untitled (7)](https://user-images.githubusercontent.com/58289110/106902578-58c5f880-673c-11eb-8a84-a3c4babfe9e8.png)
