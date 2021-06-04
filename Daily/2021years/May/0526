# 1. Overall Technical Stacks

- TypeScript
- Node.js (V.10.24.1)
- React.js (Mobx V5)
- GraphQL
- next.js (V8)

# 2. Dev Setting

1. nvm install
2. yarn install

    ```jsx
    install with brew

    $ brew install yarn --without-node # node 가 설치되어있다면
    $ brew install yarn # node 가 없다면

    install with npm

    $ npm install --global yarn
    ```

3. clone projects from github
4. cd classroom, install package

    ```jsx
    $ yarn

    $ yarn bootstrap

    $ yarn build

    ```

5. git token setting
    1. github > Settings > Developer Settings > Personal Access Tokens - make token


         2. open terminal

        insert (a)

        ```jsx
        $ vi ~/ .zshrc
        ```

        add 

        ```jsx
        export GITHUB_TOKEN=token
        export FONTAWESOME_TOKEN=token
        ```

        exit (:wq)

        re

        ```jsx
        $ sh ~/ .zshrc
        ```

6. run

    ```jsx
    $ yarn dev
    ```

# 3.  Services

(SaaS Dependencies)

1.  서버는 AWS 배포 후 사용중
    - DynamoDB 제외 온프레미스로 전환가능
    - 수업 어플리케이션의 경우 DB 의존성이 낮아 쉽게 다른 DB로 전환 가능
    - Kubernetes 등 오픈소스 기술을 통해 온프레미스로 전환 가능
2. WebRTC 음성/영상 서비스로 Twolio Programmable Video 사용
    - 오픈소스 기술 활용하여 구축 가능 ( Agora 전환 예정)

# 4. Softwares

각 서비스, SDK, 플러그인 등은 Lerna를 통해 단일 Git 레포지토리로 관리 중

CircleCI를 통해 코드 Commit시 업데이트가 필요한 서비스 즉각 배포

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6baecd90-a193-417e-be06-d23378a83d17/_2021-06-08__1.50.12.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6baecd90-a193-417e-be06-d23378a83d17/_2021-06-08__1.50.12.png)

## Request-Response Interface

부모에서 특정함수를 레지스트리에 등록

자식이 sdk를 총해 해당함수의 이름과 arguments로 요청

해당정보를 모아 부모에 전송

등록한 함수가 특정값을 리턴하면 해당값을 자식에게 리턴해줌

—> 각 메시지별 uuid 생성

—> 응답메시지에 요청 메시지의 ID를 넣어 1:1 대응 관계를 만들어줌

## Action - Reaction Interface

예를들어 이미지 업로드시 업로드 퍼센트 구현

부모에서 특정함수 레지스트리 등록

자식 sdk 통해 해당함수의 이름과 arguments 요청

응답에 promise가 아닌 on을 노출

해당정보를 모아 부모로 전송

부모가 함수를 실행하면서 첫번째 argument 리액트 함수 실행 

함수 실행시마다 응답값이 날아오게 되고 올때마다 listener작동함

—> 각 메시지별 uuid 생성

—> 응답메시지에 요청 메시지의 ID를 넣어 1:N 대응 관계를 만들어줌

## One-way Binding Interface

iframe을 리액트 컴포넌트로 감싸서 특정 props를 받을 수 있게 함

처음 컴포넌트가 initialize 될때/ props의 값이 바뀔때마다 자식에게 메시지가 가고

이를 sdk 내부의 mobx가 받아서 해당 sdk를 subscirbe하고 잇는 컴포넌트를 다시 그려주는 방식

observer사용 변경사항 감지

의존성을 줄이면서 안정적인 웹앱 제작가능

## 공용 메시지 프로토콜

메시지마다 생성되는 uuid + 메시지 생성시간 + 메시지가 생성된 인스턴스의 ID + 메시지를 생성한 user ID + 이벤트 이름 string + 내용 (message payload)

## 구현

### Core

- 메시지 생성
- 메시지 송수신
- 메시지 처리
- 메시지 리스너 등록

### Deployment

- 기능 사이 의존성 최소화
- 통신 공통의 프로토콜로 가능하도록 설계
- 춘분히 고도화된 하나의코드로 관리
- 오류가 발생하더라고 전체 앱은 멈추지 않음
- 쉽게 개발할 수 있도록 함
