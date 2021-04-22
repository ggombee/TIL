## 2. 렌더링 엔진의 동작과정

우리가 어떤 웹 페이지에 접속하면, 네트워크를 통해 해당 웹 페이지의 html 문서를 얻어온다. 렌더링 엔진은 읽어들인 html문서를 해석한다. 각 브라우저 엔진마다 해석 방식이 조금씩 다르지만, 크게 4단계로 이루어져 있다고 봐도 무방하다.

- 파싱
- 렌더 트리 구축
- 레이아웃 또는 리플로우
- 페인트

위에서 이야기한 모든 과정들을 **중요 렌더링 경로**라고 부른다.

각 단계에서 리소스를 로드하는 순서나 작성한 스크립트의 내용에 따라 웹페이지의 반응 속도가 달라질 수 있다.

이러한 과정의 최적화를 통해 프론트엔드 개발자는 렌더링에 걸리는 시간을 개선시키고, 사용자 경험을 방해하지 않을 수 있다.

각 단계에 대해 자세히 알아보자.

### 파싱

파싱은 토큰화된 코드를 구조화하는 과정을 말한다.

이러한 파싱 과정을 전문적으로 해주는 부분을 파서라고 부른다.

> 정확하게는 어휘분석기를 통해 토큰화된 코드가 생성되고, 이를 파서가 해석하는 순서로 이루어진다. 토큰화라는 것은 의미가 있는 최소 단위로 코드를 쪼개는 것을 의미한다.

파싱 과정은 입력받은 문자열이 정해진 문법들을 모두 따르는지 확인 하는 과정이다.

각 문법은 어휘와 문법 규칙으로 구성되어 있는데 어휘는 알파벳이나 한글처럼 사용할 수 있는 단어와 그 조합들을 의미하며, 문법 규칙은 어휘 사이에 적용될 수 있는 규칙들을 의미한다. 

브라우저는 HTML,CSS,JavaScript 세 종류의 언어를 해석할 수 있다.

그 중에서 JavaScript 는 렌더링 엔진 레이어가 아니라 JavaScript 해석기라는 별도의 레이어에서 언어를 해석한다. 따라서 렌더링 엔진에서는 HTML과 CSS를 파싱한다.
