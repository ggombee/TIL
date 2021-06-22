## 3. event에 api 추가하기

### axios

초반에는 간단히 slack api를 axios로 작성해서 post 해보았다.

초대코드를 통해 입장할때 버튼에다가 추가해주었다.

```jsx
onButtonClick = async () => {
    const TOKEN = "";

    if(this.user){
      try{
        axios({=
          method: "post",
          url:
              "https://slack.com/api/chat.postMessage",
          data: {
            text : `${this.user.displayName}님이 클래스룸에 입장하셨습니다.`,
            channel: "",
          },
          headers: {
            "Content-type": "application/json",
            Authorization: `Bearer ${TOKEN}`
          },
        }).then((response)=>{
          console.log(response)
        })
      }catch (e){
        console.log(e)
      }
    }
    await this.connect.enterWithCode(this.props.apolloClient, this.state.code);

    this.setState({
      code: "",
    });
  };
```

이렇게 해서 포스트를 계속 보냈는데 CORS error가 났다.

이를 잡기위해서

```jsx
url:
              "https://cors-anywhere.herokuapp.com/" +
              "https://slack.com/api/channels.list",
```

구글링 후 히로쿠 앱 서버 url을 추가해주니 이번에는 403 forbidden 에러가 났다.

CORS error는 해결했지만 계속나는 403에러를 잡을 수 있는 방법이 떠오르지 않았다.

그런데.. 아뿔싸 저 주소로 접속하니 프록시 서버형태로 구동을 해야 에러가 나지 않는 것이였다.

결국 우리 프로젝트에 프록시서버 환경을 구축해야 되는 문제가 발생하였다. 

현상황에서는 불가능하다고 판단되어 axios방법이 아닌 slack 라이브러리를 사용하여 만드는 방법으로 전환했다.

### slack webhook 라이브러리 활용

slack webhook라이브러리를 먼저 프로젝트에 추가해준다.

```jsx
$ yarn add @slack/webhook
```

추가 후 웹훅을 이용하여 api post를 해준다.

```jsx
onButtonClick = async () => {
    const token = "xoxb-";
    const channelId = ""

    const {WebClient} = require('@slack/web-api');
    const web = new WebClient(token);

    if(this.user){
      web.chat.postMessage({channel: channelId, text: `${this.user.displayName}님이 클래스룸에 입장하셨습니다.`});
    }
    await this.connect.enterWithCode(this.props.apolloClient, this.state.code);

    this.setState({
      code: "",
    });
  };
```

이렇게 하면 정상적으로 메시지가 가는것을 확인할 수 있다.

다만 여러 곳에서 웹훅을 호출하고 현재 서비스가 테스트,개발,운영환경에 나뉘어서 동작하다보니 슬랙에 한채널에 모든 로그를 보여주는 것 보다는 여러 채널에 환경에 따라 분리하여 찍어주는게 나을 것 같다는 생각이 들었다.

한 군데에서 여러 채널값과 토큰값을 효과적으로 쓸 수 있는 방법이 없을까 고민하던 중 env파일에 토큰값과 채널값을  정의 해놓고 사용하기로 했다.

<img width="380" alt="_2021-06-22__2 13 34" src="https://user-images.githubusercontent.com/58289110/122876851-f11dec00-d370-11eb-81ea-23883fc0f886.png">

.env파일에 각각 상황에 맞는 토큰과 채널값을 넣어주고

```jsx
NEXT_APP_SLACK_BOT_TOKEN="xoxb-"
NEXT_APP_SLACK_CHANNEL=""
```

해당 상수를 코드 상에서 process.env나 스토어를 이용해서 추출해서 사용하면 구동환경에 따라 다른 토큰값과 채널값을 사용해서 각각의 채널에 메시지가 전송되는 것을 확인할 수 있다.

아래와 같이 코딩했을때 직접적으로 코드상에 토큰값이나 채널값이 노출되지 않는다는 장점도 존재한다.

```jsx
onButtonClick = async () => {
    const token = `${this.store.environments.NEXT_APP_SLACK_BOT_TOKEN}`;
    const channelId = `${this.store.environments.NEXT_APP_SLACK_CHANNEL}`;
    const {WebClient} = require('@slack/web-api');
    const web = new WebClient(token);

    if(this.user){
      web.chat.postMessage({channel: channelId, text: `${this.user.displayName}님이 클래스룸에 입장하셨습니다.`});
    }
    await this.connect.enterWithCode(this.props.apolloClient, this.state.code);

    this.setState({
      code: "",
    });
  };
```
