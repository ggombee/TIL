## 리액트 기본개념

액션생성자 - 상태를 바꿀때 항상 액션필요

스토어 - 모든 상태변화는 스토어에 의해 이루어짐

리듀서 - 상태 객체 직접변경하지 않고 복사후 새로운 상태 객체 하나로 합쳐짐

컨트롤러뷰/일반뷰 -

디스패처- 콜백이 등록되어 잇는곳

useCallback-이중으로 도는거 피하려면 쓰면안됨

index.ts 메인 컴포넌트

action.ts 액션타입 정의

types.ts 데이터 타입 정의

constants.ts 리듀서 필요한 액션타입 정의

reducer.ts 액션일어났을때 함수 정의

스토어 생성 - 사용 리듀서 알림 - 액션 콜백

액션 요청 - 액션 포맷 변환 후 돌려줌 - 스토어가 액션 받아서 루트 리듀서로 보냄 - 서브 리듀서 전달 - 서브리듀서 상태복사후 변경 후 다시 돌려줌 - 루트리듀서 상태트리로 전환후 스토어 돌려줌 - 스토어 상태 트리바꿈

- 바인딩에게 상태변화 알려줌 - 새로운 상태 변화 요청 - 바인딩이 뷰에 화면 업데이트 요청

## Promise.all 비동기처리

api를 action에 정의하여 5개의 api를 대시보드에서 한꺼번에 호출할때 토큰값이 없으면 error에 alert창이 다섯번이 뜨는일이 발생했다.

이를 해결하기 위해서는

함수안에 .then을 중첩으로 쓰거나,,

action/slice 단에 5개의 api를 하나로 엮어서 써야한다...~~야매임~~

그러다가 발견한 방법이 async/await 그리고 promise이다..

일반적으로 순차적인 것을 처리할때는 async/await를 많이 쓰고 순차적이지 않을때는 promise를 쓰는것 같은데,,

아직은 써본적인 없어서 잘 모르겠다.

반복문을 이용하여 비동기 처리를 하고 Promise 객체를 Promise.all에 넣고 한번에 결과를 확인하는 경우와 하나씩 비동기처리를 하는 경우.. 어떤 방식이 효율적인가 고민했을 때, 전자가 당연히 효율적일 것이다.

[참고]

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/all](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

[https://medium.com/@kiwanjung/번역-async-await-를-사용하기-전에-promise를-이해하기-955dbac2c4a4](https://medium.com/@kiwanjung/%EB%B2%88%EC%97%AD-async-await-%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-%EC%A0%84%EC%97%90-promise%EB%A5%BC-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-955dbac2c4a4)

## 지금 프로젝트...

현재 프로젝트는 3개의 admin프론트가 react-redux로 구현되어 있고, 1개의 프론트 페이지가 react-redux,next.js로 설계되었다.

잘만 따라가면 좋은 코드를 볼수있는 기회이니, 많이 봐두어야겠다. 
