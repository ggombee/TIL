1. HTML 마크업을 처리하고 DOM트리를 빌드한다. ("무엇을" 그릴지 결정)

2. CSS 마크업을 처리하고 CSSOM 트리를 빌드한다. ("어떻게" 그릴지 결정)
3. DOM 및 CSSOM 을 결합하여 렌더링 트리를 형성한다. (**"화면에 그려질 것만"** 결정)
4. 렌더링 트리에서 레이아웃을 실행하여 각 노드의 기하학적 형태를 계산한다. (**"Box-Model"** 을 생성한다.)
5. 개별 노드를 화면에 페인트한다.(or 래스터화)

---

출처

- [Naver D2 - 브라우저의 작동 원리](http://d2.naver.com/helloworld/59361)
- [Web fundamentals - Critical-rendering-path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/?hl=ko)
- [브라우저의 Critical path (한글)](http://m.post.naver.com/viewer/postView.nhn?volumeNo=8431285&memberNo=34176766)