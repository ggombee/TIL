# 리플로우와 리페인트

렌더트리 생성을 하는 과정에서 각각의 높이와 너비등을 계산하는 플로우 작업이 일어나는데 리플로우는 이과정을 다시 거치는것을 의미합니다.

그리고 렌더 트리 과정에서 플로우를 통해 계산한 것을 그리는 과ㅓㅇ이 바로 페인트입니다.

렌더 트리 생성이 끝나면 배치가 시작된다.

**레이아웃 단계는 트리를 생성하면서 계산된 노드와 스타일을 기기의 뷰포트에서 어떤 위치에서 어떻게 보이도록 하는지 결정하는 단계이다.**

레이아웃 프로세스는 뷰포트 내에서 각 요소의 정확한 위치와 크기를 캡쳐하는 '상자 모델'이 출력되며 상대적인 측정값도 모두 절대적인 픽셀로 변환된다.

레이아웃 과정 즉, 리플로우는 최초 한 번만 실행되고 끝나는 것이 아니라 width, height, left, top, offsetHeight, offsetWidth, scrollTop 등 수치를 계산해 새로운 위치에 나타나게 하는 동작이 일어날 때마다 반복해서 실행된다.

모든 렌더러는 '배치' 또는 '리플로' 메서드를 갖는데 각 렌더러는 배치해야 할 자식의 배치 메소드를 불러온다.

layout 알고리즘으로는,

각 박스의 넓이는 viewport 기준,각 박스의 높이는 contents(font) 기준으로 배치가 된다.

**소소한 변경 때문에 전체를 다시 배치하지 않기 위해서는 브라우저는 더티 비트 체제를 사용하여 점층적인 배치를 한다.** 렌더러는 다시 배치할 필요가 있는 변경 요소 또는 추가된 것과 그 자식을 더티라고 표시하는 것이다.

반대로 렌더러 트리 전체에서 일어날 수 있는 전역 배치(global layout)에는, 윈도우 사이즈를 변경하거나 폰트 크기 변경과 같은 사항에서 발생한다.

배치에 따라 동기와 비동기적인 실행도 달라지는데, 점층 배치는 렌더러가 더치일 때 비동기적으로 일어난다. 예를 들면 네트워크로부터 추가 내용을 받아서 DOM 트리에 더해진 다음 새로운 렌더러가 렌더 트리에 붙을 때이다.

웹킷의 경우 점증 배치를 실행하는 타이머가 있는데 트리를 탐색하여 더티 렌더러를 배치한다. offsetHeight 같은 스타일 정보를 요청하는 스크립트는 동기적으로 점증 배치를 실행한다.

전역 배치는 보통 동기적으로 실행된다. 때때로 배치는 스크롤 위치 변화와 같은 일부 속성들 때문에 초기 배치 이후 콜백으로 실행된다.

또한**렌더링 엔진은 좀 더 나은 사용자 경험을 위해 가능하면 빠르게 내용을 표시하는데 모든 HTML을 파싱할 때까지 기다리지 않고 배치와 그리기 과정을 시작한다.**

네트워크로부터 나머지 내용이 전송되기를 기다리는 동시에 받은 내용의 일부를 먼저 화면에 표시하는 것이다.