[https://n1tjrgns.tistory.com/196](https://n1tjrgns.tistory.com/196)

[https://developer.mozilla.org/ko/docs/Web/HTTP/CORS](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)

heroku app 사용시 axios proxy 문제 발생

→ package.json proxy 해결 가능

구조상 적용 어려움

슬랙 web api 사용해서 적용

```jsx
$ yarn add @slack/web-api
```

슬랙 web api 6버전은 node 12이상 적용가능

현재 프로젝트 node 10버전으로 되어있음

npm에서 슬랙 web api 5버전 다운 후 적용

추후 node 버전 업그레이드 시 다시 슬랙 api도 업그레이드 할것..!

yarn clean → yarn으로 깔린 모듈 초기화

yarn

yarn bootstrap

yarn build 로 프로젝트 제 실행



npm, yarn이라는 자바스크립트 패키지 매니저가 있음.
저 친구들은 패키지를 프로젝트에 설치하거나 갱신 또는 삭제할 때 사용되는 도구.

package.json 파일에 해당 프로젝트가 의존하고 있는 모든 패키지 이름과 버젼을 명시
(dependencies : 설치되어야 하는 패키지 / devDependencies : 개발할 때만 필요한 패키지들)

-> npm i(stall) or yarn i(nstall) 명령어로 필요한 패키지를 모두 다운받을 수 있고, node_modules 디렉터리에 저장됨
(∴ package.json 파일만 있으면 다운받을 수 있으니 node_modules 디렉터리는 .gitignore에 추가한다)


but 패키지 버젼은 설치 시점에 따라 달라짐…;;
그래서 팀원마다 패키지의 버젼이 달라질 수 있고, 큰 문제가 생김

∴ 패키지 잠금이라는 개념을 패키지 매니져(npm, yarn)에서 지원


yarn이나 npm을 통해 프로젝트에 새로운 패키지를 설치하면

-> package.json에 해당 패키지가 등록 &&
-> 패키지 잠금 파일 (package-lock.json, yarn.lock)이 생성!!

패키지 잠금 파일 에는 프로젝트에 패키지가 최초로 추가될 당시의 버젼을 기록함!!

-> 패키지 잠금 파일 이 생성된 이후에는 npm i와 같은 명렁어를 수행해도 npm registry에 등록한 최신 버젼을 설치하지 않음!

대신 항상 패키지 잠금 파일 에 명시되어 있는 버젼으로 패키지를 설치해주기 때문에, 설치 시점에 상관없이 항상 동일한 버젼의 패키지가 설치됨을 보장받음!

그래서 패키지 잠금 파일 인 package-lock.json파일을 git에 추가하여 올려두면,

다른 사람들도 package.json 파일 뿐 아니라 package-lock.json 파일도 내려받음

그럼 모든 개발자의 pc와 배포되는 서버도 package-lock.json에 기록된 버젼 기준으로 패키지가 설치!!! 😀

<img width="566" alt="Untitled" src="https://user-images.githubusercontent.com/58289110/122716657-818efa80-d2a5-11eb-9732-d3011872ead2.png">

<img width="698" alt="_2021-06-18__1 49 44" src="https://user-images.githubusercontent.com/58289110/122716626-776cfc00-d2a5-11eb-918f-f4fa94fe3051.png">

<img width="1067" alt="_2021-06-18__2 20 51" src="https://user-images.githubusercontent.com/58289110/122716750-a1262300-d2a5-11eb-889e-9edb51fabb14.png">

주의 사항!
프로젝트 최초 셋팅하는 개발자는 패키지 잠금 파일 을 git 저장소에 무조건 올려야 한다!

패키지 잠금 파일 은 패키지 매니져가 패키지의 변동(새로운 설치 or 갱신/제거)이 있을 때
package.json과 자동으로 동기를 맞춰주기 때문에 개발자가 이 파일을 직접 수정해야 할 필요는 없고 하면 안됨!

신규 패키지를 설치하거나 갱신/제거한 개발자는 package.json과 더불어 함께 업데이트 된 패키지 잠금 파일 을 반드시 커밋해야 함!!
