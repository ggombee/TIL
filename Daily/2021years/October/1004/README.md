# 브라우저의 동작원리

1. HTML 마크업을 처리하고 DOM트리를 빌드한다. ("무엇을" 그릴지 결정)

   ![Screen Shot 2021-12-09 at 11.44.14 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/02784635-cd7f-4f6c-a9ee-24ce1bc155e2/Screen_Shot_2021-12-09_at_11.44.14_AM.png)

2. CSS 마크업을 처리하고 CSSOM 트리를 빌드한다. ("어떻게" 그릴지 결정)
3. DOM 및 CSSOM 을 결합하여 렌더링 트리를 형성한다. (**"화면에 그려질 것만"** 결정)
4. 렌더링 트리에서 레이아웃을 실행하여 각 노드의 기하학적 형태를 계산한다. (**"Box-Model"** 을 생성한다.)
5. 개별 노드를 화면에 페인트한다.(or 래스터화)

![Screen Shot 2022-01-24 at 1.49.34 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/381d0b3f-a171-47e6-807f-9a4301baff31/Screen_Shot_2022-01-24_at_1.49.34_PM.png)

### DNS

도메인 네임과 해당하는 ip주소값을 한쌍으로 저장하고 있는 데이터베이스를 DNS라고 부른다.

![Screen Shot 2022-01-24 at 1.52.05 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e3378ccf-c508-4b62-ba10-0e566fd5ff1e/Screen_Shot_2022-01-24_at_1.52.05_PM.png)

S

---

출처

- [Naver D2 - 브라우저의 작동 원리](http://d2.naver.com/helloworld/59361)
- [Web fundamentals - Critical-rendering-path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/?hl=ko)
- [브라우저의 Critical path (한글)](http://m.post.naver.com/viewer/postView.nhn?volumeNo=8431285&memberNo=34176766)
