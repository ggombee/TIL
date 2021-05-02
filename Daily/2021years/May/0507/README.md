# 6. 텍스트 마이닝

텍스트 마이닝은 비정형 텍스트에서 패턴, 관계 등을 분석하여 의미있는 정보를 도출해내는 데이터 마이닝 기법이다.

참고 : [https://parksrazor.tistory.com/516](https://parksrazor.tistory.com/516)

## 1. 삼성 2018 산업보고서 텍스트 마이닝

이 예제에서는 로컬에 데이터를 다운로드 해야 한다.

[data.zip](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/72eeb331-48a6-4164-96c9-cabc43526188/data.zip)

이 폴더에는 워드클라우드를 위한 폰트와 텍스트 마이닝 대상 파일, 제거할 노이즈 단어목록 파일을 포함하고 있다.

추가할 패키지는 KoNLPy 이다. 해당 패키지에 대한 홈페이지는 ([konlpy.org/ko/v0.5.2/install/#](https://konlpy.org/ko/v0.5.2/install/#)) 이다.

KoNLPy는 한국어 정보 전처리에 사용되는 파이썬 패키지다. 자연어처리(NLP)에서 **형태소를 분리**(형태소 단위 토크나이징)하는 데이터 전처리작업에서 많이 사용된다. KoNLPy 사이트는 설정하는 과정이 많이 생략되어 있어 이 블로그( [https://ebbnflow.tistory.com/143](https://ebbnflow.tistory.com/143))를 참조하는 것이 유용하다.

추가로 NLTK ([www.nltk.org/data.html](https://www.nltk.org/data.html)) 에 관한 지식이 필요하다. NLTK는 자연어 처리를 위한 파이썬 패키지이다. 설정하는 과정은 이 블로그 ([wikidocs.net/22488](https://wikidocs.net/22488)) 를 통해 참조하는 것이 유용하다.

에러시....

## JAVA 환경변수 설정

![Untitled](https://user-images.githubusercontent.com/58289110/117744058-eb49cc80-b242-11eb-9a49-81ad32b5aad5.png)

![Untitled (1)](https://user-images.githubusercontent.com/58289110/117744059-ebe26300-b242-11eb-83de-e34f3246281c.png)

![Untitled (2)](https://user-images.githubusercontent.com/58289110/117744060-ebe26300-b242-11eb-9477-645563518b43.png)

 
## 제이파이프 설치

![Untitled (3)](https://user-images.githubusercontent.com/58289110/117744061-ec7af980-b242-11eb-8e89-b515a98ee039.png)

## konlpy 설치

![Untitled (4)](https://user-images.githubusercontent.com/58289110/117744062-ec7af980-b242-11eb-8240-8b73bc8731b2.png)

## wordcloud 설치

![Untitled (5)](https://user-images.githubusercontent.com/58289110/117744064-ed139000-b242-11eb-821b-8dc7fce87438.png)

## nltk 설치

![Untitled (6)](https://user-images.githubusercontent.com/58289110/117744065-ed139000-b242-11eb-9612-fc57a5d50a83.png)

![Untitled (7)](https://user-images.githubusercontent.com/58289110/117744067-edac2680-b242-11eb-9ac6-852c2daf821e.png)

## 캐글 타이타닉 데이터 다운

![Untitled (8)](https://user-images.githubusercontent.com/58289110/117744068-edac2680-b242-11eb-9834-210d07f4666b.png)

## nltk 다운로드

![Untitled (9)](https://user-images.githubusercontent.com/58289110/117744071-eedd5380-b242-11eb-967b-2d16ae5e4fef.png)

![Untitled (10)](https://user-images.githubusercontent.com/58289110/117744074-ef75ea00-b242-11eb-82d3-e66f67302739.png)

[https://needjarvis.tistory.com/642](https://needjarvis.tistory.com/642)

![Untitled (11)](https://user-images.githubusercontent.com/58289110/117744077-ef75ea00-b242-11eb-8bce-a1be210aa166.png)
