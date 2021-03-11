## Image mockData를 dispatch 해서 swiper 적용해보기

### mockdata.js

```jsx
export const imageData = [
  {
    id: 1,
    image:
      "app/resources/renewal/images/temp/main_swiper1.jpg",
  },
  {
    id: 2,
    image:
      "app/resources/renewal/images/temp/main_swiper2.jpg",
  },
  {
    id: 3,
    image:
      "app/resources/renewal/images/temp/main_swiper3.jpg",
  },
  {
    id: 4,
    image:
      "app/resources/renewal/images/temp/main_swiper4.jpg",
  },
  {
    id: 5,
    image:
      "app/resources/renewal/images/temp/main_swiper5.jpg",
  },
];
```

데이터를 받아오기 위해 스토어 세팅을 먼저 해준다. 

createStore로 store.js를 만들고 루트 리듀서를 생성한다.

### rootReducer.js

```jsx
import { combineReducers } from "redux";

import mainReducer from "./main/reducer";

const rootReducer = combineReducers({
  mainReducer,
});

export default rootReducer;
```

### configureStore.js

```jsx
import { createStore } from "redux";

import rootReducer from "./rootReducer";

const configureStore = () => createStore(rootReducer);

export default configureStore;
```

그리고 index.js에 import 해준다..

### index.js

```jsx
import React from "react";
import ReactDOM from "react-dom"; 
import App from "./app/App";

import reportWebVitals from "./reportWebVitals";
import configureStore from "./stores/configureStore";

const store = configureStore();

ReactDOM.render(<App store={store} />, document.getElementById("root"));

reportWebVitals();
```

서버 연결이 아직 되어있지 않은 프로젝트 이기 때문에, 이미지 배너 리스트를 mockdata에 명시해두고, mockdata를 dispatch함으로써 스토어의 기능을 테스트 해본다.

### MainImageBanner.js

```jsx
import React, { useCallback, useEffect } from "react";
import { useDispatch, useSelector } from "react-redux";
import { imageData } from "../../../stores/main/__mocks__/mockData";
import { getImageList } from "../../../stores/main/actions";

function MainImageBanner() {
  const { bannerList } = useSelector((state) => {
    return {
      bannerList: state.mainReducer.imageItem,
    };
  });

  const dispatch = useDispatch();

  const getImageBanner = useCallback(() => {
    dispatch(getImageList(imageData));
  }, [dispatch]);

  useEffect(() => {
    getImageBanner();
  }, [getImageBanner]);

  return (
    <>
      {bannerList &&
        bannerList.map((item) => (
          <div key={item.id}>
            <img src={item.image} width="100%" height="100" alt={item.id}></img>
          </div>
        ))}
    </>
  );
}

export default MainImageBanner;
```

이때 , 받아온 이미지의 경로를 찾지 못하여 렌더링이 안되는 오류가 생길 것이다.

이미지의 경로와 url도메인이 합쳐지면서 이미지 파일의 경로를 찾지 못하기 때문이다..(아마)

이미지의 경로는 서버에 올라가 있는 이미지 일경우 렌더링 되므로, 서버가 없는 경우 구글 이미지 검색 후, 우클릭 > 이미지 링크 복사 후 그 링크를 넣어주도록 한다.

![Untitled (2)](https://user-images.githubusercontent.com/58289110/105854846-be263500-602a-11eb-8b84-8cf158cb0efd.png)

나는  개인페이지에 올려놓은 이미지의 링크를 넣어주었다. ~~(도메인 부끄러우니까 가리기..)~~

그리고 실행을 해주면,,

![Untitled (3)](https://user-images.githubusercontent.com/58289110/105854849-bebecb80-602a-11eb-8f74-ed2c84a3ec3e.png)

쨘! 이렇게 이미지가 다섯개가 노출되는 것을 확인 할 수 있다.

이미지는 스와이퍼 테스트를 위해 임의로 제작한 이미지다....

바로 스와이퍼 라이브러리 깔아서 테스트를 해보고 싶지만 우선,, 

안오신다했던 PL님이 오시게 되서 머리빠지도록 열심히 짠 구조가 날아갈까봐 걱정했는데,, 

내가 만든 구조를 채택하여 프로젝트를 진행하기로 하여서 다행이다..

다만 프로젝트가 JS가 아닌 TS로 바뀔 것 같기에..  지금 프로젝트에 TypeScript 적용을 먼저하고, 후임이 들어오기 전에 ESLint와 Prettier 설정을 마저 해놓아야 한다... 훟....하하핳 신난ㄷㅏ...🤑
