## 2. slack api

먼저 slack api 공식 홈페이지에서 어떤 방식으로 메시지를 보낼지 생각해보았다.

api는 먼저 [chat.postMessage](https://api.slack.com/methods/chat.postMessage)라는 api를 이용하면 될 것 같았다.

요청 파라미터 보낼때 특정 채널의 ID를 보내야 해서 이는 channellist라는 api를 통해 확인하거나 슬랙 브라우저로 접속하여 확인하면 된다.

<img width="463" alt="_2021-06-21__3 58 31" src="https://user-images.githubusercontent.com/58289110/122876179-2a099100-d370-11eb-8719-4976f9b318e1.png">

위 사진에서 url의 첫번째말고 두번때 네모칸에 있는게 해당 채널의 아이디다.

개개인의 계정보다는 하나의 봇을 만들어서  봇이 채널에 입장로그를 뿌리는 것이 더 효율적이라고 생각 되어 봇을 먼저 만들었다.

봇은 [슬랙 api](https://api.slack.com/) 홈페이지에서 만들 수 있다.

Create a custom app > Create New App 에서 봇을 만든 뒤 OAuth & Permissions에 들어가서  Scopes를 추가해준뒤 봇토큰을 발급받는다.

<img width="669" alt="_2021-06-21__4 26 31" src="https://user-images.githubusercontent.com/58289110/122876213-32fa6280-d370-11eb-98c7-80c4f9c14a4a.png">

봇토큰 발급이 완료되면 Install to Workspace로 나의 Workspace에 추가해준뒤 해당 채널에서 앱을 추가해주면 준비는 완료된다.

정상적으로 완료되었는지 확인해보기 위해서는 해당값들을 이용하여 [api teste](https://api.slack.com/methods/chat.postMessage/test)r로 전송해보면 된다.

메시지가 정상적으로 해당 채널에 전송되면 권한과 토큰 설정이 제대로 된 것이다.
