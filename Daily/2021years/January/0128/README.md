## JS React 프로젝트 → TS로 변환하기 

때가 왔다... 바꿀시간...

타입스크립트의 이해를 위해서는 한시빨리 변환이 필요했다...

기존소스를 다른 폴더에 클론하고 변환을 시작했다.

변환은 제로초님의 블로그를 참고했다. ([https://www.zerocho.com/category/TypeScript/post/5ba90297cf54b471088ce40b](https://www.zerocho.com/category/TypeScript/post/5ba90297cf54b471088ce40b))

### 확장자명 바꾸기...

먼저 js 파일들을 ts로, jsx를 tsx로 바꾸고, 바벨을 타입스크립트로 바꾸는 과정이 필요하다..

한땀 한땀 바꿔주다보면 기계가 되어있는 나자신을 발견할 수 있다..

![Untitled](https://user-images.githubusercontent.com/58289110/106136674-f3f32700-61ac-11eb-8c5b-437071656d36.png)

열심히 바꿔주고 문득 정신을 차리면,,

![Untitled (1)](https://user-images.githubusercontent.com/58289110/106136708-01a8ac80-61ad-11eb-890b-ee7bc2efc827.png)

타입에러가 가득한 현장을 맛볼수 있다.

기타 설정들을 마저해준다...

이미 만든 프로젝트에 타입스크립트를 적용해야 한다면, 타입정의 파일을 다운받아야 한다.

```jsx
$ npm install --save-dev typescript @types/node @types/react @types/react-dom @types/jest

# or

$ yarn add typescript @types/node @types/react @types/react-dom @types/jest
```

그리고 타입스크립트 코드를 작성하기 위해 Typescript 패키지도 설치한다.

```jsx
$ npm install --save-dev typescript
```

redux의 경우엔 자체적으로 TypeScript 지원이 된다. 하지만 react-redux의 경우 그렇지 않기 때문에 패키지명 앞에 @types를 붙인 패키지를 설치해주어야 한다.

`@types`는 TypeScript 미지원 라이브러리에 TypeScript 지원을 받을 수 있게 해주는 써드파티 라이브러리이다. 

이에 관련된 소스코드는 [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped) 라는 GitHub 레포에서 관리가 되고 있다.

라이브러리에서 공식 TypeScript지원이 되는지 안되는지 확인을 하시려면 직접 설치 후 불러와서 확인을 해보셔도 되고, GitHub레포를 열어서 `index.d.ts` 라는 파일이 존재하는지 확인해도 된다.

```jsx
$ yarn add redux react-redux @types/react-redux
```

다운로드한 typescript 명령어를 이용하면 타입스크립트 설정 파일 생성이 자동으로 된다.

```jsx
$ npx typescript --init
```

리액트의 jsx코드를 사용하기 위해서는 compilerOptions의 jsx속성에 "react"값을 추가해야한다.

기본값은 주석이 되어있으니 주석을 풀어주도록 하자.

![Untitled (2)](https://user-images.githubusercontent.com/58289110/106136714-040b0680-61ad-11eb-9d09-9b2d76799060.png)

VSCode는 tsconfig.json을 보고 타입스크립트 문법을 검사할 뿐만 아니라 웹팩에서 설정한 ts-loadr가 이 파일을 참고해서 트랜스파일을 작업하기 때문에 가장먼저 생성해야 한다.

## TypeScript로 redux 활용

typescript로 react앱을 만들던 중 불편한점을 해소할 수 있는 typesafe-actions라는 패키지를 적용시켜보려 한다.

![Untitled (3)](https://user-images.githubusercontent.com/58289110/106136751-11c08c00-61ad-11eb-8fa0-268819a22e4c.png)

근데... 웨 에러나,,,,

![Untitled (4)](https://user-images.githubusercontent.com/58289110/106136781-1be28a80-61ad-11eb-83d4-b1caf28014c0.png)

으악.. 캐시지워 노드모듈 지워..

```jsx
$ npm cache clean --force
```

다시 인스탈해...다시해...😥

```jsx
$ yarn global add nodemon
```

## VSCode 절대경로 설정

### tsconfig.json or jsconfig.json

- package.json 명령어 수정할 필요 없음

```
{
  "compilerOptions": {
    "baseUrl": "src"
  },
  "include": ["src"]
}
```

## tsconfig.json 파일 설정

tsconfig 파일 속 설정들에 대해 검색을 해봤다.

일단 지속적으로 에러가나는 이부분은 ... noImplicitAny를 false로 해주면 된다..

![Untitled (5)](https://user-images.githubusercontent.com/58289110/106136825-2a30a680-61ad-11eb-9a9c-2e00d83461a5.png)

그러면 깔끔하게 사라지는걸 볼수있다.. 하지만 에러방지를 위해서 켜놓는게 좋겠지..

타입스크립트 설정을 하면서 @types 패키지들을 깔고 나면, 기존 코드에서 import 부분부터 에러가 난다. 이럴 때, esModuleInterop이라는 옵션을 켜면 한줄로 쓸수 있다.

[https://www.zerocho.com/category/TypeScript/post/5bab2086103eac558e45cdd7](https://www.zerocho.com/category/TypeScript/post/5bab2086103eac558e45cdd7)

하지만, 

```jsx
# esMouduleInterop false
import * as React from 'react';
import {PureComponent} from 'react';

# esMouduleInterop true
import React, {PureComponent} from 'react';
```

아래꺼는 require('react').default를 불러오고,

위에꺼는 require('react')의 전부 moudule.exports를 전부 끌어오는 개념이라..

default를 강제로 가져오지 않는 false일때가 정상작동이라고 한다. ~~(갓미녁님이 알려주셨다)~~

자세한 사항은... [https://www.zerocho.com/category/ECMAScript/post/579dca4054bae71500727ab9](https://www.zerocho.com/category/ECMAScript/post/579dca4054bae71500727ab9)

제로초님의 모듈강좌를 부셔보도록 하자...

그리고 에러를 잡고 yarn start를 돌린다.

그러면!!

![Untitled (6)](https://user-images.githubusercontent.com/58289110/106136830-2ac93d00-61ad-11eb-9673-c6ce28c067dc.png)

또 타입에러가 난다..

anyanyany...

WBS 작성요청이 들어와서.. 기획서보고 작성하고... 이거는 내일 마저해야겠다..히히

~~(절대 에러떄문에 도망가는거 아님...)~~
