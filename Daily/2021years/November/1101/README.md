# 서버 세팅 해보기

brew install yarn

```jsx
$ mkdir server

$ cd server

$ yarn init -y

```

### Apollo Server 및 GraphQL 설치

```jsx
$ yarn add apollo-server graphql
```

Apollo Server는 GraphQL이 적용된 서버를 생성할 수 있는 클래스를 제공한다. 비유하자면 `create-react-app` 패키지와 비슷한 역할이다.

### 개발도구 설치

```jsx
$ yarn add nodemon @babel/core @babel/node @babel/preset-env --dev
```

- `nodemon`
    - 실행중인 자바스크립트 파일 변경을 감지하고, 파일이 변경되면 Node를 재실행해 변경 사항이 자동으로 반영되게 도와준다..  많이 쓰는 패키지라서 `yarn global add nodemon`으로 설치하면 좋다.

- `babel`
    - 우리가 Javascript 최신 문법을 사용하면 자동으로 각 브라우저가 지원하는 Javascript 버전에 맞게 문법을 바꿔준다.

### .babelrc 파일 생성

```jsx
// .babelrc
{
  "presets": ["@babel/preset-env"]
}
```

### package.json 파일 수정

```jsx
// package.json
{
  ...
  "scripts": {
    "start": "nodemon --exec babel-node src/index.js"
  }
}
```

.babelrc 파일 생성
brew install yarn

```jsx
$ mkdir server

$ cd server

$ yarn init -y

```

### Apollo Server 및 GraphQL 설치

```jsx
$ yarn add apollo-server graphql
```

Apollo Server는 GraphQL이 적용된 서버를 생성할 수 있는 클래스를 제공한다. 비유하자면 `create-react-app` 패키지와 비슷한 역할이다.

### 개발도구 설치

```jsx
$ yarn add nodemon @babel/core @babel/node @babel/preset-env --dev
```

- `nodemon`
    - 실행중인 자바스크립트 파일 변경을 감지하고, 파일이 변경되면 Node를 재실행해 변경 사항이 자동으로 반영되게 도와준다..  많이 쓰는 패키지라서 `yarn global add nodemon`으로 설치하면 좋다.

- `babel`
    - 우리가 Javascript 최신 문법을 사용하면 자동으로 각 브라우저가 지원하는 Javascript 버전에 맞게 문법을 바꿔준다.

### .babelrc 파일 생성

```jsx
// .babelrc
{
  "presets": ["@babel/preset-env"]
}
```

### package.json 파일 수정

```jsx
// package.json
{
  ...
  "scripts": {
    "start": "nodemon --exec babel-node src/index.js"
  }
}
```

.babelrc 파일 생성
