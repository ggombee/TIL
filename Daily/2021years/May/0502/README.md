# 1. 개발 환경 설정

## 1. 아나콘다 설치

appwiz.cpl -- 애플리케이션 확인

![Untitled (2)](https://user-images.githubusercontent.com/58289110/117740285-13353200-b23b-11eb-86e8-9100180c5030.png)

![Untitled (3)](https://user-images.githubusercontent.com/58289110/117740284-129c9b80-b23b-11eb-9f92-4d11fe8f4538.png)

## 1. 아나콘다 시스템 변수 및 환경변수 설정

```jsx
ANACONDA_HOME1 C:\ProgramData\Anaconda3

ANACONDA_HOME2 C:\ProgramData\Anaconda3\Scripts

ANACONDA_HOME3 C:\ProgramData\Anaconda3\Library\bin

ANACONDA_HOME4 C:\ProgramData\Anaconda3\Library\mingw-w64\bin
```

위에 있는 아나콘다 설치 경로 및 이름을 변수 설정해준다

![Untitled (4)](https://user-images.githubusercontent.com/58289110/117740281-116b6e80-b23b-11eb-91ca-67f7cd054764.png)

시스템 변수와 환경변수를 설정해준다!

![Untitled (5)](https://user-images.githubusercontent.com/58289110/117740291-14665f00-b23b-11eb-8627-6e458befe666.png)

cmd 창을 열어 conda —version을 입력해서 버전 출력이 되면 설치 성공이다.

![Untitled (6)](https://user-images.githubusercontent.com/58289110/117740290-14665f00-b23b-11eb-9de8-3de78cd92471.png)

## 2. 파이참 설치

![Untitled (7)](https://user-images.githubusercontent.com/58289110/117740289-13cdc880-b23b-11eb-8cf4-73941fa0fa7b.png)

![Untitled (8)](https://user-images.githubusercontent.com/58289110/117740288-13cdc880-b23b-11eb-9cc5-93a5de69f89e.png)

## 3. git 레포지토리에 추가

```jsx
git init

git add .

git commit -m "first commit"

git remote add origin <GIT 주소>

git push -u origin master

git config --global user.name "<YOUR ID>“

git config --global user.email <EMAIL>
```
