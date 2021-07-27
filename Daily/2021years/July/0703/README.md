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
