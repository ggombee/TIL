# MAC 터미널 꾸미기

## 잘쓰다가 갑자기 왜 포스팅..?

### 사실 구글링 하면 해결된다.. 😂

이직을 하거나 새로운 기기에 터미널 세팅을 할때마다 외워놓은 명령어를 이용해서 하고 기억이 안날때마다 구글링을 통해 해결하곤 했는데...

최근 M1과 BigSur의 등장으로 어마무시하게 나와 관련없는 정보들이..(~~M1관련 script..~~) 넘쳐흐른 탓인지..

오늘..! 맥북 pro를 초기화 하고 다시 설정하는데... 알수 없는 오류들때문에.. 시간을 너무 날려서.. 나를  위한 정리를 해놓으려고 한다..!

## 본격 iTerm 세팅편

### 1. iTerm 설치

간단하다.
[iTerm 공식 사이트](https://iterm2.com/)에 방문해서 다운로드만 하면 된다.
여기까지는 모든 것이 순조로웠다..

- *다운로드 후 바로 사용해도 무관하지만 나의 윤택한 개발 생활을 위해.. 테마를 적용해 보도록 하자!!
**

### 2. homebrew 설치

(~~전쟁의 서막...~~)

하던대로...했는데... 왜 자꾸 에러가...??!

예전에는 마구 검색해서 마구 적용하면 따란 하고 적용됬는데,,
지금은 각 OS마다 CPU마다 환경변수 설정을 달리 해주어야 한다고 한다.

먼저 iTerm을 켜고,
homebrew 사이트에 들어가 환경에 맞는 스크립트를 찾아서 입력한다.

내 맥북은 intel칩을 사용하였고 현재는 Big Sur 업데이트를 한 상태이다.

따라서 아래 스크립트를 실행하였다.

```
$ /bin/bash -c "$(curl -fsSL <https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh>)"

```

스크립트를 실행하고 맥북의 비번 입력후 엔터를 치면 다운로드가 완료 된다.

그리고 brew --version 이나 brew config를 통해 설치여부를 확인할 수 있는데,  config를 이용해서 설치 경로를 다시 한번 확인하는 것을 추천한다..!

- *만약!! brew를 찾을 수 없다는 오류가 발생한다면!!
(에러가 안나면 쭈욱 내리세용)
**

vi ~/.zshrc에 들어가서 환경변수를 설정해주면 되는데,,
이때 각 OS마다 CPU의 버전마다 방법이 상이하다.

기존의 방법은 아래 스크립트를 zshrc파일에 추가하면 되는데

```
export PATH=/usr/local/bin:$PATH

```

M1 등 특정 기기는

```
eval $(/opt/homebrew/bin/brew shellenv)

```

이 스크립트를 넣으면 된다.

### 3. oh-my-zsh 설치

다음은 zsh와 oh-my-zsh를 설치한다.
iTerm에서 아래 명령어를 차례로 입력해준다.

```
# zsh install
$ brew install zsh

# oh-my-zsh install
$ sh -c "$(curl -fsSL <https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh>)"

```

<img width="565" alt="스크린샷 2021-07-27 오전 4 49 18" src="https://user-images.githubusercontent.com/58289110/127143855-1ceafa7c-8baa-499b-9deb-3d281f5a1a6a.png">

이렇게 뜨면 성공이다!
사실 여기까지만 해도... 터미널 입문자들에겐 삐까번쩍 세계가 보이겠지만..!!!! ~~만족스럽다면 창을 나가도..~~

추가로.. 사용자명 지우기, 테마 바꾸기, 줄바꿈, 자동완성, 하이라이팅 기능도!!! 보너스로..!! (~~다른곳가면 따로 찾아봐야..읍!!~~)

### 4. 사용자명 지우기

vi ~/.zshrc에 들어가서 아래 코드를 추가해준다.

```
# DEFAULT_USER
DEFAULT_USER="$(whoami)"

```

추가 후 재시작을 하거나 source ~/.zshrc 등을 해주면 적용된 것을 확인할 수 있다.

### 5. theme 변경

터미널의 테마를 변경해보도록 하자.
사용할 테마는 agnoster라는 테마인데 이 테마로 현재 checkout중인 branch를 손쉽게 확인할 수 있다.

<img width="485" alt="스크린샷 2021-07-27 오전 5 10 48" src="https://user-images.githubusercontent.com/58289110/127143875-facfab00-769a-4ad7-9319-570837a820cd.png">

vi ~/.zshrc	에 들어가서 robbyrussell이라고 되어있는 부분을 agnoster로 변경한다.
(~~지금보니 사진에 default 오타가..~~)

여기까지 적용하면.. 와장창 폰트가 깨진다..!!
이건 [d2codingfont](http://github.com/naver/d2codingfont)를 받아서 해결해준다.
(서체관리자에서 적용가능)

### 6. 줄바꾸기

긴 스크립트를 입력하다보면 끝이잘려 불편할 때가 많은데,
이때 아주 유용한 new line을 설치해보자.

agnoster 테마에 맞추어 아래 명령어로 편집창을 연다.

```
$ vi ~/.oh-my-zsh/themes/agnoster.zsh-theme

```

편집창에서 build_prompt내의 prompt_newline을 추가한다.
이때 반드시 end보다 위에 저위치에 넣어주어야 된다!!!

그리고 아래

```
prompt_newline() {
  if [[ -n $CURRENT_BG ]]; then
    echo -n "%{%k%F{$CURRENT_BG}%}$SEGMENT_SEPARATOR
%{%k%F{blue}%}$SEGMENT_SEPARATOR"
  else
    echo -n "%{%k%}"
  fi
  echo -n "%{%f%}"
  CURRENT_BG=''
}

```

아래화면처럼 이것도 추가해준다.

<img width="482" alt="스크린샷 2021-07-27 오전 5 26 18" src="https://user-images.githubusercontent.com/58289110/127143896-4b94dcb5-3969-46f2-b4fc-99d9e5ee3623.png">

그러면 줄바꿈된 라인에서 명령어가 입력된다!

<img width="207" alt="스크린샷 2021-07-27 오전 5 31 25" src="https://user-images.githubusercontent.com/58289110/127143908-23e83011-8514-4d2b-bd80-1a81597e5c0b.png">

### 7. 하이라이팅

~~휴.. 이제 두개 남았다..~~
하이라이팅 기능을 활용하면 잘못된 명령어를 쉽게 거를 수 있다.

아래 스크립트를 통해 플러그인을 설치 후 zshrc에 플러그인을 추가해준다.

```
$ brew install zsh-syntax-highlighting

```

```
# vi ~/.zshrc
plugins=(
  git
  zsh-syntax-highlighting
)

```

**만약..!! not found 에러가 뜬다면**
아래 스트립트를 실행해준다.

```
$ git clone <https://github.com/zsh-users/zsh-syntax-highlighting.git> ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting

```

이 스크립트는 다시 설치한다는 의미를 내포하므로 상단에서 추가한 plugins안에 zsh-zyntax-highlighting 줄을 지우는 것을 추천한다고 한다.
~~나는 따로 에러가 안나길래 그냥 뒀다.~~

### 8. 대망의.. 마지막!@! 자동완성🤩

자동완성 플러그인을 이곳을 참고하여 추가한다.
아래 스크립트 통해 설치 후 zshrc파일에 zsh-autosuggestions를 추가한다.

```
$ git clone <https://github.com/zsh-users/zsh-autosuggestions> ~/.zsh/zsh-autosuggestions

```

- *
이런...! 마지막까지..! 또 에러가 난다면..**
zshrc파일에 추가한 zsh-autosuggestions을 삭제하고,
아래 스크립트를 마지막에 추가해주면.. 정상적으로 실행된다..!!

<img width="151" alt="스크린샷 2021-07-27 오전 5 51 45" src="https://user-images.githubusercontent.com/58289110/127143927-f37b006a-a048-4e20-95e1-33d2a62d05b1.png">

완성된 화면을 보니 편-안..
색은 command+, 눌러서 각자 맞춰서 바꿔도 되고, 컬러테마 다운받아도 된다!!

내가 편하자고 만든 포스팅이지만,, 너무 길어져서 가독성이 많이 떨어지는 것 같다..
그래도 누군가는 북마크해서 찾아보겠지..ㅎㅎ (나라도..)

다들 개발속도 향상하세여~!!
그럼 20000..
