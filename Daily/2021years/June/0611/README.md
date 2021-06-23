# 1. Babel

- Transpiler, Compiler 역할
    - 언어 ⇒  언어 변환
    - 특정 문법 등을 Javascript Code로 바꿔줌

        ex)  [Optional Chaning](https://www.notion.so/Optional-Chaining-5e25ac028c234114a6e80dfb81ab35ad) (최신문법을 과거 문법으로)

        ```jsx
        //Put in next-gen JavaScript - Optional Chaning
        const city = address?.city

        //Get browser-compatible JavaScript out
        "use strict";

        var _address;

        const city = (_address = address) === null || _address === void 0 ? void 0 : _address.city;
        ```

- Plugin
    - 각각의 문법마다 플러그인이 존재

        ex) 위 Optional Chaining 사용시 `@babel/plugin-proposal-optional-chaining` 설치

        ex) `@babel/plugin-proposal-class-properties`

- Preset
    - plugin을 모아서 제공 (왜냐면 하나하나 설정해주기 귀찮으니까)

        ex) `@babel/preset-env` : plugin 모아 특정 환경으로 타겟팅 해줌 

        ```jsx
        // target - caniuse 
        {
          "targets": {
            "chrome": "58",
            "ie": "11"
          }
        }
        ```

- JavaScript 표준 만드는 방법
    - 문법의 정의한다
    - Babel Plugin을 만든다
    - tc39 organization에 제출 (proposal)

- 어떻게 사용 ?
    - babel-plugin-lodash - 번들 사이즈 줄여주는 플러그인
    - JSX
