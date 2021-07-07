# 1. [GraphQL] Apollo Client로 react 앱 개발하기

아폴로 클라이언트는 GraphQL API를 호출하기 위해 사용되는 라이브러리이다. 

GraphQL을 호출할때 꼭 아폴로 클라이언트와 같은 전용 클라이언트가 필요한 것은 아니다.

별다른 방법없이 최대한 간단하게 호출하는 방법에 대해서도 나중에 알아보도록 하자..

## 1. 패키지 설치

리액트 프로젝트에서 아폴로 클라이언트를 사용하기 위해서 다음 패키지 세개를 설치한다.

```jsx
$ npm i apollo-boost graphql react-apollo
```

`apollo-boost`  아폴로에서 제공하는 그래프큐엘 클라이언트 패키지이며, `graphql`은 Facebook에 정의한 GraphQL 스팩을 JavaScript 언어로 구현한 패키지이다. 

Apollo Server든 Apollo Client든 내부적으로는 모두 `graphql` 패키지에 의존하고 있기 때문에 반드시 함께 설치를 해줘야 한다. `react-apollo`는 React 앱에 Apollo Client를 연결(Integration)해주는 패키지입니다.

## 2. Apollo Client 생성

먼저 클라이언트 생성시 호출할 GraphQL API의 접속 정보를 설정해준다.

`apollo-boost` 패키지에서 임포트한 `ApolloClient` 생성자 함수의 인자로 `uri` 속성이 포함된 설정 객체를 넘기면 된다. 아래에서는 대륙/국가 데이터를 제공하는 공개된 GraphQL API를 사용했다.

```jsx
import ApolloClient from "apollo-boost";

const client = new ApolloClient({
	uri: "https://countries/trevorblades.com:,
});
```

## 3. React에 Apollo Client 연결

다음으로, 위에서 생성한 `ApolloClient`  객체를 React에 연결해줘야 한다. 

앱 내에서 특정 React 컴포넌트만 GraphQL API 호출이 필요한 경우가 아닌 이상, 모든 React 컴포넌트에서 `ApolloClient`를 사용하도록 설정하는 것이 일반적이다. 

예를 들어, `create-react-app`으로 생성한 React 앱이라면 `App.js` 파일에서 이 작업을 해야한다.

현재 프로젝트는 `next.js` 로 이루어져 있어 최상위가 _app.tsx이기 때문에 그곳에서 작업을 해주면 된다.

`react-apollo` 패키지에서 임포트한 `ApolloProvider` 컴포넌트로 앱의 최상위 컴포넌트를 감싸준다. 이 때, `client` prop에 위에서 생성한 `ApolloClient` 객체를 넘겨줘야 한다. 이렇게 설정을 해주면, 앱 내의 모든 컴포넌트에서 GraphQL API 연동이 가능해진다.

## 4. GraphQL API 호출

React에서 Apollo Client를 사용해서 좀 더 간편하게 GraphQL API를 호출할 수 있도록..

`react-apollo` 패키지는 `Query`와 `Mutation` 컴포넌트를 제공한다. 

본 글에서 사용하는 GraphQL API는 mutation은 제공하지 않기 때문에, query를 호출하는 예제 컴포넌트만 작성해보자.

먼저, `apollo-boost` 패키지에서 제공하는 `gql`이라는 template literal tag를 사용해서 일반 자바스크립트 문자열을 GraphQL 구문으로 바꿔준다. 

그 다음, 이 GraphQL 구문을 `react-apollo` 패키지에서 임포트 한 `Query` 컴포넌트의 `query` prop으로 넘긴다. 그리고 이 `Query` 컴포넌트는 GraphQL API 호출 상태에 따라 랜더링할 내용을 리턴하는 함수를 자식으로 가져야한다.

```jsx
import React from "react";
import { qpl } from "apollo-boost";
import { Query } from "react-apollo";

const GET_CONTINENTS = qpl`
	query {
		continents {
			code
			name
		}
	}
`;

function Continents() {
	return  (
		<>
			<h2>Continents</h2>
			<Query query={GET_CONTINENTS}>
				{({ loading, error, data }) => {
					if (loading) return <p>Loading...</p>;
					if (error){ return <p>Error!</p>;
					return (
						<ul>
							{Data.continents.map(({ code, name }) => (
								<li key={code}>{name}</li>
							))}
						</ul>
					);
				}}
			</Query>
		</>
	);
}

export default Continents;
```