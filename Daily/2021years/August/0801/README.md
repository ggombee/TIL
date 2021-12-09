# 웹 성능과 관련된 이슈

### **1. 네트워크 요청에 빠르게 응답하자**

- `3.xx` 리다이렉트를 피할 것
- `meta-refresh` 사용금지
- `CDN(content delivery network)`을 사용할 것
- 콘텐츠 전송 네트워크는 콘텐츠를 효율적으로 전달하기 위해 여러 노드를 가진 네트워크에 데이터를 저장하여 제공하는 시스템을 말한다. 인터넷 서비스 제공자에 직접 연결되어 데이터를 전송하므로, 콘텐츠 병목을 피할 수 있는 장점이 있다.
- 동시 커넥션 수를 최소화 할 것
- 커넥션을 재활용할 것

### **2. 자원을 최소한의 크기로 내려받자**

- 777K
- `gzip` 압축을 사용할 것
- `HTML5 App cache`를 활용할 것
- 자원을 캐시 가능하게 할 것
- 조건 요청을 보낼 것

### **3. 효율적인 마크업 구조를 구축하자**

- 레거시 IE 모드는 http 헤더를 사용할 것
- @import 의 사용을 피할 것
- inline 스타일과 embedded 스타일은 피할 것
- 사용하는 스타일만 CSS 에 포함할 것
- 중복되는 코드를 최소화 할 것
- 단일 프레임워크를 사용할 것
- Third Party 스크립트를 삽입하지 말 것

### **4. 미디어 사용을 개선하자**

- 이미지 스프라이트를 사용할 것 ( 하나의 이미지로 편집해서 요청을 한번만 보낸다의 의미인가? )
- 실제 이미지 해상도를 사용할 것
- CSS3 를 활용할 것
- 하나의 작은 크기의 이미지는 DataURL 을 사용할 것
- 비디오의 미리보기 이미지를 만들 것

### **5. 빠른 자바스크립트 코드를 작성하자**

- 코드를 최소화할 것
- 필요할 때만 스크립트를 가져올 것 : flag 사용
- DOM 에 대한 접근을 최소화 할 것 : Dom manipulate 는 느리다.
- 다수의 엘리먼트를 찾을 때는 selector api 를 사용할 것.
- 마크업의 변경은 한번에 할 것 : temp 변수를 활용
- DOM 의 크기를 작게 유지할 것.
- 내장 JSON 메서드를 사용할 것.

### **6. 애플리케이션의 작동원리를 알고 있자.**

- Timer 사용에 유의할 것.
- `requestAnimationFrame` 을 사용할 것
- 활성화될 때를 알고 있을 것

### **Reference**

- [HTML5 앱과 웹사이트를 보다 빠르게 하는 50 가지 - yongwoo Jeon](https://www.slideshare.net/mixed/html5-50)