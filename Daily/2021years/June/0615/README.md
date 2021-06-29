# 🧐 Yarn 부터..

일반적으로는 Node.js와 Npm을 사용하는데 Npm이 문제가 많았다.

여러 보안 이슈와 속도가 느린 점 등 여러가지 문제점으로 인해 Yarn이 나오게 되었다.

Yarn 또한 node_modules라는 파일을 지니고 있었고 Node.js의 패키지 관련된 여러가지 이슈, 문제점을 지니고 있었다... 

## Node.js 패키지 관련 이슈

- 보안성 관련 문제
- dependencies
- devDependencies
- peerDependencies
    - 모호한 개념.. 애매함..

### PeerDependencies

내가 만든 패키지가 다른 패키지에 직접 require되는 것은 아니지만 그 호스트 패키지와 호환성을 가지고 있는 것을 표현하고 싶을 때 플러그인을 사용한다. 특히 각 모듈은 호스트의 패키지 문서에 의해 지저오디거나 예측되는 특정한 인터페이스를 가지고 있을지도 모른다.

일반적으로 dependency는 내가 만든 모듈에서 사용하는 패키지들을 지정하는 반면, peerDependencies는 반대로 내가 만든 모듈이 다른 모듈과 함께 동작할 수 있다는 호환성을 표시하는 것이다. 마치 gulp가 있다면 내가 만든 모듈은 gulp의 플러그인 중 하나인 것이다. 이때 내가 만든 모듈이 gulp의 모든 버전이 아니라 1.3버전과만 동작한다면 그런 정보를 표시해야하는데 이때 사용하는 것이 peerDependencies 이다.

```jsx
"name" : "a",
"version" : "1.3.5",
"peerDependencies" : {
	"b" :"v1.0.0"
}
```

  

**문제 1) storybook → B → commander → Phantom dependencies**     

Npm , Yarn1 에서는 의존성들이 트리형태로 분포해 있는 것을 **호이스팅** 방법을 통해서 위로 끌어올린다. 

아래와 같이 의존성이 존재한다고 할때,

- A/package.json

    ```jsx
    {
    	"dependencies" : {
    		"B" : "^0.0.1"
    	}
    }
    ```

- B/package.json

 `yarn add A` 시 A, B, C가 설치된다.

A라는 라이브러리에서, C를 참조할수 있다.

- `import { something } from 'C'`

이게 되는게.... 문제다...!

이 방법을 사용하면 **유령 의존성(Phantom dependencies)** 현상이 발생하게 된다. 어떠한 의존성이 호이스팅을 통해서 최상단으로 선언되었다면, 실제로는 package.json에 선언되지 않은 패키지임에 불구하고, 사용할 수 있는 것이다.

실제로 이렇게 사용하는 것은 개발 협업간 큰 혼란을 야기할 수 있다.

~~Node.js Package Resolving Algorith... 문제이다...!!! (기술부채...)~~

**문제 2) require()**

require를 사용해서 동적으로 변수를 받을 수 있다. 

```jsx
let pkg = 'express'

if (...) {
	pkg = 'lodash'
}

const m = require(a)

//m??
```

이게 되는게... 또 문제다..

문제 3 ) node_modules가 너무... 거..지..

