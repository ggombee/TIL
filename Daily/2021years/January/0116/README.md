### create react app

![Untitled (2)](https://user-images.githubusercontent.com/58289110/110725485-0906af80-825b-11eb-886b-33a4575a9840.png)

![Untitled (3)](https://user-images.githubusercontent.com/58289110/110725491-0a37dc80-825b-11eb-8285-48bcc83afb58.png)

![Untitled (4)](https://user-images.githubusercontent.com/58289110/110725494-0b690980-825b-11eb-9d43-f84f8dd9b1da.png)

### 타입스크립트 적용(이미 존재하는 프로젝트)

처음부터 아래명령어를 실행 시키면 타입스크립트로 적용된 프로젝트를 시작할 수 있다.

```jsx
npx create-react-app my-app --template typescript

#or

yarn create react-app my-app --template typescript
```

하지만 이미 존재하는 프로젝트에 타입스크립트를 적용시키려면 아래 명령어를 실행시켜주면 된다.

```jsx
npm install --save typescript @types.npde @types/react @types/react-dom @types/jest

#or

yarn add typescript @types/node @types/react @types/react-dom @types/jest
```

![Untitled (5)](https://user-images.githubusercontent.com/58289110/110725496-0c9a3680-825b-11eb-843c-4536ca5dcfe3.png)

타입스크립트 코드를 작성하기 위해서는 typescript 패키지도 설치해야 한다.

```jsx
npm install --save-dev typescript
```

typescript 명령어를 이용하면 타입스크립트 설정 파일을 생성할 수 있다.

```jsx
npx typescript --init
```

tsconfig.json파일 자동 생성 후 compilorOptions에 jsx 속성에 'react'값을 추가해야 한다.

(기본으로 주석처리 되어 있으므로 풀고 추가한다)

```jsx
"compilorOptions": {
  "jsx": "react"
```

vscode는 이 tsconfig.json을 참고해서 타입스크립트 문법을 검사한다. 뿐만 아니라 웹팩에서 설정한 ts-loader가 이 파일을 참고해서 트랜스파일 작업을 하기 때문에 tsconfig.json 파일은 먼저 생성해야 한다.

이때 tsconfig.json파일에서 No inputs were found in config file Specified 'include' paths were '["**/*"]' and 'exclude' paths were '[]'.

비슷한 에러가 난다면 tsconfig.json과 같은 레벨에 typescript파일이 없는것이다.

ts파일 만들고 vsconde 껐다 키면 에러가 없어진다.

간단한 카운터 컴포넌트를 구현해보았다...ㅎㅎ

![Untitled (6)](https://user-images.githubusercontent.com/58289110/110725501-0dcb6380-825b-11eb-83cb-259a9c732283.png)

[https://medium.com/tapjoykorea/typescript-현업-적용-후기-caad266c8142](https://medium.com/tapjoykorea/typescript-%ED%98%84%EC%97%85-%EC%A0%81%EC%9A%A9-%ED%9B%84%EA%B8%B0-caad266c8142)

[https://musma.github.io/2019/03/05/typescript-getting-started.html](https://musma.github.io/2019/03/05/typescript-getting-started.html)
