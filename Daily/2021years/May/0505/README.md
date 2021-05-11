- Beautiful Soup
    - Beautiful Soup 정의
    - Beautiful Soup 설정하기
    - 벅스뮤직 예제
    - 위키피디아 예제


# 1. 정의

Beautiful Soup은 HTML과 XML 문서를 구문 분석하기 위한 파이썬 패키지이다. HTML에서 데이터를 추출하는 데 사용할 수 있는 구문 분석된 페이지에 대한 구문 분석 트리를 만든다. 이것은 웹 스크래핑에 유용하다.[위키백과]

# 2. Beautiful Soup 설정하기

[pypi.org/project/](https://pypi.org/)로 접속한다.

Beautiful Soup을 검색한다.beautifulsoup4 <버전> 을 선택한다.

![Untitled](https://user-images.githubusercontent.com/58289110/117743190-467abf80-b241-11eb-9435-b3c0b141242b.png)

이 예제에서는 PIP 로 패키지를 설치하는 학습이 필요하다.

패키지는 특정 기능을 수행하기 위한 함수들을 모아놓은 라이브러리(모듈)이다.

PIP란 패키지 소프트웨어를 설치, 관리하는 시스템이다.

![Untitled (1)](https://user-images.githubusercontent.com/58289110/117743193-47abec80-b241-11eb-988f-0737603e9d23.png)

아래의 패키지를 터미널에서 추가해준다.

```jsx
pip install beautifulsoup4
```

![Untitled (2)](https://user-images.githubusercontent.com/58289110/117743196-48448300-b241-11eb-8931-b32672923006.png)

```jsx
pip install beautifulsoup4pip install lxml
```

![Untitled (3)](https://user-images.githubusercontent.com/58289110/117743197-48dd1980-b241-11eb-8fb2-8049a24f95cd.png)

[벅스뮤직 예제](https://music.bugs.co.kr/chart/track/realtime/total?chartdate=20181124&charthour=10music.bugs.co.kr/chart/track/day/total?chartdate=20210505)

[위키피디아 예제](http://dh.aks.ac.kr/Encyves/wiki/index.php/%EC%A1%B0%EC%84%A0_%EC%84%B8%EC%A2%85)

스크랩핑하는 모듈을 작성한다.

이 예제에서는 다음과 같은 선행 지식이 필요하다. 이 문법을 CSS 셀렉터라고 한다. [참조사이트 [www.w3schools.com/cssref/css_selectors.asp](https://www.w3schools.com/cssref/css_selectors.asp)]

- a.get('href') 태그 a 에서 href 속성의 값(하이퍼링크 url) 추출하기
- soup.title.name title 태그의 이름 title 추출하기
- soup.title.string title 태그의 문자값 추출하기
- soup.['class'] 클래스 추출
- soup.find(id = 'link') 아이디가 link 인 태그와 값 추출
