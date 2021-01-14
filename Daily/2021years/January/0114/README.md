## TypeScript 프로젝트에 eslint/prettier 적용

 전에 프로젝트에서 과장님이 설정해주신 eslint/ prettier가 정말 편리했던 기억이나서 오늘은 이것을 세팅해보려고 한다.

> Typescript는 Javascript에 정적 타입 기능을 추가한 언어이다.

> ESLint는 JavaScript 코드를 분석해 문제점을 찾고 고쳐주는 도구이다.

> Prettier는 작성한 코드의 형식을 자동으로 맞춰주는 도구이다.

이 세 가지 퉁릉 같이 쓰먄 생산성에 큰 도움이 될 것이다. ~~(빠른작업)~~

### 확장 프로그램 설치

먼저 확장 프로그램을 설치해준다. 

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7f562c3d-301a-4b36-9f60-920611654e74/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7f562c3d-301a-4b36-9f60-920611654e74/Untitled.png)

 

아주 손쉽게 install이 가능하다.

그 후 cmd에서 설치 및 설정을 진행한다.

### ESLint 설치

```jsx
npm i -D eslint
```

우선 npm을 통해 ESLint를 설치해준다.

### .eslintrc.json 파일 설정

그 뒤 cmd에서 다음 명령을 실행한다.

```jsx
npx eslint --init
```

이때, 여러가지 사항을 물어볼텐데, 자신의 프로젝트 상황에 맞게 설정하면 된다.

```jsx
√ How would you like to use ESLint? · problems
√ What type of modules does your project use? · esm
√ Which framework does your project use? · react
√ Does your project use TypeScript? · No / Yes
√ Where does your code run? · browser
√ What format do you want your config file to be in? · JSON
The config that you've selected requires the following dependencies:

eslint-plugin-react@latest @typescript-eslint/eslint-plugin@latest @typescript-eslint/parser@latest √ Would you like to install them now with npm? · No / Yes
```

나는 위와 같이 설정하고 설치를 진행하였다.

설정이 모두 끝나면, 해당 설정에 맞는 패키지들을 자동으로 설치된다.

그리고 설치가 끝난뒤 .eslintrc.json 파일을 수정해준다.

```jsx
{
  ...
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:@typescript-eslint/recommended-requiring-type-checking"
  ],
  "parserOptions": {
    "project": "./tsconfig.json",
    "ecmaVersion": 2018,
    "sourceType": "module"
  },
  "ignorePatterns": ["dist/", "node_modules/"]
  ...
}
```

`extends`는 ESLint에 적용할 규칙들을 정의해주는 곳이다. **나중에 정의된(= 밑에 있는) 옵션일수록 높은 우선 순위를 가진다.**(설정 출처: [typescript-eslint-plugin - Recommended Configs](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/eslint-plugin#recommended-configs))

`parserOptions.project`는 타입 정보를 필요로 하는 규칙들을 사용하고 싶으면 설정해야 하는 속성이다. (출처: [@typescript-eslint/parser - ParserOptions.project](https://www.npmjs.com/package/@typescript-eslint/parser#parseroptionsproject))프로젝트의 `tsconfig.json` 파일의 위치를 적어준다.

`ignorePatterns`는 ESLint가 무시할 폴더, 파일을 적어주는 옵션이다.

이 밖에 ESLint의 자세한 설정을 알고 싶으시면 [Configuring ESLint](https://eslint.org/docs/user-guide/configuring) 를 참고하면 된다.

### Prettier 설치

npm통해 패키지를 설치해준다.

```jsx
npm i -D prettier
```

그리고 충돌방지를 위해 플러그인을 설치해준다.

```jsx
npm i -D eslint-config-prettier eslint-plugin-prettier
```

eslint-config-prettier는 Prettier와 충돌되는 ESLint 규칙들을 무시하는 설정이고, eslint-plugin-prettier는 Prettier를 사용해 포맷팅을 하도록 ESLint 규칙을 추가하는 플러그인이다.

### .eslint.json과 .prettierrc.json 파일 설정

프로젝트 폴더에 .prettierrc.json 파일을 생성해준다. 다른 툴들과 달리 직접 파일을 생성해줘야 된다. 

아래 페이지를 참고해서 다양한 옵션을 원하는 스타일로 설정하면 된다.

[Options · Prettier](https://prettier.io/docs/en/options.html)

```jsx
{
    "printWidth": 80,			// 한 줄의 라인 수
    "tabWidth": 2,			// tab의 너비
    "useTabs": false,			// tab 사용 여부
    "semi": true,				// ; 사용 여부
    "singleQuote": true,			// 'string' 사용 여부
    "quoteProps": "consistent",		// 객체 property의 따옴표 여부
    "trailingComma": "es5",		// 끝에 , 사용 여부
    "bracketSpacing": true,		// Object literal에 띄어쓰기 사용 여부 (ex: { foo: bar })
    "arrowParens": "always",		// 함수에서 인자에 괄호 사용 여부 (ex: (x) => y)
    "endOfLine": "lf"			// 라인 엔딩 지정
  }
```

```jsx
{
    "printWidth": 80,
    "tabWidth": 2,
    "useTabs": false,
    "semi": true,
    "singleQuote": true,
    "trailingComma": "all",
    "arrowParens": "avoid"
}
```

이런식으로 각자의 맞게 설정해준다.

### VSCode Format On Save 설정

자신이 작성한 코드가 자동으로 수정되게 설정하기 위해 Preferences > Settings > Workspace > Editor: Format On Save 옵션에 체크를 해준다.

파일을 저장할때마다 포맷팅이 된다.