![01](https://user-images.githubusercontent.com/58289110/124865785-4b1be400-dff6-11eb-9a4d-3ab6d9fb3d61.png)

위 밈 사진에서도 볼 수 있듯이 node_modules의 거대한 양 때문에 여러가지 이슈가 생기기도 하는데, 파일 수가 많고 무거운게 또또 문제다...

# 🤭 Yarn 2 등장!

TMI : 왜 'Berry'?
→ yarn2의 프로젝트 명이 berry이다. (실 레포지토리명)

## Plug'n'Play

현재 react 또는 vue 프로젝트에서 가장 많은 부분을 차지하는 것이 node_modules라는 파일이다.

이 부분에서 야기되는 문제가 많기에 yarn2에서는 이 문제를 해결하고자 하였다.

### 그래서!!

`node_modules` 을 없애버렸다! 
Node.js의 모듈 Resolving 방식을 전부 Polyfill하고 커스텀 로직으로 바꾸었다.
(ex.. require, require.resolve...)
이 방식을 사용하면 어떠한 패키지를 설치하게 되면 더 이상 `node_modules`에 저장되지 않는다.

그리고 새롭게 패키지 관리 시스템을 만들었다.

CLI에서 `yarn add ...` 을 하면 된다.

PHP Composer에서 영감을 받아 제작하였지만, 사용자들의 사용성이 높지 않았다.

하위호환성이 안되었기 때문이다... 그래서 많은 사용자들의 불만을 얻었지만 아랑곳하지 않고 리브랜딩을 진행하였다.

- 빼애애애애액!! 소프트웨어에서 하위호환성이 얼마나 중요한데! Yarn 1 이제 신경 안쓸꺼냐!! 기존 프로젝트들도 쉽게 Yarn 2로 마이그레이션 할 수 있도록 기존 방식의 옵션을 제공해달라!!
- Yarn 팀: 안돼. 안 바꿔줘. 바꿀 생각 없어. 빨리 돌아가. (그럴꺼면 `npm` 써라)

![unnamed](https://user-images.githubusercontent.com/58289110/124865848-64bd2b80-dff6-11eb-84c0-696fb7db2d3e.jpg)

그리고 실제 반응

- 패키지 메인테이너: 헐 Yarn 2에서 우리 패키지 안 돌아가네;;; (이슈 생성) peerDependencies 빼고, 빠진 Dependency 넣고! 이상한 require 문 다 없애자!!

# Yarn 2 사용하기

- Fun facts: 원래 Yarn은 각 프로젝트별로 어떤 `yarn` 을 쓸지 내재화 할 수 있음.

    ```jsx
    $ yarn set version berry
    $ yarn set version latest
    ```

## 패키지 설치하기

### 한번 패키지를 설치해볼까?

```bash
$ yarn add express
```

패키지를 설치하면, `.yarn/cache` 에 해당 패키지의 `.zip` 파일이 복사되고, Yarn 2 내부 Webpack 비스무리한 무언가가 동작해서 `.pnp.js` 파일에 해당 패키지가 설치 된다. (Webpack이 맞는지는 모르겠음)

만약 `postinstall` 을 가진 패키지가 있다면, `.yarn/unplugged` 폴더에 기존 `node_modules`와 같은 방식으로 설치된다.

Yarn 2에서 제대로 작동하지 않는 패키지가 있다면? → `yarn unplug {패키지_이름}` 을 해보자. 이렇게 해도 안되면? → 100% 패키지 문제!!!! → 클린한 Node.js 생태계를 위해 해당 패키지 레포에 가서 이슈를 남기자.

그게 귀찮다면, `.yarnrc.yml`의 `packageExtensions` 옵션을 활용하자

### 패키지 사용하기

대신 `.yarn.cache` 폴더에 해당 의존성의 정보가 저장되고, 아래와 같이 `.pnp.js`파일에 의존성을 찾을 수 있는 정보가 기록된다.

```jsx
["styled-components", [
  ["npm:5.3.0", {
    "packageLocation": "./.yarn/cache/styled-components-npm-5.3.0-965f77d02b-1f94f92b5d.zip/node_modules/styled-components/",
    "packageDependencies": [
      ["styled-components", "npm:5.3.0"]
    ],
    "linkType": "SOFT",
  }]
]]
```

또한, 각 의존성을 ZIP 아카이브로 관리하게 되어, 실제 `.yarn/cache` 폴더에 들어가보면, 다음과 같이 압축파일들이 존재하는 것을 확인할 수 있다.

이로서, `.pnp.js` 명시된 정보에 다라서 각 패키지들은 동적으로 참조되게 된다. 해당 방식을 택함으로서 기존의 방식보다 용량이 획기적으로 줄었고 기존의 트리형태의 `node_modules`폴더를 순회할 필요가 없어졌기 때문에, 검색 속도도 증가하게 되었다.

띠용? node_modules가 없으면 require는 어떻게 동작하는거야??

→ 이를 위해서 node를 실행시킬때 yarn 2를 통해서 실행시켜야함. JS가 읽히기전 Yarn 2가 `require` 함수를 override 한다고 생각하면 된다. (런타임 성능적으로 File System 접근이 줄어들어서 좋아진다는데, 솔직히 공감안됨)

```bash
$ yarn node ./index.js
```

음 yarn 명령어를 못쓸때는 어떻게?? (예: pm2의 `ecosystem.config.js`)

→ 엔트리 파일 첫번째에서 `.pnp.js` 파일의 `setup` 함수를 실행하면 됨!

```jsx
require('./.pnp.js').setup()
```

### 마이그레이션 하고 싶어요!

- 삽질 각오하시고 시작하시길
- **NPM 생태계가 그동안 얼마나 드러웠는지 알게됩니다 ㅋㅋ**

# Yarn 2 프로젝트 관리하기

## 충격과 공포의 cache commit

- `.yarn/cache` 폴더를 커밋한다.
    - 패키지를 다운로드하지 않으므로 yarn install 속도가 엄청 빨라진다.
    - `GITHUB_TOKEN`, `FONTAWESOME_TOKEN` 설정은 이제 안녕
        - 처음 설치할때만 `.yarnrc.yml` 에 설정하면 됨
            - 요렇게

                ```yaml
                yarnPath: ...

                npmScopes:
                  daangn:
                    npmRegistryServer: https://npm.pkg.github.com/
                    npmAlwaysAuth: true
                    npmAuthToken: ${GITHUB_TOKEN}
                ```

- `.pnp.js` 를 커밋한다
    - PnP 파일은 어차피 JavaScript라서 OS에 독립적이다. postinstall 필요한 패키지는 자동으로 unplugged 에 들어가니까 PnP 파일을 커밋해도 상관없다.
- 그래서 `.gitignore` 는 이렇게

    ```bash
    ›ﬁ/.yarn/unplugged
    /.yarn/build-state.yml
    /.yarn/install-state.gz
    ```

- CI에서 5초로 단축된 yarn install를 즐긴다

해당 `.yarn` 폴더 자체를 깃에 올릴때도 **Zero-install** 방식을 사용하게 되면, 더 이상 clone을 실행한 뒤 추가 설치가 필요없이 바로 실행이 가능하다. 

기존 CI속도가 빨라지며 더 이상 호이스팅을 하지않음으로써 유령 의존성 문제도 근본적으로 해결된 셈이다.

## 오픈소스라면 조심하기

- `.yarn/cache` 에 커밋이 있는 PR이 들어오면 Cache를 확인하는 스크립트를 싹 돌린다. (악성코드를 삽입할 수 있으므로)

## 삽질

- VS Code에서 TypeScript, Prettier, ESLint 등등... PnP 기반 개발도구 사용하기

    ```bash
    $ yarn dlx @yarnpkg/pnpify --sdk vscode # 를 실행하면 자동으로 매핑해줌~~
    ```

- Node.js 기반 CLI 패키지를 GitHub Package Registry에 올리면 작동안함. ⇒ GitHub Package Registry 문제, `yarn.lock` 에서 다른 CLI 패키지 참고해서 손으로 한땀한땀 넣어준다.
    - 그래도 한번 넣어주면 잘 작동한다.

---

### 참고

[package.json](https://programmingsummaries.tistory.com/385)

[https://velog.io/@altmshfkgudtjr/yarn2와-함께-Plug-n-Play를-적용해보자](https://velog.io/@altmshfkgudtjr/yarn2%EC%99%80-%ED%95%A8%EA%BB%98-Plug-n-Play%EB%A5%BC-%EC%A0%81%EC%9A%A9%ED%95%B4%EB%B3%B4%EC%9E%90)

[https://seungho.dev/yarn-2-announced/](https://seungho.dev/yarn-2-announced/)
