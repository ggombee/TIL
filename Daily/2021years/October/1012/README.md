# event loop

- V8 엔진에서 코드가 실행되면, Call Stack에 쌓인다.
- Stack의 선입후출의 룰에 따라 제일 마지막에 들어온 함수가 먼저 실행되며,Stack에 쌓여진 함수가 모두 실행된다.
  - 비동기함수가 실행된다면, Web API가 호출된다.
  - Web API는 비동기함수의 콜백함수를 Callback Queue에 밀어넣는다.
  - Event Loop는 Call Stack이 빈 상태가 되면Callback Queue에 있는 첫번째 콜백을 Call Stack으로 이동시킨다.(이러한 반복적인 행동을 틱(tick)이라 한다.)
