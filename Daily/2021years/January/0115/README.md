### 타입스크립트로 리액트 상태 관리하기

→ 카운터 만들어보기 (useState)

### src/Counter.tsx

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState<number>(0);
  const onIncrease = () => setCount(count + 1);
  const onDecrease = () => setCount(count - 1);
  return (
    <div>
      <h1>{count}</h1>
      <div>
        <button onClick={onIncrease}>+1</button>
        <button onClick={onDecrease}>-1</button>
      </div>
    </div>
  );
}

export default Counter;
```

### Expected linebreaks to be 'LF' but found 'CRLF' 오류 관련

갑자기 오류가 마구 나서 검색해보니,,

```jsx
"rules": {
    "linebreak-style": 0
  },
```

이거를 .eslintrc.json파일에 추가하니까 괜찮아졌다!

근데 또 다른 이슈가...
 
### Mobx, Redux 차이점 — 꼭 정독

[https://woowabros.github.io/experience/2019/01/02/kimcj-react-mobx.html](https://woowabros.github.io/experience/2019/01/02/kimcj-react-mobx.html)
