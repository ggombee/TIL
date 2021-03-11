## Router 적용

라우터를 통해 페이지 이동을 먼저 해보도록 한다.

원래 같으면 린트나 프리티어 설정, 리덕스 설치 등을 먼저해주고 하는게 나을텐데,,,

일단 UI를 보시기를 원하시는 것 같아서 가주아..

HashRouter, Browser Router의 차이는 아래 페이지에서 확인한다.

[https://likejirak.tistory.com/66](https://likejirak.tistory.com/66)

### 최적화 TIP

패키지를 설치할 때 yarn install --production을 입력하거나 환경변수가 NODE_ENV=production 이면 dependancy에 있는 패키지만 설치해서 빌드 결과물 크기를 최적화할 수 있다. 그래서 프로젝트에 꼭 필요한 패키지만 dependancy로 설치하고, typescript나 eslint 등 빌드 파일 실행에 필요하지 않는 패키지는 devDependancy로 설치한다.

## 본격 리덕스 설치🤣

### redux 설치

```jsx
$ yarn add react-router-dom react-redux redux
```

리덕스를 프로젝트에 추가하기 위해 npm이나 yarn 명령어를 통해 추가한다.

### redux-devtools 설치

크롬브라우저 확장프로그램설치와 연동하기 위해 툴킷을 설치한다. 스토어 값이 바뀌는 상태를 쉽게 확인 할수 있다. 

```jsx
$ yarn add redux-devtools-extension
```
