### 페인트

레이아웃 단계를 통해 화면에 배치된 엘리먼트들에게 색을 입히고 레이어의 위피를 결정하는 단계이다.

이 단계 역시 루트 오브젝트로부터 재귀적으로 실행이 됩니다. 또한 레이아웃과 마찬가지로 페인팅에도 **전역적 페인팅**과 **증분적 페인팅**이 있다.

즉, 문서가 클수록 브라우저가 수행해야 하는 작업도 더 많아지며, 스타일이 복잡할수록 페인팅에 걸리는 시간도 늘어난다. 예를 들어, 단색은 페인트하는 데 시간과 작업이 적게 필요한 반면, 그림자 효과는 계산하고 페인트 하는데 시간과 작업이 더 필요하다.

페인팅에는 그 순서가 있는데, 이는 `z-index` 축을 이용한 [쌓임 맥락(Stacking context)](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)과도 일맥상통한다. 때문에 `z-index`가 낮은 순서대로 먼저 페인팅이 된다.

한편 블록 단위에서의 페인팅 순서는 [CSS 페인팅 명세](https://www.w3.org/TR/CSS21/zindex.html#painting-order)에 따르면 다음과 같다.

> background-color
background-image
border
children
outline

따라서 만약 background-color와 background-image 가 함께 세팅되어 있고, background-image로 설정한 외부 리소스의 크기가 크다면 background-color 를 먼저 보게 될 것이고, 나중에 이미지가 완전히 로드된 후 background-image로 교체가 될 것이다.
