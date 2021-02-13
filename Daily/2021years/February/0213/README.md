## GitLab 연결

1. git bash를 사용하는 방법

- 기초설정

> $ git config --global user.name "깃헙이름"

> $ git config --global user.email 이메일@도메인

> 설정내용 확인 $ git config --list

> 디렉토리 이동 방법 (cd 폴더명, cd.. 등)

- 현재 폴더를 git 로컬 저장소로 등록

> $ git init

> 폴더 옆에 <master> 표시되면 성공

- 커밋

> $ git commit -m 'initial commit'

- 원격 저장소 추가

> $ git remote add origin 깃허브URL([https://github.com/HyeongJunMin/Bitcamp.git)](https://github.com/HyeongJunMin/Bitcamp/)

> $ git push origin master

**- 폴더 삭제(드디어..!)**

**> $ git rm -r 대상폴더이름(pracProject190514_operator/bin)**

**> $ git commit -m 'delete 대상폴더이름(pracProject190514_operator/bin)'**

**> $ git push origin master**

**> 삭제 성공!!**
