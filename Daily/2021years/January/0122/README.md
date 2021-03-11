## 스타일 라이브러리 설치

CSS Module 을 사용 할 때에는 `styles.icon` 이런 식으로 객체안에 있는 값을 조회해야 하는데, 만약 클래스 이름에 `-` 가 들어가 있다면 다음과 같이 사용해야한다: `styles['my-class']`

그리고, 만약에 여러개가 있다면 다음과 같이 작성해한다: `${styles.one} ${styles.two}`

조건부 스타일링을 해야 한다면 더더욱 번거롭...다.. `${styles.one} ${condition ? styles.two : ''}`

우리가 이전 섹션에서 Sass 를 배울 때 썼었던 [classnames](https://github.com/JedWatson/classnames) 라이브러리에는 [bind](https://github.com/JedWatson/classnames#alternate-bind-version-for-css-modules) 기능이 있는데, 이 기능을 사용하면 CSS Module 을 조금 더 편하게 사용 할 수 있다.

```jsx
$ yarn add classnames
```

sass파일을 이용하려면 nods-sass를 설치한다.

```jsx
$ yarn add node-sass
```

## 헤더 만들기

![Untitled (1)](https://user-images.githubusercontent.com/58289110/105502954-5bbaf500-5d09-11eb-9124-d180c96495ad.png)


### axios-mock-adapter

고의로 에러를 발생시켜 그에 따른 에러를 핸들링할 수 있는 라이브러리
 
 
