# 3. Webpack

- 여러 파일(모듈)들을 한 파일로 뭉쳐준다.
- 파일 → Loader → Webpack → 후처리 Plugin
    - TypeScipt 적용 → ts loader 설치 - .ts로 끝나는 파일 설정해줌
    - JavaScript 관련된건 Babel Loader를 주로 쓴다!

    - Q. svg 파일을 읽고 싶다.
        - `import ... from './hello/world/something.svg'`
        - svg → 경로로 읽고싶다!

            ex) url-loader

        - svg → string으로 읽고싶다!

            ex) raw-loader

        - svg → React 컴포넌트로 읽고싶다.

            ex) @svgr/webpack

    - 결론적으로, 내가 뭔가 특이한걸 import 하고 싶다!
        - 엑셀을 읽고싶다.

            ex) xlsx-loader

    - CRA로 할때 (eject 안하고 사용하는 경우)
        - `react-app-rewired` + `customize-cra`

            ```jsx
            $ yarn add customize-cra --dev
            $ yarn add react-app-rewired --dev
            ```

            package.json에서 script를 수정하여 프로젝트 실행시 react-scripts 대신 react-app-rewired를 통해 실행

            ```jsx
            "scripts": {
                "start": "react-app-rewired start",
                "build": "react-app-rewired build",
                "test": "react-app-rewired test",
              },
            ```

            프로젝트 가장 최상단 위치에서 config-overrides.js 라는 파일을 생성한 뒤, 원하는 customizing을 하면 된다. 

            config-overrides.js 를 작성하기 전에, decorator 문법을 사용하기 위해 필요한 패키지를 설치

            ```jsx
            $ yarn add --dev @babel/plugin-proposal-decorators
            ```

            아래와 같이

            ```jsx
            const { 
                addDecoratorsLegacy, 
                disableEsLint, 
                override 
            } = require("customize-cra");
              
              module.exports = {
                webpack: override(
                    disableEsLint(),
                    addDecoratorsLegacy()
                )
              };
            ```

            customize-cra가 지원해주는 addDecoratorsLegacy 를 통해 decorator문법을 사용할 수 있게 되었다.

             mobx-react의 observer decorator를 App.js에 적용해 볼 것이다. 

            customize-cra 문서에서 disableEsLint 플러그인을 같이 사용하라고 나타나있기 때문에 설정파일에 명시하였다.

        - `craco`

## 참고

---

[Eject 없이 CRA 하기](https://medium.com/@jsh901220/create-react-app%EC%97%90%EC%84%9C-eject%EC%82%AC%EC%9A%A9%EC%95%88%ED%95%98%EA%B8%B0-customize-cra-react-app-rewired-10a83522ace0)
