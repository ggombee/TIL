# 1. GraphQL ([사이트](https://graphql-kr.github.io/))

- JSON API
- RESTful (약속)
- PHP 기반에서 벗어나 새로운 모바일 환경에서 뉴스피드 API를 만들기 위해 만든 언어 (약속)
- 약속의 형태로 존재할 뿐만 아니라 어느정도의  의견을 포함하고 있음

## Query

쿼리는 아래와 같은 형식으로 존재할 수 있다

```jsx
type Query {
	jobPosts: [JobPost!]!
	viewer: User
}

type Jobpost {
	id: String!
	title: String!
	user: User!
}

type User {
	id: String!
	nickname: String!
	jobPosts: [JobPost!]!
}
```

→ API를 표현하기 위한 도구이자, 

→ API표현 위한 도메인 knowledge를 포함하는 스키마를 통해 내가 원하는정보를 query할 수 있음

## classroom schema

현재 classroom에서 사용되는 스키마는 아래 사이트를 통해 확인가능하다.

[https://api.alpha.classroom.im/graphql](https://api.alpha.classroom.im/graphql) 접속 하거나,

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8c853596-cc61-44ca-afc9-1565ec8d9914/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8c853596-cc61-44ca-afc9-1565ec8d9914/Untitled.png)

해당 주소를 아래 주소에 접속하여 sandbox란에 입력 하면

[https://studio.apollographql.com/sandbox/schema/sdl](https://studio.apollographql.com/sandbox/schema/sdl)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cd4b371e-c3e6-4ac1-beec-db9a2c65453c/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cd4b371e-c3e6-4ac1-beec-db9a2c65453c/Untitled.png)

아래와 같이 스키마를 확인할 수 있다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/149a243d-ef30-4d3d-b580-345d9c34e4b8/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/149a243d-ef30-4d3d-b580-345d9c34e4b8/Untitled.png)

그리고 이 스키마를 [GraphQL Voyager](https://apis.guru/graphql-voyager/)에 접속해서 붙여넣기 하면 클래스룸의 도메인 모델을 확인할 수 있다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eae52e4d-01b8-4cd5-bf88-d3bbb6182384/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eae52e4d-01b8-4cd5-bf88-d3bbb6182384/Untitled.png)
