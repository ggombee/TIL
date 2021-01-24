# Flux

Dispatcher에서 Store → View → Action → Dispatcher

## Dispatcher

Dispatcher는 Flux의 모든 데이터 흐름을 관리하는 허브 역할을 하는 부분이다. Action이 발생되면 Dispatcher로 전달되는데, Dispatcher는 전달된 Action을 보고, 등록된 콜백 함수를 실행하여 Store에 데이터를 전달한다. Dispatcher는 전체 어플리케이션에서 한 개의 인스턴스만 사용된다.

## Store

어플리케이션의 모든 상태 변경은 Store에 의해 결정이 된다. Dispatcher로 부터 메시지를 수신 받기 위해서는 Dispatcher에 콜백 함수를 등록해야 한다. Store가 변경되면 View에 변경되었다는 사실을 알려주게 된다. Store은 [싱글톤](https://ko.wikipedia.org/wiki/%EC%8B%B1%EA%B8%80%ED%84%B4_%ED%8C%A8%ED%84%B4)으로 관리된다.

## View

Flux의 View는 화면에 나타내는 것 뿐만이나라, 자식 View로 데이터를 흘려 보내는 뷰 컨트롤러의 역할도 함께 한다.

## Action

Dispatcher에서 콜백 함수가 실행 되면 Store가 업데이트 되게 되는데, 이 콜백 함수를 실행 할 떼 데이터가 담겨 있는 객체가 인수로 전달 되어야 한다. 이 전달 되는 객체를 Action이라고 하는데, Action은 대채로 액션 생성자(Action creator)에서 만들어진다.

## Presentational 컴포넌트와 Container 컴포넌트

프리젠테이셔널 컴포넌트와 컨테이너 컴포넌트는, 리덕스를 사용하는 프로젝트에서 자주 사용되는 구조이다. Dumb 컴포넌트와 Smart 컴포넌트로도 알려져있다.

### 프리젠테이셔널 컴포넌트

프리젠테이셔널 컴포넌트는 오직 뷰만을 담당한다. 이 안에는 DOM 엘리먼트, 그리고 스타일을 갖고 있으며, 프리젠테이셔널 컴포넌트나 컨테이너 컴포넌트를 가지고 있을 수도 있다. 

하지만, 리덕스의 스토어에는 직접적인 접근 권한이 없으며 오직 props 로만 데이터를 가져올수 있다. 또한, 대부분의 경우 state 를 갖고있지 않으며, 갖고있을 경우엔 데이터에 관련된것이 아니라 UI 에 관련된것이어야 한다.

주로 함수형 컴포넌트로 작성되며, state 를 갖고있어야하거나, 최적화를 위해 LifeCycle 이 필요해질때 클래스형 컴포넌트로 작성된다.

### 컨테이너 컴포넌트

이 컴포넌트는 프리젠테이셔널 컴포넌트들과 컨테이너 컴포넌트들을 관리하는것을 담당한다. 주로 내부에 DOM 엘리먼트가 직접적으로 사용되는 경우는 없다. 사용되는 경우는 감싸는 용도일때만 사용 된다. 또한, 스타일을 가지고있지 않아야한다. 스타일들은 모두 프리젠테이셔널 컴포넌트에서 정의되어야 한다. 상태를 가지고 있을 때가 많으며, 리덕스에 직접적으로 접근 할 수 있다.

### 고찰

UI 쪽과 Data 쪽이 분리되어 프로젝트를 이해하기가 쉬워지며, 컴포넌트의 재사용률도 높여준다는 장점이 존재한다.

아래와 같은 것을 컨테이너로 제작한다.

- 페이지
- 리스트
- 헤더
- 사이드바
- 내부의 컴포넌트 때문에 props가 여러 컴포넌트를 거쳐야 하는 경우

컨테이너 컴포넌트라고해서 무조건 그 내부에 여러개의 컴포넌트가 있어야하는것이 아니다. 예를들어 Item 이란 프리젠테이셔널 컴포넌트가 있다면, ItemContainer 라는 컴포넌트를 만들어서 그 안에 Item 컴포넌트 하나만 넣고 데이터를 연결해주는 것도 가능하다.

추가적으로, 어떤걸 컨테이너로 만들지, 그리고 이 구조를 사용할지는 여러분의 자유다. 이 구조는 리덕스의 창시자 Dan Abramov가 공유한 구조이긴 하나, 무조건 따라야 할 규칙이 아니다. 따라하면 유용한 팁일수도 있고, 어쩌면 여러분들의 개발 흐름에 어울리지 않을 수도 있다. 무조건 프리젠테이셔널 컴포넌트로 분리하지 않고 그냥 DOM 엘리먼트를 지닌 컴포넌트에 직접 리덕스를 연결해도 상관없다. 그러다 나중에 컴포넌트를 재사용을 해야될 때쯤 다시 분리시켜도 된다.

## 그렇다면 나는?

흠 몰라....대충살자. 이거때문에 하루버린게 레전드

![Untitled](https://user-images.githubusercontent.com/58289110/105352812-bf71ef00-5c31-11eb-9f5a-c7bd98347cc5.png)

## 3. 폴더 구조

*> src*

*> <br>*

*>*

*> > app*

*> > <br>*

*> >*

*> > > components (Presentation Components)*

*> > > <br>*

*> > > containers (Container Components)*

*> > > <br>*

*> > > pages *

*> > > <br>*

*> > stores (actions)*

*> > <br>*

*> > styles (CSSmodules (\*.module.scss))*

*> > <br>*

*> > utils (utilities)*

### containers

- 컨테이너 컴포넌트

### components

- 프리젠테이션 컴포넌트

### pages

- routes > container

### stores

*> Component (폴더명)*

*>*

*> > action.ts : 액션 관리*

*> > <br>*

*> > constant.ts : 액션 타입 관리*

*> > <br>* 

*> > reducer.ts : 액션 타입 관리*

### styles

- Scss : \*.scss 를 \*.module.scss (CSS Module) 으로 변경하여 사용
- image : nas에 올려사용(tsx에서 직접 import 하는 이미지 제외한 모든 이미지(아이콘 등등)로컬 이미지 사용하지 않음)

### utils

- 공통 유틸리티

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
 
