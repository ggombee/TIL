# 1. 셀레니움과 크롬 드라이버

## 1. 셀레니움 설정하기

아래의 패키지를 터미널에 추가해준다.

```jsx
pip install selenium
```

## 2. 크롬드라이버 설정하기

크롬 브라우저 우측 상단에 세로 점3개을 클릭 후 설정탭을 선택한다. 좌측 Chrome 정보를 클릭한다. <그림2>와 같이 크롬 버전을 확인한다. [chromedriver.chromium.org/downloads  에 접속한다.](https://chromedriver.chromium.org/downloads)

버전과 일치하는 드라이버를 <그림3> 처럼 선택한 후 본인 OS 와 맞춰서 다운받는다.

다운받은 드라이버를 C:/Program Files/Google/Chrome 에 저장한다.

해당 프로젝트의 경로를 카피해서, 작업 중인 모듈에 입력한다.

![Untitled (5)](https://user-images.githubusercontent.com/58289110/117743643-20a1ea80-b242-11eb-97a4-102c63cddaa0.png)

[네이버 영화 예제](https://movie.naver.com/movie/sdb/rank/rmovie.nhn)

이 예제에서는 html parser 에 대한 지식이 필요하다. [참고사이트]( [docs.python.org/ko/3/library/html.parser.html)](https://docs.python.org/ko/3/library/html.parser.html)

그리고, List Comprehension을 사용한 for 문에 대한 내용은 다음과 같다.

a = [1,2,3,4]

result = [ i * 3 for i in a if i % 2 == 0 ]

print(result)

[6, 12]

네이버 자동로그인
